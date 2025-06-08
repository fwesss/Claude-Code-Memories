# Testing Best Practices

Based on Kent C. Dodds' "Common Testing Mistakes" principles.

## Core Testing Philosophy

- **Primary Goal**: Tests should provide confidence that the application works
- **Golden Rule**: "The more your tests resemble the way your software is used, the more confidence they can give you"
- Focus on testing behavior, not implementation details
- Test what users actually experience, not internal code mechanics

## Key Principles

### 1. Avoid Testing Implementation Details

**Definition**: Implementation details are things users of your code will not typically use, see, or know about.

**Why Avoid**:

- **False Negatives**: Tests break during refactoring even when functionality is unchanged
- **False Positives**: Tests pass despite actual functional problems

**Implementation Details to Avoid**:

- Component internal state (e.g., `wrapper.state('openIndex')`)
- Private methods and internal APIs
- Specific CSS class names or DOM structure
- Internal component lifecycle methods
- Hook implementation details

**Focus Instead On**:

- User interactions (clicks, typing, form submissions)
- Visible text and UI elements
- Accessible roles and labels
- Network requests and responses (from user perspective)
- Observable behavior and outcomes

**Example**:

- ❌ `expect(component.state.isLoading).toBe(true)`
- ✅ `expect(screen.getByText('Loading...')).toBeInTheDocument()`

### 2. Don't Obsess Over 100% Code Coverage

- Code coverage tells you code was executed, not that it works correctly
- Focus on testing critical application paths and user journeys
- High-value tests > high coverage percentage
- Better to have 80% coverage of important features than 100% coverage of trivial code

### 3. Optimize E2E Test Efficiency

- **Problem**: Repeatedly running full registration/login flows in every test
- **Solution**: Use direct HTTP calls or test utilities to set up test state
- Maintain test isolation while eliminating unnecessary UI repetition
- Reserve full user flows for critical path testing

### 4. AHA Testing: Avoid Hasty Abstraction

**Philosophy**: Find the sweet spot between no abstraction and over-abstraction.

**When to Abstract**:

- When repetitive test code obscures the key differences between tests
- When abstraction reveals the actual intent and variations in test scenarios
- When it makes tests clearer and more maintainable

**When NOT to Abstract**:

- Don't abstract on the first instance of similarity
- Avoid complex test utilities that hide important test logic
- Don't create abstractions that make tests harder to understand

**Key Question**: "How easy is it to determine the difference between assertions of two similar tests and what causes that difference?"

### 5. Write Fewer, Longer Tests

**Philosophy**: Structure tests around complete user workflows rather than isolated assertions.

**Benefits of Longer Tests**:

- Better test isolation (no shared mutable state between tests)
- More comprehensive coverage of user scenarios
- Improved readability and maintainability
- Reduced test complexity and setup duplication

**Approach**:

- Think like a manual tester performing a complete workflow
- Use single "Arrange" setup with multiple "Act" and "Assert" steps
- Combine related assertions into cohesive test scenarios
- Don't worry about test length if it reflects real user behavior

**Key Principle**: "Think of a test case workflow for a manual tester and try to make each of your test cases include all parts to that workflow."

**Examples**:
❌ **Multiple short, fragmented tests**:

```javascript
test("shows loading initially", () => {
  render(<UserProfile userId="1" />);
  expect(screen.getByText("Loading...")).toBeInTheDocument();
});

test("calls API with correct userId", () => {
  render(<UserProfile userId="1" />);
  expect(mockFetch).toHaveBeenCalledWith("/api/users/1");
});

test("displays user data when loaded", async () => {
  render(<UserProfile userId="1" />);
  await waitFor(() => {
    expect(screen.getByText("John Doe")).toBeInTheDocument();
  });
});
```

✅ **Comprehensive workflow test**:

```javascript
test("loads and displays user profile", async () => {
  const user = userEvent.setup();

  // Arrange
  mockFetch.mockResolvedValue({ name: "John Doe", email: "john@example.com" });

  // Act & Assert - complete user workflow
  render(<UserProfile userId="1" />);

  // Shows loading state
  expect(screen.getByText("Loading...")).toBeInTheDocument();

  // Makes correct API call
  expect(mockFetch).toHaveBeenCalledWith("/api/users/1");

  // Shows user data when loaded
  await screen.findByText("John Doe");
  expect(screen.getByText("john@example.com")).toBeInTheDocument();

  // User can interact with profile
  await user.click(screen.getByRole("button", { name: "Edit Profile" }));
  expect(screen.getByRole("dialog")).toBeInTheDocument();
});
```

## AHA Testing Examples

❌ **Over-abstracted**:

```javascript
// Complex utility that hides important differences
function testUserFlow(config) {
  // 50 lines of complex setup
  // Hard to see what's actually different between tests
}
```

✅ **Good abstraction**:

```javascript
function setupUser(location = "London") {
  return { id: 1, name: "John", location };
}

test("shows local content for London user", () => {
  const user = setupUser("London");
  // Clear what's being tested - location affects content
});

test("shows local content for Shanghai user", () => {
  const user = setupUser("Shanghai");
  // Easy to see the key difference
});
```

❌ **No abstraction when helpful**:

```javascript
// Repetitive setup obscures the key differences
test('test 1', () => {
  const user = { id: 1, name: 'John', location: 'London', role: 'admin', ... }
  // 10 more lines of setup
})

test('test 2', () => {
  const user = { id: 1, name: 'John', location: 'Shanghai', role: 'admin', ... }
  // Same 10 lines - hard to spot the location difference
})
```

## Test Types Strategy

- **Unit Tests**: Test individual functions and components in isolation
- **Integration Tests**: Test component interactions and data flow
- **E2E Tests**: Test critical user journeys end-to-end

## Writing Effective Tests

### Test Writing Process

1. Identify critical parts of the codebase
2. Narrow down specific units of code
3. Consider who the "users" are (end users, other developers, etc.)
4. Write manual testing instructions
5. Convert those instructions into automated tests

### Test Structure

- Test one behavior at a time
- Use descriptive test names that explain the expected behavior
- Arrange-Act-Assert pattern for clarity
- Keep tests simple and focused
- Make tests readable and maintainable

### Avoid Nesting and Complex Setup

- **Minimize nested `describe` blocks** - they increase cognitive load
- **Avoid excessive `beforeEach` hooks** - can lead to variable reassignment confusion
- **Prefer inline setup** - keep test context clear and immediate
- **Use constants instead of mutable variables** when possible
- **Optimize for change first** - make tests easy to understand and modify

**Examples**:
❌ **Nested and complex**:

```javascript
describe("LoginForm", () => {
  let handleSubmit, user, wrapper;
  beforeEach(() => {
    handleSubmit = vi.fn();
    user = { username: "test", password: "pass" };
  });

  describe("when valid credentials", () => {
    beforeEach(() => {
      // More setup...
    });

    test("should call onSubmit", () => {
      // Hard to track variable state
    });
  });
});
```

✅ **Inline and self-contained**:

```javascript
test('calls onSubmit with valid credentials', () => {
  const handleSubmit = vi.fn()
  const user = { username: 'test', password: 'pass' }

  render(<LoginForm onSubmit={handleSubmit} />)
  // Rest of test - all context is clear and immediate
})

### Recommended Tools
- **React Testing Library**: Provides implementation detail-free and refactor-friendly testing
- **@testing-library/user-event**: For realistic user interactions
- **@testing-library/jest-dom**: For better assertions and error messages (works with Vitest)
- **ESLint plugins**: Use testing-library/recommended and jest-dom/recommended

## React Testing Library Best Practices

### Query Methods (Priority Order)
1. **Prefer `*ByRole`**: Most accessible and user-like queries
2. **Use `*ByLabelText`**: For form controls
3. **Use `*ByText`**: For non-interactive elements with text content
4. **Avoid `container.querySelector()`**: Breaks user-centric testing approach

**Examples**:
- ✅ `screen.getByRole('button', { name: 'Submit' })`
- ✅ `screen.getByLabelText('Username')`
- ✅ `screen.getByText('Welcome')`
- ❌ `container.querySelector('.submit-button')`

### Use `screen` for Queries
- ✅ `screen.getByText('Hello')`
- ❌ `const { getByText } = render(<Component />); getByText('Hello')`

### Async Testing
- **Use `find*` queries** instead of `waitFor` when waiting for elements
- **One assertion per `waitFor`** - don't combine multiple expectations
- **No side effects in `waitFor`** - only use for assertions
- **Don't pass empty callbacks** to `waitFor`

**Examples**:
- ✅ `await screen.findByText('Data loaded')`
- ✅ `await waitFor(() => expect(mockFn).toHaveBeenCalled())`
- ❌ `await waitFor(() => { /* multiple assertions */ })`

### User Interactions
- **Always use `userEvent`** over `fireEvent` for realistic interactions
- **Setup userEvent properly**: `const user = userEvent.setup()`

**Examples**:
- ✅ `await user.click(screen.getByRole('button'))`
- ✅ `await user.type(screen.getByLabelText('Email'), 'test@example.com')`
- ❌ `fireEvent.click(button)`

### Element Existence Checks
- **Use `query*` only for non-existence** checks
- **Use `get*` for elements that should exist**
- **Use `find*` for async elements that should exist**

**Examples**:
- ✅ `expect(screen.queryByText('Error')).not.toBeInTheDocument()`
- ✅ `expect(screen.getByText('Success')).toBeInTheDocument()`
- ❌ `expect(screen.queryByText('Success')).toBeInTheDocument()`

## Red Flags to Avoid

- Tests that break when refactoring without changing behavior
- Tests that require knowledge of implementation to understand
- Mocking everything (reduces confidence in integration)
- Tests that duplicate what other tests already cover
- Nested `describe` blocks that make variable tracking difficult
- Over-abstracted test setup that obscures test intent
- Mutable variables in test setup that get reassigned across hooks
- Copying and slightly modifying previous tests without thoughtful consideration
- Creating complex test utilities that hide the actual test logic
- Abstracting too early before understanding the real patterns
- Breaking complete user workflows into fragmented, isolated tests
- Writing many short tests that share state or require specific execution order
```

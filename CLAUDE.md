# User-Level Development Guidelines

This file organizes my personal development guidelines and best practices that apply across all projects.

## Core Guidelines

@/Users/wesfeller/.claude/guidelines/design-principles.md
@/Users/wesfeller/.claude/guidelines/naming-antipatterns.md
@/Users/wesfeller/.claude/guidelines/pr-creation.md
@/Users/wesfeller/.claude/guidelines/commit-conventions.md
@/Users/wesfeller/.claude/guidelines/pre-commit-checklist.md
@/Users/wesfeller/.claude/guidelines/react-structure.md
@/Users/wesfeller/.claude/guidelines/domain-driven-types.md
@/Users/wesfeller/.claude/guidelines/functional-programming-style.md
@/Users/wesfeller/.claude/guidelines/file-sectioning.md
@/Users/wesfeller/.claude/guidelines/jsx-preferences.md
@/Users/wesfeller/.claude/guidelines/testing-best-practices.md

## Additional Personal Preferences

### Code Style

- Use 2-space indentation for all languages unless project specifies otherwise
- Prefer early returns to reduce nesting
- Extract complex conditions into well-named boolean variables
- Avoid barrel imports (index.ts re-exports) - import directly from source files
- Use specific imports rather than wildcard imports
- Always use `.at()` method instead of bracket notation for JavaScript array access (e.g., `arr.at(0)` instead of `arr[0]`, `arr.at(-1)` instead of `arr[arr.length - 1]`)

### Development Workflow

- Write tests for any non-trivial logic
- Prefer refactoring over comments to make code self-explanatory

### Test-Driven Development (TDD)

- Always follow TDD practices: write tests first, then write the minimal code to make them pass
- Follow the Red-Green-Refactor cycle:
  - Red: Write a failing test that defines the desired behavior
  - Green: Write the simplest code that makes the test pass
  - Refactor: Improve the code while keeping tests green
- Write one test at a time - don't write multiple tests before implementation
- Tests should be specific and test one behavior at a time
- Start with the simplest test case and gradually add complexity
- Ensure tests fail for the right reason before making them pass
- Keep test code clean and maintainable - tests are first-class code

### Documentation

- Only create documentation when explicitly requested
- Keep inline comments minimal - code should be self-documenting
- When documentation is needed, focus on "why" not "what"

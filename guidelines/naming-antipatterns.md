# Naming Anti-Pattern Guidelines

## Method Naming Conventions

### Avoid Confusable Method Names
- Never create methods with similar names in the same class (e.g., `start()` vs `run()`)
- Use distinct, unambiguous names that clearly differentiate functionality
- When methods have different behaviors, their names should be clearly different
- Consider prefixes/suffixes that clarify intent: `startNewThread()` vs `runInCurrentThread()`

### Return Type Consistency
- Methods starting with `get` must always return a value, never void
- Methods starting with `is`, `has`, `can`, `should` must return boolean
- Methods starting with `set` should return void (or self for fluent interfaces)
- Validation methods like `validate()` or `check()` should return boolean or validation results
- Transformation methods must return the transformed value, not void

### Side Effect Clarity
- Pure getter methods (`getSomething()`) must never modify state
- If a method modifies state, use action verbs: `loadAndCache()`, `fetchAndStore()`
- Methods that initialize or configure should be named accordingly: `initializeDatabase()` not `getDatabase()`
- Clearly indicate side effects in method names: `saveAndGetUser()` not just `getUser()`

## Variable and Parameter Naming

### Type-Name Alignment
- Boolean variables/parameters must start with `is`, `has`, `can`, `should`, `will`
- Singular names should represent single items, not collections
- Plural names or names ending in `List`, `Array`, `Set` should represent collections
- Numeric configuration values should indicate expected range in name or documentation

### Avoid Over-Specific Names
- Don't use language-specific names unless truly language-dependent: `text` not `englishText`
- Avoid coupling names to specific frameworks/standards: `privacySettings` not `gdprSettings`
- Use general names for general-purpose functionality: `userIdentifier` not `emailAddress` if it accepts multiple ID types
- Don't embed implementation details in names unless they're part of the contract

## Class and Module Naming

### Framework Independence
- Don't include framework names unless the class is framework-specific
- Bad: `SpringRepeat` for a general-purpose repeat utility
- Good: `RepeatUtil` or `Repeater`

### Clear Contract Communication
- Class names should accurately reflect their responsibilities
- Connection classes should manage connections, not just store credentials
- Builder/Factory classes should actually build/create objects
- Template classes should be clearly named as templates, not as the objects they template

## Code Review Checklist

### When Reviewing Names, Ask:
- Does this name accurately describe what the code does?
- Could this name be confused with something else in the codebase?
- Does the return type match what the name implies?
- Are side effects clearly indicated in the name?
- Is the name more specific than the actual functionality?
- Would a developer using this API be surprised by its behavior?

## Refactoring Priorities

### High Priority Fixes
- Methods that don't return what their names imply (especially security-sensitive ones)
- Boolean-sounding parameters that accept non-boolean values
- Getter methods with side effects
- Similar method names with different behaviors in the same class

### Medium Priority Fixes
- Over-specific names that limit future flexibility
- Names that reference old requirements or frameworks no longer used
- Inconsistent naming patterns within the same module

## Testing Considerations

### Name-Based Testing
- Test that methods return types matching their names
- Verify getters don't modify state
- Ensure boolean methods return boolean values
- Check that similar-named methods have clearly different behaviors

### Documentation Requirements
- Document any naming that might be surprising or counter-intuitive
- Explain why a name doesn't follow conventions if there's a good reason
- Clarify the contract when names might be ambiguous
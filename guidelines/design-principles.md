# Embedded Design Principle (from pathsensitive.com)

## Core Principle

Always code in a way that makes the design apparent. The structure of your code should reflect the conceptual design of your program.

## Key Guidelines

### 1. Represent Design Concepts as First-Class Code Constructs

- If you have a concept in your design (e.g., "dashboard stat"), create an explicit type/class for it
- Don't let design concepts exist only implicitly through repeated code patterns
- Example: Instead of repeating caching logic for each stat, create a `DashboardStat` type that encapsulates the concept

### 2. One Line of Code Per Low-Level Concept

- Each design concept should map to ideally one place in the code
- Avoid having multiple independent "knobs" for what should be a single concept
- This prevents bugs where parts of a concept can be changed independently

### 3. The True DRY Principle

- Don't just avoid repeating code - avoid repeating the expression of concepts
- If you find yourself implementing the same design pattern multiple times, abstract it
- Example: If multiple items share caching behavior, the caching should be implemented once

### 4. Make Design Decisions Explicit

- Wrap conceptual decisions in code structures (even if they're currently no-ops)
- Example: Wrap translatable strings in an i18n function, even if it's just identity for now
- This marks design decisions and makes future changes easier

### 5. Think Beyond Level 2 (What Code Does)

- Level 1: The code itself
- Level 2: What the code does (behavior)
- Level 3: The design - concepts and their relationships
- Good refactoring comes from thinking at Level 3

## Warning Signs of Design Principle Violations

- Multiple places where the same conceptual change would need to be made
- Code that's "indistinguishable from an alternate design"
- Ability to partially modify what should be atomic operations
- Repeated patterns that represent the same concept

## Practical Application

When reviewing or writing code:

1. Identify the concepts in your design
2. Check if each concept is represented explicitly in code
3. Look for repeated patterns that might indicate hidden concepts
4. Consider whether future changes would require modifying multiple places

## Example Transformation

```java
// Bad: Design concepts spread across multiple lines
if (shouldRefresh()) {
    users = countUsers();
    updateCache();
    print("Users: " + users);
}
// ... repeated for each stat

// Good: Design concept as first-class construct
class DashboardStat {
    computation; label;
}
dashboard.getCurrentValues().forEach(stat -> print(stat));
```

## Remember

- "Forms" (higher-level concepts) should be buildable directly in code
- Abstract early rather than late when unsure
- A good structure makes certain bugs impossible

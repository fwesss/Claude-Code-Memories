# Functional Programming Style Guidelines

## Actions, Calculations, and Data Classification
- Distinguish three categories: actions, calculations, and data
- **Actions**: Depend on when/how many times they run; affect or are affected by the world
- **Calculations**: Pure computations from inputs to outputs; no external effects
- **Data**: Immutable facts about events
- **Preference order**: Data > Calculations > Actions
- Calculations are easier to test than actions (same input = same output)

## Extracting Calculations from Actions
- Replace implicit inputs with explicit arguments
- Replace implicit outputs with return values
- Eliminate shared/global variables as implicit inputs/outputs
- Shift code ratio toward calculations and away from actions
- Pull functions apart by single responsibility - they can be recombined

## Immutability Disciplines

### Copy-on-Write (for trusted code)
- Make shallow copy before modifying, then return the copy
- Use for code you control that follows immutability discipline
- More efficient than defensive copying

### Defensive Copying (for untrusted code)
- Make deep copies as data enters/leaves your code
- Protects against code that doesn't follow immutability discipline
- More expensive but provides stronger guarantees

## Stratified Design Principles
- Organize code into layers of abstraction
- Each layer helps ignore different details
- **Layer identification clues**:
  - Function name (intent and grouping)
  - Function body (important details)
  - Call graph structure (implementation complexity)

### Stratified Design Patterns
- **Straightforward Implementation**: Functions implemented clearly at appropriate abstraction level
- **Abstraction Barrier**: Hide implementation details completely
- **Minimal Interface**: Converge on stable, mature interfaces for business concepts
- **Comfort**: Apply abstraction purposefully, avoid over-abstraction

## First-Class Functions and Higher-Order Functions
- Make non-first-class language parts first-class by wrapping in functions
- Use higher-order functions to abstract over varying behavior
- **Code smell**: "Implicit argument in function name" - make it explicit instead
- **Refactoring**: "Replace body with callback" to abstract behavior differences
- Higher-order functions codify patterns and disciplines automatically
- **Trade-off**: Reduce duplication vs. potential readability cost

## Functional Iteration Tools
- **Primary tools**: `map()`, `filter()`, `reduce()`
- Replace specialized for loops with clear, purpose-built operations
- **map()**: Transform array elements one-to-one
- **filter()**: Select subset based on predicate
- **reduce()**: Combine elements into single value

## Chaining and Data Transformation
- Combine functional tools into multi-step chains
- Think of chains as query language (like SQL for arrays)
- Make implicit information explicit as data for subsequent steps
- Look for opportunities to represent concepts as data rather than behavior

## Nested Data Operations
- **update()**: Modify values inside objects functionally
- **nestedUpdate()**: Operate on deeply nested data via key paths
- Use recursion for nested data (clearer than iteration)
- Recursion structure mirrors data structure
- Apply abstraction barriers to complex nested structures

## Timeline and Concurrency Principles
- **Timelines**: Sequences of actions that can run simultaneously
- Multiple timelines create many possible orderings
- Use timeline diagrams to analyze interference
- **Shared resources** are primary source of bugs
- Timelines without shared resources can be understood in isolation

### Concurrency Patterns
- Learn from real-world resource sharing solutions
- Build reusable concurrency primitives
- Use higher-order functions on actions for coordination
- **Cutting timelines**: Coordinate multiple timelines to wait before continuing

## Architecture Patterns

### Reactive Architecture
- Flip from "Do X, do Y" to "When X, then do Y"
- Organize actions/calculations into pipelines
- Use first-class mutable state (like ValueCell) for reactive pipelines

### Onion Architecture
- **Three layers**:
  - **Interaction Layer** (outer): Actions and orchestration
  - **Domain Layer** (middle): Business logic and rules (calculations only)
  - **Language Layer** (inner): Language + utility libraries
- Architecture is fractal - appears at every abstraction level

## TypeScript-Specific Patterns
```typescript
// Sum types with discriminated unions
type Result<T, E> = 
  | { type: 'success'; value: T }
  | { type: 'error'; error: E }

// Function composition helpers
const pipe = <T>(...fns: Array<(x: T) => T>) => (x: T) => 
  fns.reduce((v, f) => f(v), x)

// Curried functions for reusability
const map = <A, B>(f: (a: A) => B) => (xs: A[]): B[] => xs.map(f)
const filter = <A>(p: (a: A) => boolean) => (xs: A[]): A[] => xs.filter(p)
```

## What to Avoid
- Loops - use map, filter, reduce, recursion
- Mutable variables - use const exclusively  
- Classes with mutable state - use factory functions returning immutable objects
- Imperative if/else chains - use pattern matching or function dispatch
- Shared mutable state across timelines
- Deep nesting without abstraction barriers

## Libraries to Consider
- fp-ts or Effect for TypeScript
- Ramda for JavaScript utilities
- Sanctuary for stricter FP in JavaScript
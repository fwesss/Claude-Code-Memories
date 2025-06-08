# Making Bugs Impossible - Design Principles

## Core Principle: Embedded Design

Code should make the design of the program apparent. Represent key design concepts directly in code rather than scattering them across multiple places.

## Key Techniques

### 1. Create Explicit Types for Core Concepts

- Identify the fundamental concepts in your design
- Create classes/types that directly represent these concepts
- Example: Instead of scattered dashboard stat logic, create a `DashboardStat` class

### 2. Consolidate Repeated Logic

- Look for patterns of repeated code
- Extract shared behavior into single, clear implementations
- Centralize caching, computation, and display logic

### 3. Make Design Assumptions Explicit

- Dependencies and relationships should be obvious in the code structure
- Reduce "knobs" - the number of independent configuration points
- Prefer fewer, more intentional configuration options

### 4. Ask the Right Questions

When reviewing or writing code:

- "What are the core concepts in this program?"
- "Does the code structure reflect the design?"
- "Are there scattered pieces of logic that represent a single concept?"

## Practical Application

1. Look beyond immediate functionality
2. Design code to reflect the underlying conceptual structure
3. Consolidate related behaviors into cohesive units
4. Make it hard to introduce inconsistencies by design

## Key Insight

"Finding a good structure for the code was easy once we saw the structure of the design."

The goal is to make certain categories of bugs impossible by ensuring the code structure naturally enforces correct behavior.
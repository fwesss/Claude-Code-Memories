# File Sectioning Guidelines

## Core Principle
Good code makes it easy to recover the intent of the programmer. File organization should support this goal.

## When to Keep Code in One File
- Related functionality that shares control flow
- Code that would be harder to understand if split across files
- When clear section headers can maintain organization
- Early in development when structure is still evolving

## Section Organization
Use clear, visually distinct headers:
```
/************************
 * Section Name
 ************************/
```

Organize sections hierarchically:
- Main sections for major functionality
- Subsections for related groups within main sections
- Keep related code close together

## When to Split Files
Only split when:
- The file structure becomes chaotic despite good sectioning
- Sections are too numerous or complex to navigate easily
- Control flow becomes difficult to track within the file
- Team agrees the cognitive overhead of multiple files is worth it

## Best Practices
- Start with sections in a single file
- Let organization evolve naturally
- Prioritize readability over arbitrary size limits
- Think of files like book chapters - they should tell a coherent story
- Use descriptive section names that explain the "why" not just the "what"
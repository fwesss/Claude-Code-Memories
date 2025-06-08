# Pull Request Creation Guidelines

## PR Titles

### Format
- Keep titles under 80 characters
- Use categorization prefixes followed by a colon and space
- Title should explain the "what" clearly and concisely
- Make titles self-explanatory without needing the description

### Categorization Prefixes
- `feat:` or `feature:` - New features or functionality
- `fix:` - Bug fixes, hot fixes
- `docs:` - Documentation changes
- `chore:` - Maintenance tasks, dependency updates, CI/CD changes
- `breaking:` - Breaking changes that alter core functionality

### Examples
- ✅ `fix: misplaced decimal point miscalculates invoice subtotal`
- ✅ `feat: add axis option to slide transition`
- ✅ `chore(deps): bump alpine from 3.17.3 to 3.18.0`
- ❌ `bug fix for invoice issue` (too vague)
- ❌ `fix issue #1462` (requires context)

## PR Descriptions

### Core Structure
Descriptions should explain the "why" behind changes with these elements:

#### Always Include
- **Context/Justification**: Why the changes were made, implementation decisions, relevant conversations

#### Based on PR Type
- **Features**: Use cases, testing approach, preview (if applicable), documentation, tests
- **Fixes**: Linked issue #, before/after comparison, testing steps, documentation, tests
- **Documentation**: Context, linked issues, use cases, preview
- **Chores**: Context/justification only
- **Breaking Changes**: Context, testing approach, affected projects, mitigation steps, documentation

### Testing Instructions
When applicable, provide clear numbered steps:
1. Navigate to [specific location]
2. Perform [specific action]
3. Verify [expected result]

### Best Practices
- Link issues in description, not title (for future-proofing)
- Use visual aids for UI changes or structural modifications
- Include migration/deprecation steps for breaking changes
- Be thorough but organized - use sections and bullet points
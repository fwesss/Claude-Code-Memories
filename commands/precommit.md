# /precommit

Run through the pre-commit checklist before committing changes.

## Instructions

Please review the following pre-commit checklist items that apply to the current changes:

### Code Quality

- Verify complex algorithms have "why" comments
- Check workarounds include issue tracker links
- Ensure public APIs have proper documentation

### Project Documentation

- Update README if dependencies or setup changed
- Document new environment variables
- Update architecture diagrams if needed
- Add migration notes for breaking changes

### Memory Consistency

- Changes align with project CLAUDE.md patterns
- Code follows established architectural decisions
- Naming matches project domain language
- No conflicts with user preferences (~/.claude/CLAUDE.md)
- Testing approach matches established patterns
- File organization respects project structure

### Type Safety & Testing

- Verify discriminated unions are exhaustive
- Check edge cases are tested
- Ensure error paths have coverage

### Security Review

- No hardcoded secrets or API keys
- User input is validated/sanitized
- Proper authentication on new endpoints
- No SQL injection or XSS vulnerabilities

### Final Checks

- Check for breaking changes
- Review git diff one more time

After reviewing, provide a summary of:

1. ✅ Items that pass
2. ⚠️ Items that need attention
3. ❌ Critical issues to fix

Then ask if the user wants to proceed with the commit.

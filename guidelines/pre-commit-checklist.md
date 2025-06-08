# Pre-Commit Checklist

## Code Comments and Documentation

- Verify all complex algorithms have "why" comments explaining the approach
- Check that any workarounds include comments linking to relevant issue trackers
- Ensure public APIs have JSDoc/docstring comments with examples
- Update inline documentation if behavior changed

## README and Project Documentation

- Update README if adding new dependencies or changing setup steps
- Document any new environment variables in README or .env.example
- Update architecture diagrams if system design changed
- Add migration notes for breaking changes
- Update troubleshooting section if addressing known issues
- Check if project CLAUDE.md needs updating with new development patterns, conventions, or project-specific guidelines

## Memory Consistency and Alignment

- Verify changes align with project-specific patterns documented in project CLAUDE.md
- Check that new code follows established architectural decisions and design principles
- Ensure naming conventions match project memory and domain language
- Validate that changes don't contradict established user preferences or workflow patterns
- Review staged changes against user-level development guidelines (~/.claude/CLAUDE.md)
- Confirm new features follow established testing approaches and framework choices
- Check that changes respect established code organization and file structure patterns

## API and Interface Changes

- Verify backward compatibility or document breaking changes
- Update API documentation for new/modified endpoints
- Check that error responses follow project conventions
- Ensure new API endpoints have rate limiting considerations
- Document any new webhook events or message formats

## Type Definitions and Contracts

- Export new types that other modules might need
- Check that discriminated unions are exhaustive
- Ensure generic types have meaningful names and constraints
- Update shared type definition files if modifying data structures

## Test Coverage Considerations

- Verify edge cases are tested (null, undefined, empty arrays)
- Check error paths have test coverage
- Ensure new public methods have unit tests
- Add integration tests for new API endpoints
- Verify tests cover both success and failure scenarios

## Configuration and Infrastructure

- Document new feature flags and their purpose
- Check that config changes work in all environments
- Verify new dependencies are in correct section (dev vs prod)
- Ensure database migrations are reversible
- Update CI/CD configuration if build process changed

## Breaking Changes and Migration

- Create migration guide for breaking API changes
- Add deprecation warnings to old methods (don't remove yet)
- Update version numbers following semver
- Document data migration steps if schema changed
- Ensure feature flags exist for gradual rollout

## Security and Privacy Review

- Check no secrets or API keys in code (use environment variables)
- Verify user input is validated and sanitized
- Ensure new endpoints have proper authentication/authorization
- Check for SQL injection or XSS vulnerabilities
- Verify PII is handled according to privacy policy
- Review dependencies for known vulnerabilities

# Commit Message Conventions

Follow the Conventional Commits 1.0.0 specification for all commit messages.

## Format

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

## Types

- **feat**: A new feature (correlates with MINOR in SemVer)
- **fix**: A bug fix (correlates with PATCH in SemVer)
- **docs**: Documentation only changes
- **style**: Changes that do not affect the meaning of the code (white-space, formatting, etc)
- **refactor**: A code change that neither fixes a bug nor adds a feature
- **perf**: A code change that improves performance
- **test**: Adding missing tests or correcting existing tests
- **build**: Changes that affect the build system or external dependencies
- **ci**: Changes to CI configuration files and scripts
- **chore**: Other changes that don't modify src or test files
- **revert**: Reverts a previous commit

## Breaking Changes

- Add `!` after type/scope: `feat!: send email when product is shipped`
- OR include `BREAKING CHANGE:` in footer
- Breaking changes correlate with MAJOR in SemVer

## Scope

Optional, provides additional context:
- `feat(parser): add ability to parse arrays`
- `fix(api): handle empty responses`

## Examples

### Simple fix
```
fix: prevent racing of requests
```

### Feature with scope
```
feat(lang): add Polish language
```

### Breaking change
```
feat!: send email to customer when product is shipped

BREAKING CHANGE: email notifications are now sent by default
```

### Multi-paragraph with footer
```
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.

Reviewed-by: Z
Refs: #123
```

## Key Guidelines

- Use imperative mood in description ("add" not "added" or "adds")
- Don't capitalize first letter of description
- No period at the end of description
- Keep first line under 72 characters
- Body should explain what and why, not how
- Reference issues and PRs in footer when applicable
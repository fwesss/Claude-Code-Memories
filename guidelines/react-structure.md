# React Application Structure Guidelines

## Import Philosophy

**No Barrel Imports**: This project avoids index.ts/index.js barrel files that re-export modules. Benefits:
- Improved tree-shaking and smaller bundle sizes
- Better IDE performance and import suggestions
- Clearer dependency tracking
- Faster build times

Always import directly from the source file where the export is defined.

## Directory Structure Evolution

Follow this progressive approach based on application size:

### 1. Small Applications (< 10 components)
- Keep components in a single `components/` folder
- Use kebab-case for all file names (e.g., `user-profile.js`, not `UserProfile.js`)

### 2. Medium Applications (10-50 components)
```
src/
├── components/     # Reusable UI components
├── hooks/         # Shared custom hooks  
├── context/       # React Context providers
└── services/      # API calls, utilities, formatters
```

### 3. Large Applications (50+ components)
```
src/
├── features/      # Feature-based organization
│   ├── user/
│   ├── dashboard/
│   └── settings/
├── components/    # Only truly reusable UI components
├── hooks/        # Only globally shared hooks
├── context/      # Only global context
└── services/     # Only global services
```

## Component Folder Structure

When a component grows beyond a single file, structure it as:
```
component-name/
├── component-name.tsx  # Component implementation (main file)
├── component-name.test.tsx   # Tests
├── component-name.module.css    # Styles
├── types.ts        # TypeScript definitions
├── hooks.ts        # Component-specific hooks
└── utils.ts        # Component-specific utilities
```

**Note**: Avoid creating index.ts barrel files. Import directly from the specific file.

## Key Principles

### File Naming
- **Always use kebab-case** for file names: `user-profile.js`, `use-auth.js`
- Component files should match their export name in kebab-case
- Test files: `component-name.test.js`
- Style files: `component-name.module.css` or `styles.css`

### Organization Rules
- **Start simple**: Begin with files, evolve to folders only when needed
- **Co-location**: Keep related code together (component + its hooks/utils/styles)
- **Maximum nesting**: Limit to 2 levels deep to maintain simplicity
- **No barrel exports**: Avoid index.ts files; import directly from source files for better tree-shaking

### When to Extract
- Extract to shared folders only when code is used by 2+ components
- Component-specific code stays with the component
- Move from technical to feature organization when folders get too large (10+ items)

### Import Patterns
```javascript
// Good - import directly from the source file
import { UserProfile } from './components/user-profile/user-profile';
import { useAuth } from './hooks/use-auth';
import { formatDate } from './services/formatters/date-formatter';

// Avoid - using barrel exports (index files)
import { UserProfile } from './components/user-profile';
import { useAuth, useApi, useLocalStorage } from './hooks';
```

## Common Patterns

### Custom Hooks Organization
```
hooks/
├── use-auth.js
├── use-api.js
└── use-local-storage.js
```

### Context Organization
```
context/
├── auth-context.js
├── theme-context.js
└── app-context.js
```

### Service Layer Organization
```
services/
├── api/
│   ├── user-api.js
│   └── post-api.js
├── formatters/
│   ├── date-formatter.js
│   └── currency-formatter.js
└── validators/
    └── form-validators.js
```

## Anti-patterns to Avoid
- Don't use PascalCase for file names
- Don't create deeply nested structures (> 2 levels)
- Don't separate by file type at the root level (e.g., `/styles`, `/tests`)
- Don't create folders for single files
- Don't mix feature and technical organization at the same level
- Don't create index.ts/index.js barrel files for re-exporting modules
- Don't use wildcard exports (`export * from './module'`)
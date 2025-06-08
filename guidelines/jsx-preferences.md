# JSX Code Style Preferences

## Key Principles
- Keep JSX clean and readable by minimizing inline logic
- Extract calculations and expressions from JSX templates
- Define callbacks outside of JSX props

## Guidelines

### Callbacks
- Define callbacks in the component body or as separate functions
- Never define callbacks inline in props

```tsx
// ❌ Bad
<button onClick={() => handleClick(item.id)}>Click</button>

// ✅ Good
const handleItemClick = () => handleClick(item.id);
// ...
<button onClick={handleItemClick}>Click</button>
```

### Conditional Rendering
- Avoid nested ternaries in JSX
- Extract complex conditions to variables or early returns

```tsx
// ❌ Bad
<div>{isLoading ? <Spinner /> : hasError ? <Error /> : <Content />}</div>

// ✅ Good
const renderContent = () => {
  if (isLoading) return <Spinner />;
  if (hasError) return <Error />;
  return <Content />;
};
// ...
<div>{renderContent()}</div>
```

### Expressions
- Extract calculations and expressions to variables
- Keep JSX focused on structure, not logic

```tsx
// ❌ Bad
<div className={`px-4 ${isActive ? 'bg-blue-500' : 'bg-gray-200'} ${size === 'large' ? 'py-3' : 'py-2'}`}>

// ✅ Good
const buttonClasses = cn(
  'px-4',
  isActive ? 'bg-blue-500' : 'bg-gray-200',
  size === 'large' ? 'py-3' : 'py-2'
);
// ...
<div className={buttonClasses}>
```

### Component Props
- Prepare props objects when multiple props depend on conditions
- Avoid spreading complex expressions

```tsx
// ❌ Bad
<Component
  {...(isEnabled && { onClick: handleClick, disabled: false })}
  className={`base ${isActive && 'active'}`}
/>

// ✅ Good
const componentProps = isEnabled
  ? { onClick: handleClick, disabled: false }
  : { disabled: true };
const className = cn('base', isActive && 'active');
// ...
<Component {...componentProps} className={className} />
```
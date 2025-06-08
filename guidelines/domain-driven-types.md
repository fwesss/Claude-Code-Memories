# Domain-Driven Design and Type Usage

## Avoid Primitive Obsession
- Never use primitive types directly for domain concepts
- Always create named types and interfaces that represent domain entities
- Primitive types (string, number, boolean) should only be used as building blocks within domain types

## Examples of Good Type Usage

### Instead of primitives:
```typescript
// ❌ Bad - primitive obsession
function processOrder(orderId: string, customerId: string, amount: number) {}

// ✅ Good - domain types
interface OrderId { value: string }
interface CustomerId { value: string }
interface Money { amount: number; currency: string }
function processOrder(orderId: OrderId, customerId: CustomerId, total: Money) {}
```

### Create meaningful domain types:
```typescript
// ❌ Bad
type User = {
  email: string;
  age: number;
  verified: boolean;
}

// ✅ Good
type EmailAddress = { value: string }
type Age = { years: number }
type VerificationStatus = 'pending' | 'verified' | 'rejected'

type User = {
  email: EmailAddress;
  age: Age;
  verificationStatus: VerificationStatus;
}
```

## Benefits
- Self-documenting code through type names
- Type safety prevents mixing up similar primitives
- Easy to add validation and business rules to domain types
- Better IDE support and refactoring capabilities
- Clear domain boundaries and concepts
---
name: error_handling
description: Master error handling patterns across languages including exceptions, Result types, error propagation, and graceful degradation. Use when implementing error handling, designing APIs, debugging issues, or improving application reliability.
---

# Error Handling Patterns

Build resilient applications with robust error handling strategies that gracefully handle failures and provide excellent debugging experiences.

## When to Use This Skill

- Implementing error handling in new features
- Designing error-resilient APIs
- Debugging production issues
- Improving application reliability
- Creating better error messages for users and developers
- Implementing retry and circuit breaker patterns
- Handling async/concurrent errors
- Building fault-tolerant distributed systems

## Core Concepts

### Error Handling Philosophies

**Exceptions vs Result Types:**

- **Exceptions**: Traditional try-catch, disrupts control flow
  - Use for: Unexpected errors, exceptional conditions
- **Result Types**: Explicit success/failure, functional approach
  - Use for: Expected errors, validation failures
- **Panics/Crashes**: Unrecoverable errors, programming bugs

### Error Categories

**Recoverable Errors:**

- Network timeouts
- Missing files
- Invalid user input
- API rate limits

**Unrecoverable Errors:**

- Out of memory
- Stack overflow
- Programming bugs (null pointer, etc.)

## Quick Reference

### Pattern 1: Custom Exception Hierarchy

Create a base exception class with context information:

```python
class ApplicationError(Exception):
    """Base exception for all application errors."""
    def __init__(self, message: str, code: str = None, details: dict = None):
        super().__init__(message)
        self.code = code
        self.details = details or {}
        self.timestamp = datetime.utcnow()

class ValidationError(ApplicationError):
    """Raised when validation fails."""
    pass

class NotFoundError(ApplicationError):
    """Raised when resource not found."""
    pass
```

### Pattern 2: Result Type Pattern

Explicit success/failure without exceptions:

```typescript
type Result<T, E = Error> = { ok: true; value: T } | { ok: false; error: E };

function Ok<T>(value: T): Result<T, never> {
  return { ok: true, value };
}

function Err<E>(error: E): Result<never, E> {
  return { ok: false, error };
}

// Usage
const result = parseJSON<User>(userJson);
if (result.ok) {
  console.log(result.value.name);
} else {
  console.error("Parse failed:", result.error.message);
}
```

### Pattern 3: Retry with Exponential Backoff

```python
def retry(max_attempts: int = 3, backoff_factor: float = 2.0):
    """Retry decorator with exponential backoff."""
    def decorator(func):
        def wrapper(*args, **kwargs):
            for attempt in range(max_attempts):
                try:
                    return func(*args, **kwargs)
                except Exception as e:
                    if attempt < max_attempts - 1:
                        time.sleep(backoff_factor ** attempt)
                        continue
                    raise
        return wrapper
    return decorator
```

### Pattern 4: Circuit Breaker

Prevent cascading failures in distributed systems:

```python
class CircuitBreaker:
    """
    States: CLOSED (normal) → OPEN (failing) → HALF_OPEN (testing)
    """
    def __init__(self, failure_threshold=5, timeout=60, success_threshold=2):
        self.failure_threshold = failure_threshold
        self.timeout = timeout
        self.success_threshold = success_threshold
        self.state = CircuitState.CLOSED

    def call(self, func):
        if self.state == CircuitState.OPEN:
            if self._should_attempt_reset():
                self.state = CircuitState.HALF_OPEN
            else:
                raise Exception("Circuit breaker is OPEN")

        try:
            result = func()
            self.on_success()
            return result
        except Exception:
            self.on_failure()
            raise
```

### Pattern 5: Graceful Degradation

Provide fallback functionality when errors occur:

```python
def with_fallback(primary, fallback, log_error=True):
    """Try primary function, fall back to fallback on error."""
    try:
        return primary()
    except Exception as e:
        if log_error:
            logger.error(f"Primary function failed: {e}")
        return fallback()

# Usage: Try cache, fall back to database
user = with_fallback(
    primary=lambda: fetch_from_cache(user_id),
    fallback=lambda: fetch_from_database(user_id)
)
```

### Pattern 6: Error Aggregation

Collect multiple errors instead of failing on first error:

```typescript
class ErrorCollector {
  private errors: Error[] = [];

  add(error: Error): void {
    this.errors.push(error);
  }

  hasErrors(): boolean {
    return this.errors.length > 0;
  }

  throw(): never {
    if (this.errors.length === 1) throw this.errors[0];
    throw new AggregateError(
      this.errors,
      `${this.errors.length} errors occurred`,
    );
  }
}

// Usage: Validate all fields before throwing
function validateUser(data: any): User {
  const errors = new ErrorCollector();

  if (!data.email) errors.add(new ValidationError("Email required"));
  if (!data.name) errors.add(new ValidationError("Name required"));
  if (data.age < 18) errors.add(new ValidationError("Must be 18+"));

  if (errors.hasErrors()) errors.throw();
  return data as User;
}
```

## Best Practices

1. **Fail Fast** - Validate input early, fail quickly
2. **Preserve Context** - Include stack traces, metadata, timestamps
3. **Meaningful Messages** - Explain what happened and how to fix it
4. **Log Appropriately** - Error = log, expected failure = don't spam logs
5. **Handle at Right Level** - Catch where you can meaningfully handle
6. **Clean Up Resources** - Use try-finally, context managers, defer
7. **Don't Swallow Errors** - Log or re-throw, don't silently ignore
8. **Type-Safe Errors** - Use typed errors when possible

### Good Error Handling Example

```python
def process_order(order_id: str) -> Order:
    """Process order with comprehensive error handling."""
    try:
        # Validate input early
        if not order_id:
            raise ValidationError("Order ID is required")

        # Fetch order
        order = db.get_order(order_id)
        if not order:
            raise NotFoundError("Order", order_id)

        # Process payment with specific error handling
        try:
            payment_result = payment_service.charge(order.total)
        except PaymentServiceError as e:
            logger.error(f"Payment failed for order {order_id}: {e}")
            raise ExternalServiceError(
                "Payment processing failed",
                service="payment_service",
                details={"order_id": order_id, "amount": order.total}
            ) from e

        # Update order
        order.status = "completed"
        order.payment_id = payment_result.id
        db.save(order)

        return order

    except ApplicationError:
        raise  # Re-raise known errors
    except Exception as e:
        logger.exception(f"Unexpected error processing order {order_id}")
        raise ApplicationError("Order processing failed", code="INTERNAL_ERROR") from e
```

## Common Pitfalls

❌ **Catching Too Broadly** - `except Exception` hides bugs
❌ **Empty Catch Blocks** - Silently swallowing errors
❌ **Logging and Re-throwing** - Creates duplicate log entries
❌ **Not Cleaning Up** - Forgetting to close files, connections
❌ **Poor Error Messages** - "Error occurred" is not helpful
❌ **Returning Error Codes** - Use exceptions or Result types
❌ **Ignoring Async Errors** - Unhandled promise rejections

## Language-Specific Details

For detailed language-specific patterns and examples, see:

- **[reference.md](reference.md)** - Comprehensive language-specific examples
  - Python: Custom exceptions, context managers, retry decorators
  - TypeScript/JavaScript: Custom errors, Result types, async handling
  - Rust: Result and Option types, error propagation
  - Go: Explicit error returns, error wrapping
  - Detailed circuit breaker implementation
  - Advanced error aggregation patterns
  - Multiple fallback strategies

## Anti-Patterns to Avoid

```python
# ❌ Bad: Swallowing errors
try:
    risky_operation()
except:
    pass  # Silent failure!

# ✅ Good: Log and handle appropriately
try:
    risky_operation()
except SpecificError as e:
    logger.error(f"Operation failed: {e}")
    return fallback_value()
```

```typescript
// ❌ Bad: Vague error message
throw new Error("Error");

// ✅ Good: Descriptive error with context
throw new ValidationError("Email validation failed: invalid format", {
  email: userInput,
  pattern: EMAIL_REGEX,
});
```

## Quick Decision Tree

```
Error occurred?
├─ Expected error (validation, not found)?
│  └─ Use Result type or custom exception
├─ External service failure?
│  ├─ Transient? → Retry with backoff
│  └─ Persistent? → Circuit breaker + fallback
├─ Programming bug?
│  └─ Panic/crash with detailed context
└─ Resource cleanup needed?
   └─ Use try-finally or context manager
```

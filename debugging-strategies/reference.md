# Debugging Strategies Reference

Detailed documentation for language-specific tools, advanced techniques, and common error patterns.

## Debugging Tools by Language

### JavaScript/TypeScript

```typescript
// Chrome DevTools Debugger
function processOrder(order: Order) {
  debugger; // Execution pauses here

  const total = calculateTotal(order);
  console.log("Total:", total);

  // Conditional breakpoint
  if (order.items.length > 10) {
    debugger; // Only breaks if condition true
  }

  return total;
}

// Console debugging techniques
console.log("Value:", value); // Basic
console.table(arrayOfObjects); // Table format
console.time("operation");
/* code */ console.timeEnd("operation"); // Timing
console.trace(); // Stack trace
console.assert(value > 0, "Value must be positive"); // Assertion

// Performance profiling
performance.mark("start-operation");
// ... operation code
performance.mark("end-operation");
performance.measure("operation", "start-operation", "end-operation");
console.log(performance.getEntriesByType("measure"));
```

**VS Code Debugger Configuration (`.vscode/launch.json`):**

```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "Debug Program",
      "program": "${workspaceFolder}/src/index.ts",
      "preLaunchTask": "tsc: build - tsconfig.json",
      "outFiles": ["${workspaceFolder}/dist/**/*.js"],
      "skipFiles": ["<node_internals>/**"]
    },
    {
      "type": "node",
      "request": "launch",
      "name": "Debug Tests",
      "program": "${workspaceFolder}/node_modules/jest/bin/jest",
      "args": ["--runInBand", "--no-cache"],
      "console": "integratedTerminal"
    }
  ]
}
```

### Python

```python
# Built-in debugger (pdb)
import pdb

def calculate_total(items):
    total = 0
    pdb.set_trace()  # Debugger starts here

    for item in items:
        total += item.price * item.quantity

    return total

# Breakpoint (Python 3.7+)
def process_order(order):
    breakpoint()  # More convenient than pdb.set_trace()

# Post-mortem debugging
try:
    risky_operation()
except Exception:
    import pdb
    pdb.post_mortem()  # Debug at exception point

# IPython debugging (ipdb)
from ipdb import set_trace
set_trace()  # Better interface than pdb

# Logging for debugging
import logging
logging.basicConfig(level=logging.DEBUG)
logger = logging.getLogger(__name__)

# Profile performance
import cProfile
import pstats

cProfile.run('slow_function()', 'profile_stats')
stats = pstats.Stats('profile_stats')
stats.sort_stats('cumulative')
stats.print_stats(10)
```

### Go

```go
// Delve debugger
// Install: go install github.com/go-delve/delve/cmd/dlv@latest
// Run: dlv debug main.go

import (
    "fmt"
    "runtime"
    "runtime/debug"
)

// Print stack trace
func debugStack() {
    debug.PrintStack()
}

// Panic recovery with debugging
func processRequest() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Panic:", r)
            debug.PrintStack()
        }
    }()
}

// Memory profiling
import _ "net/http/pprof"
// Visit http://localhost:6060/debug/pprof/

// CPU profiling
import (
    "os"
    "runtime/pprof"
)

f, _ := os.Create("cpu.prof")
pprof.StartCPUProfile(f)
defer pprof.StopCPUProfile()
```

## Advanced Debugging Techniques

### Technique 1: Binary Search Debugging

**Git bisect** is essential for finding when a bug was introduced:

```bash
git bisect start
git bisect bad                    # Current commit is bad
git bisect good v1.0.0            # v1.0.0 was good

# Test checked-out commit, then:
git bisect good   # if it works
git bisect bad    # if it's broken

git bisect reset  # when done
```

### Technique 2: Differential Debugging

Compare working vs broken states systematically:

| Aspect       | Working     | Broken       |
| ------------ | ----------- | ------------ |
| Environment  | Development | Production   |
| Node version | 18.16.0     | 18.15.0      |
| Data         | Empty DB    | 1M records   |
| User         | Admin       | Regular user |

### Technique 3: Trace Debugging

```typescript
function trace(
  target: any,
  propertyKey: string,
  descriptor: PropertyDescriptor,
) {
  const originalMethod = descriptor.value;
  descriptor.value = function (...args: any[]) {
    console.log(`Calling ${propertyKey} with args:`, args);
    const result = originalMethod.apply(this, args);
    console.log(`${propertyKey} returned:`, result);
    return result;
  };
  return descriptor;
}
```

### Technique 4: Memory Leak Detection

- **Heap Snapshots**: Compare snapshots in Chrome DevTools or Node.js.
- **Node.js Leak Detection**: `require("v8").writeHeapSnapshot()` when memory usage spikes.

## Debugging Patterns by Issue Type

### Pattern 1: Intermittent Bugs (Race Conditions)

1. **Extensive timing-based logging**.
2. **Stress testing** (run many times).
3. **Simulate network latency** to provoke race conditions.

### Pattern 2: Performance Bottlenecks

1. **Profile first**: Use `cProfile`, `Chrome Performance`, or `clinic.js`.
2. **Identify culprits**: N+1 queries, synchronous I/O, heavy re-renders.

### Pattern 3: Production Investigating

1. **Gather evidence**: Use Sentry/Bugsnag, logs, and user reports.
2. **Shadow traffic**: Use feature flags to log behavior for specific users safely.

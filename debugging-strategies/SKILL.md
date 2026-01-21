---
name: debugging-strategies
description: Master systematic debugging techniques, profiling tools, and root cause analysis to efficiently track down bugs across any codebase. Use when investigating bugs, performance issues, or unexpected behavior.
---

# Debugging Strategies

Transform debugging from frustrating guesswork into systematic problem-solving with methodical approaches.

## When to Use This Skill

- Tracking down elusive bugs or race conditions
- Investigating performance issues or memory leaks
- Analyzing crash dumps and stack traces in production
- Understanding complex, unfamiliar codebases
- Systematic root cause analysis

## Core Principles

### 1. The Scientific Method

1. **Observe**: Note the actual vs. expected behavior.
2. **Hypothesize**: Propose potential causes based on data.
3. **Experiment**: Test your hypothesis (e.g., change one variable).
4. **Analyze**: Did the results support your theory?
5. **Repeat**: Iterate until the root cause is found.

### 2. Debugging Mindset

- **Question assumptions**: Even if "nothing changed," check anyway.
- **Reproduce consistently**: If you can't repeat it, you can't verify the fix.
- **Isolate**: Remove unrelated code until you have a minimal failing case.
- **Rubber Duck**: Explaining the logic to another (or an AI) often reveals the flaw.

## Systematic Debugging Process

### Phase 1: Reproduce & Isolate

- **Consistent repro?** Find the exact steps or data required.
- **Minimal repro**: Stripe away complexity until only the bug remains.

### Phase 2: Information Gathering

- **Stack traces**: Read from top to bottom (or bottom to top for root entry).
- **Recent history**: Check `git blame` or deployment timelines.
- **Environment**: Diff dev/staging/prod configurations.

### Phase 3: Binary Search Execution

Narrow down the search area effectively:

- **Git Bisect**: Find the exact commit that broke the build.
- **Comment-out logic**: Disable halves of the suspicious code to find the faulty block.

### Phase 4: Verification

- **Test the fix**: Prove the repro steps no longer fail.
- **Regression testing**: Ensure the fix didn't break related functionality.

## Best Practices

1. **Reproduce First**: Never attempt a fix without a clear reproduction.
2. **One Change at a Time**: Don't mix fixes or changes; you'll lose track of what worked.
3. **Read the Full Error**: Don't just scan; often the cause is in the second or third line of a trace.
4. **Fix the Root, Not Symptoms**: If a value is null, find _why_ it's null, don't just add a null check.
5. **Take Breaks**: Debugging fatigue is real; fresh eyes find bugs faster.

## Quick Reference Checklist

- [ ] **Typos**: Variable names, file paths, case sensitivity.
- [ ] **State**: Is the data what you _think_ it is? (Verify with logging/debugger).
- [ ] **Async**: Are you missing an `await` or handling a race condition?
- [ ] **Environment**: Are env vars set correctly? Are dependencies up to date?
- [ ] **Cache**: Have you cleared local storage, browser cache, or build artifacts?

## Technical References

For detailed language-specific tools and advanced techniques, see:

- **[reference.md](reference.md)**: Includes:
  - **Tooling**: JS/TS (Chrome DevTools, VS Code), Python (pdb, cProfile), Go (delve, pprof).
  - **Advanced Techniques**: Git bisect, differential debugging, memory leak detection.
  - **Issue Patterns**: Intermittent bugs, performance profiling, production triage.

## Common Pitfalls

❌ **Assuming the framework is broken**: Usually, it's your code.
❌ **Ignoring warnings**: Warnings often hint at the eventual crash points.
❌ **Sticking to one tool**: Don't rely solely on `console.log`; learn the interactive debugger.
❌ **Fixing by guessing**: Randomly changing code until it "works" leaves hidden debt.

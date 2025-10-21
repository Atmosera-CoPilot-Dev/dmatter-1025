# Copilot Instructions
Coding instructions for this TypeScript + Jest repository

## TypeScript Source Files
Pattern: **/*.ts

### Runtime / Tooling
- Target Node.js LTS (>=18)
- TypeScript >=5.8 (strict mode assumed)
- Prefer modern TS features (satisfies, const type params, template literal types)
- Use ES module syntax; avoid CommonJS unless required

### General Guidelines
- Add a brief header comment per file describing purpose
- Export only intentional public API; keep internals file‑local
- Provide JSDoc for all exported symbols (functions, classes, interfaces, types)
- No implicit any; avoid broad unknown without refinement
- Prefer const; avoid var
- Use readonly (types / properties) and as const for immutable literals
- Favor discriminated unions over enums when flexible
- Avoid magic strings/numbers; centralize constants
- No dead or commented‑out code
- Avoid @ts-ignore / @ts-expect-error unless justified with a trailing comment

### Style
- camelCase for variables/functions; PascalCase for types/classes
- Keep functions small and single responsibility
- Prefer pure functions; isolate side effects
- Use template literals over string concatenation
- Narrow types early using type guards

### Error Handling
- Throw Error or custom subclasses with clear messages
- Wrap fallible async/IO in try/catch; add contextual message when rethrowing
- Do not swallow errors silently
- Use exhaustive checks (e.g., never in switch on discriminated union)

### Logging
- Minimal console usage in library code; prefer a central logger if needed
- Include actionable context in error logs

### Performance
- Avoid unnecessary cloning/spreading
- Short‑circuit on invalid input early
- Prefer clear code over premature micro‑optimizations

### Testing (Jest)
- Test file pattern: tests/**/*.test.ts
- Use describe blocks for grouping; clear behavior‑focused names
- Reset mocks/state between tests (jest.clearAllMocks or afterEach)
- Prefer toBe / toEqual / toStrictEqual appropriately
- Test error paths (expect(() => fn()).toThrow / await rejects)
- Use jest.spyOn / manual mocks for side effects
- Aim ≥80% coverage (branches/statements)
- Run: npm test
- Avoid flaky tests (no unmocked timers/network)

Sample:
```ts
describe('FeatureX', () => {
  beforeEach(() => {
    jest.clearAllMocks();
  });
  it('returns transformed value', () => {
    // Arrange / Act
    // Assert
  });
});

```

### Module Boundaries
- Expose public surface via src/index.ts
- Avoid deep relative imports from outside src; re-export as needed

### Dependencies
- Keep runtime deps minimal; prefer devDependencies for tooling
- Avoid large libs for trivial utilities
- Prefer built‑in Node APIs when sufficient

### Documentation
- Update README.md on public API changes
- JSDoc: describe params, return type, thrown errors, side effects

### SQL Files (if present)
**/*.sql
- SQLite syntax
- Uppercase keywords
- Comment complex queries
- Explicit JOIN syntax
- Qualify all column references with table names

### Commit Message Guidelines
- Subject ≤50 chars, imperative mood
- Blank line after subject
- Body (if needed) wrapped ~72 chars, explains rationale
- Be specific (e.g., "Add input validation to parser")
- Avoid vague subjects (e.g., "Update code")

Examples:
Good: Add discriminated union for request states
Bad: Update stuff

### Review Checklist
- Types explicit and narrow
- No unused exports
- Tests cover new/changed logic (incl. error paths)
- Clear error messages
- No unjustified @ts-ignore
- Documentation updated
- Commit message follows guidelines

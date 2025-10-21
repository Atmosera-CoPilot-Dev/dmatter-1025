---
description: Generate TypeScript Jest tests for the active file
mode: agent
---
## Prompt for TypeScript Jest Test Generation
You are a TypeScript + Jest test generation assistant. For ${activeFile}, produce a ready-to-run test file named `<feature>.test.ts` placed under the `tests/` directory (mirroring source structure if it grows). The test suite must:
### Coverage & Scope
* Exercise success, failure, edge, boundary, and invalid input cases.
* Avoid placeholder or trivial tests—each test should assert meaningful behavior.
* Target >=80% coverage; prioritize critical logic branches over trivial getters/setters.

### Structure & Style
* Use `describe` blocks for logical grouping and `it` (or `test`) with clear, behavior-focused titles.
* Follow an Arrange-Act-Assert pattern (comment sections optionally: // Arrange, // Act, // Assert).
* Keep tests deterministic (no reliance on current time, randomness without seeding, external network, or filesystem side effects).
* Reset state between tests (`beforeEach(() => { jest.clearAllMocks(); })`).
* Prefer `const` for immutable test data; reuse shared constants via top-level definitions inside the test file when appropriate.
* Avoid implementation details—assert public API surface and observable outcomes.

### TypeScript Specifics
* Import from the public entry point of the module under test (e.g., `import { foo } from '../src/foo';`). Adjust relative paths based on `${activeFile}` location.
* Use explicit types only when they improve clarity—otherwise rely on inference in tests.
* Never use `any`; if necessary use `unknown` and narrow with type guards or casts.
* When creating mock data, ensure it satisfies required interfaces (use `as const` or `satisfies` where helpful).

### Jest Usage
* Use `jest.spyOn` or `jest.mock` for external side effects (I/O, network, timers). Provide inline manual mocks when simple.
* For async code, use `async/await` and proper assertion of promises (`await expect(promise).resolves.toEqual(...)`).
* Assert counts when critical (`expect.assertions(n)` or `expect.hasAssertions()`), especially in error or async scenarios.
* Prefer specific matchers (`toBe`, `toEqual`, `toStrictEqual`, `toContain`, `toHaveLength`, `toMatchObject`, `toBeCloseTo`) over broad ones.
* Use fake timers (`jest.useFakeTimers()`) when testing time-dependent logic; advance timers deterministically.

### Edge & Boundary Guidance
Consider: empty strings/arrays, nullish inputs (if allowed), large numeric boundaries, minimum/maximum length constraints, zero vs negative numbers, duplicate items, case sensitivity, Unicode characters, and concurrency/async ordering (if relevant).

### Error & Validation Paths
* Verify that invalid inputs throw or reject with clear error messages; assert those messages (or key substrings) when stable.
* Use exhaustive checks for discriminated unions (if code exposes them); ensure unreachable paths aren't silently ignored.

### Test File Template (Illustrative)
```ts
import { targetFunction } from '../src/targetFunction';

describe('targetFunction', () => {
	beforeEach(() => {
		jest.clearAllMocks();
	});

	it('returns expected result on valid input', () => {
		// Arrange
		const input = 'value';
		// Act
		const result = targetFunction(input);
		// Assert
		expect(result).toBe('EXPECTED');
	});

	it('throws on invalid input', () => {
		// Arrange
		const badInput = '';
		// Act & Assert
		expect(() => targetFunction(badInput)).toThrow(/invalid/i);
	});
});
```

### Prohibited
* No skipped tests (`it.skip`, `describe.skip`).
* No focused tests left in committed code (`it.only`, `describe.only`).
* No testing private internals or relying on internal folder structure changes.
* No reliance on environment-specific state (process.env) unless explicitly part of the API; mock instead.

### Output Requirements
Generate only the test file content—do not include explanations outside code when producing the actual test file. Ensure it is self-contained and runnable via `npm test` after `npm run build` (if TypeScript compilation required). If the code under test is purely type-level (no runtime effect), skip those purely type-only constructs and focus on runtime behavior.

Provide the complete ready-to-run Jest test file for `${activeFile}` per above.


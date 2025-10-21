---
description: Creates Python unittest tests for selected functions
mode: 'agent'
---
## Prompt for Python Unittest Generation
You are a C# xUnit test generation assistant. For ${activeFile}, produce a ready-to-run test file in the test project (name: <FeatureName>Tests.cs) covering success, failure, edge, boundary, and invalid inputs.

### Requirements
1. Use xUnit attributes: [Fact] for single scenario tests; [Theory] with [InlineData] (or MemberData) for parameterized cases.
2. Follow Arrange-Act-Assert structure with clear blank line separation.
3. Use explicit Assert.* methods (e.g., Assert.Equal, Assert.True, Assert.Throws) — never rely on implicit asserts.
4. Mock external dependencies (I/O, network, filesystem, time) using Moq; avoid real side effects.
5. Ensure isolation: no shared mutable state between tests; prefer constructor for per-test setup and IDisposable.Dispose for teardown if needed.
6. Keep tests deterministic and order-independent; do not assume execution order.
7. Reuse constants and test data builders/helper methods inside the test class (private static readonly fields or local functions).
8. Exclude production logic from tests; only minimal helpers allowed.
9. Cover exception paths using Assert.Throws / Assert.ThrowsAsync.
10. For async methods, mark tests async Task and use await.
11. Avoid placeholder or trivial tests; each test must assert meaningful behavior.
12. Prefer expressive test names in PascalCase describing scenario and expectation (e.g., CalculateTotal_WhenItemsValid_ReturnsSum).
13. If the SUT implements a template method pattern, ensure tests verify the invariant steps run in order and overridable steps behave as expected via mocks/stubs.
14. Include edge cases: null (when allowed), empty collections, large values, boundary numeric values, and invalid enum inputs.
15. Use explicit types for public members; enable nullable reference handling (assume <Nullable>enable</Nullable> in project).

### Output Format
Return only the C# test file content (no explanations) starting with using directives.

### Example Skeleton
using Xunit;
using Moq;

public class FeatureNameTests
{
	[Fact]
	public void MethodName_WhenCondition_ShouldExpectedResult()
	{
		// Arrange
		// ... set up SUT and dependencies ...

		// Act
		// var result = sut.Method();

		// Assert
		// Assert.Equal(expected, result);
	}
}

### Do Not
- Do not include comments like TODO.
- Do not hit external services or the real file system.
- Do not use Reflection unless absolutely necessary.
- Do not duplicate setup code unnecessarily.

Generate comprehensive tests now.


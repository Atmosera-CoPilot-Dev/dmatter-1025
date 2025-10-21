# Copilot Instructions
Coding instructions for this repository

## C# Files
**/*.cs


### Runtime Version
- Minimum required C# version: 8
- Prefer using modern C# features when they simplify code

### General Guidelines
- Add a brief file header comment describing purpose
- Use string interpolation; follow C# coding conventions
- Provide XML doc comments for all public functions/classes
- Use explicit types for all public members
- Avoid deprecated APIs

### Error Handling
- Wrap fallible operations in try/catch (no bare catch)
- Log errors using standard .NET logging format
- Fail fast with clear messages

### Testing Conventions
- Framework: xUnit only
- File pattern: TemplateMethodApp.Tests/*.cs (mirror source tree)
- Structure: classes subclassing Xunit's Fact or Theory attributes; use constructor/Dispose for setup/teardown as needed
- Use Moq for external dependencies; keep tests deterministic
- Prefer Assert.* methods (no bare assert)
- Run: dotnet test
- Coverage (optional): use coverlet or dotnet-coverage tools
- Target: ≥80% coverage of executable code

### Version Control
- Clear, concise commit messages
- Use feature branches for new work

## SQL Files
**/*.sql
- SQLite syntax only
- Uppercase SQL keywords
- Comment complex queries
- Use explicit JOIN syntax
- Qualify all column references with table names



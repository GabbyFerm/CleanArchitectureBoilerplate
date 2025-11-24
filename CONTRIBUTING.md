# Contributing Guidelines

Thank you for contributing! This guide explains how we work in this project.

---

## 🌿 Branch Naming

Use descriptive branch names with prefixes:
```
feature/add-user-authentication
feature/implement-pagination
bugfix/fix-validation-error
bugfix/correct-null-reference
hotfix/security-patch
docs/update-readme
refactor/improve-service-layer
test/add-integration-tests
```

**Format:** `<type>/<short-description>`

---

## 🔀 Pull Request Process

### Before Creating a PR

1. **Pull latest changes from main**
```bash
   git checkout main
   git pull origin main
   git checkout your-branch
   git merge main
```

2. **Ensure everything works**
```bash
   dotnet build
   dotnet test
   dotnet format
```

3. **Update CHANGELOG.md** with your changes

### Creating the PR

1. Push your branch to GitHub
2. Create Pull Request to `main` (or `develop`)
3. Fill in the PR description:
   - What does this PR do?
   - Related issue number (if any)
   - How to test it?

### PR Checklist

- [ ] Code builds successfully
- [ ] All tests pass
- [ ] Code is formatted (`dotnet format`)
- [ ] New features have tests
- [ ] CHANGELOG.md is updated
- [ ] Documentation is updated (if needed)

---

## 📝 Commit Messages

Keep commits clear and descriptive:
```
feat: add pagination to todo list
fix: correct validation error for due date
docs: update API specifications
refactor: simplify repository pattern
test: add unit tests for TodoService
```

**Format:** `<type>: <description>`

**Types:** `feat`, `fix`, `docs`, `refactor`, `test`, `style`, `chore`

---

## 💻 Code Style

### Naming Conventions
```csharp
// Classes, Methods, Properties - PascalCase
public class TodoService
{
    public async Task<OperationResult> CreateAsync() { }
}

// Private fields - _camelCase
private readonly IRepository _repository;

// Local variables, parameters - camelCase
var todoItem = new TodoItem();
public void Handle(string userId) { }

// Interfaces - prefix with I
public interface ITodoService { }

// Constants - PascalCase
public const int MaxLength = 200;
```

### Code Organization
```csharp
// ✅ GOOD: Clean, descriptive, single responsibility
public class CreateTodoItemCommandHandler : IRequestHandler<CreateTodoItemCommand, OperationResult<TodoItemDto>>
{
    private readonly IGenericRepository<TodoItem> _repository;

    public CreateTodoItemCommandHandler(IGenericRepository<TodoItem> repository)
    {
        _repository = repository;
    }

    public async Task<OperationResult<TodoItemDto>> Handle(
        CreateTodoItemCommand request,
        CancellationToken cancellationToken)
    {
        // Business logic here
        var todoItem = new TodoItem
        {
            Id = Guid.NewGuid(),
            Title = request.Title,
            CreatedAt = DateTime.UtcNow
        };

        await _repository.AddAsync(todoItem);
        await _repository.SaveChangesAsync();

        return OperationResult<TodoItemDto>.Success(todoItem.ToDto());
    }
}
```

### Key Principles

- **Use descriptive variable names** - `todoItem`, not `t` or `item`
- **Keep methods short** - Aim for 20 lines or less
- **Use async/await** - For all I/O operations
- **Add XML comments** - For public APIs
- **Avoid magic numbers** - Use named constants
```csharp
// ❌ BAD: Magic number
if (title.Length > 200) { }

// ✅ GOOD: Named constant
private const int MaxTitleLength = 200;
if (title.Length > MaxTitleLength) { }
```

---

## 🧪 Testing

### Test Naming
```csharp
[MethodName]_[Scenario]_[ExpectedResult]
```

**Examples:**
```csharp
[Fact]
public async Task CreateAsync_ValidCommand_ShouldCreateTodoItem() { }

[Fact]
public async Task GetByIdAsync_NonExistentId_ShouldReturnNull() { }

[Fact]
public void Validate_EmptyTitle_ShouldHaveError() { }
```

### Test Structure

Use **Arrange-Act-Assert** pattern:
```csharp
[Fact]
public async Task CreateAsync_ValidCommand_ShouldCreateTodoItem()
{
    // Arrange
    var command = new CreateTodoItemCommand { Title = "Test" };
    _mockRepository.Setup(r => r.AddAsync(It.IsAny<TodoItem>()))
        .ReturnsAsync((TodoItem item) => item);

    // Act
    var result = await _handler.Handle(command, CancellationToken.None);

    // Assert
    result.Should().NotBeNull();
    result.IsSuccess.Should().BeTrue();
    _mockRepository.Verify(r => r.AddAsync(It.IsAny<TodoItem>()), Times.Once);
}
```

### Test Requirements

- Write tests for all new features
- Use **xUnit** + **Moq** + **FluentAssertions**
- Tests must be **fast** and **isolated**
- All tests must **pass** before submitting PR

---

## 📂 Project Structure

When adding new features, follow this structure:
```
Application/
└── YourFeature/
    ├── Commands/
    │   └── CreateYourFeature/
    │       ├── CreateYourFeatureCommand.cs
    │       ├── CreateYourFeatureCommandHandler.cs
    │       └── CreateYourFeatureCommandValidator.cs
    └── Queries/
        └── GetYourFeature/
            ├── GetYourFeatureQuery.cs
            └── GetYourFeatureQueryHandler.cs
```

---

## 📋 Quick Checklist

Before submitting your PR, verify:
```bash
# 1. Code builds
dotnet build --configuration Release

# 2. Tests pass
dotnet test

# 3. Code is formatted
dotnet format

# 4. No warnings
dotnet build --configuration Release /warnaserror
```

---

## ❓ Questions?

- Open an issue for questions
- Check existing issues and PRs
- Review [ARCHITECTURE.md](ARCHITECTURE.md) for design patterns

---

**Thank you for contributing! 🙏**

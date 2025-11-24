# 🏗️ Clean Architecture .NET Boilerplate

A production-ready boilerplate for building .NET Web APIs using **Clean Architecture** principles with **CQRS**, **MediatR**, and **FluentValidation**.

[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4)](https://dotnet.microsoft.com/)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

---

## 🎯 Purpose

This boilerplate provides a solid foundation for building maintainable, testable, and scalable .NET applications. It's designed to be:

- **Ready to use** - Clone and start building immediately
- **Easy to understand** - Clear structure with comprehensive documentation
- **Production-ready** - Includes logging, validation, error handling, and CI/CD
- **Flexible** - Easy to customize for your specific needs

Perfect for:
- Starting new API projects
- Learning Clean Architecture patterns
- Establishing team coding standards
- Building production applications

---

## 🚀 Quick Start

### Prerequisites

- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- [Visual Studio 2022](https://visualstudio.microsoft.com/) / [VS Code](https://code.visualstudio.com/) / [Rider](https://www.jetbrains.com/rider/)
- (Optional) [SQL Server](https://www.microsoft.com/sql-server) for production use

### Installation

1. **Clone the repository**
```bash
   git clone https://github.com/yourusername/cleanarchitecture-boilerplate.git
   cd cleanarchitecture-boilerplate
```

2. **Restore dependencies**
```bash
   dotnet restore
```

3. **Build the solution**
```bash
   dotnet build
```

4. **Run the API**
```bash
   cd src/Api
   dotnet run
```

5. **Open Swagger UI**
```
   Navigate to: https://localhost:7286/swagger
```

That's it! The API is running with an in-memory database. No setup required! 🎉

---

## 📦 What's Included

### Core Features
- ✅ **Clean Architecture** - Clear separation of concerns across layers
- ✅ **CQRS Pattern** - Commands and Queries with MediatR
- ✅ **Generic Repository** - Reusable data access pattern
- ✅ **FluentValidation** - Automatic request validation
- ✅ **Logging** - Structured logging with Serilog
- ✅ **Exception Handling** - Global error handling middleware
- ✅ **Swagger/OpenAPI** - Interactive API documentation
- ✅ **Unit Tests** - Comprehensive test coverage with xUnit
- ✅ **CI/CD** - GitHub Actions workflows

### Architectural Patterns
- **Dependency Injection** - Per-layer service registration
- **Operation Result Pattern** - Consistent response handling
- **Pipeline Behaviors** - Logging and validation via MediatR
- **DTO Mapping** - Clean data transfer between layers

---

## 🏗️ Architecture

### Project Structure
```
CleanArchitectureBoilerplate/
├── src/
│   ├── Api/                          # Presentation Layer
│   │   ├── Controllers/              # API endpoints
│   │   ├── Middleware/               # Custom middleware
│   │   ├── Configuration/            # API-specific config
│   │   └── Program.cs                # Application entry point
│   │
│   ├── Application/                  # Application Layer
│   │   ├── Common/                   # Shared application logic
│   │   │   ├── Behaviours/           # MediatR pipeline behaviors
│   │   │   ├── Mappings/             # DTO mappings
│   │   │   └── Models/               # Common models (OperationResult)
│   │   ├── TodoItems/                # Feature folders (CQRS)
│   │   │   ├── Commands/             # Write operations
│   │   │   └── Queries/              # Read operations
│   │   ├── DTOs/                     # Data Transfer Objects
│   │   ├── Interfaces/               # Application interfaces
│   │   └── DependencyInjection.cs    # Service registration
│   │
│   ├── Infrastructure/               # Infrastructure Layer
│   │   ├── Data/                     # EF Core DbContext
│   │   ├── Repositories/             # Repository implementations
│   │   ├── Services/                 # External service implementations
│   │   └── DependencyInjection.cs    # Service registration
│   │
│   └── Domain/                       # Domain Layer
│       ├── Common/                   # Base entities
│       └── Entities/                 # Domain entities
│
├── tests/
│   └── Tests/                        # All tests in one project
│       ├── DomainTests/              # Domain logic tests
│       ├── ApplicationTests/         # Business logic tests
│       └── InfrastructureTests/      # Repository tests
│
├── .github/
│   └── workflows/                    # CI/CD workflows
│
├── README.md                         # This file
├── ARCHITECTURE.md                   # Detailed architecture docs
├── SPECS.md                          # API specifications
├── CHANGELOG.md                      # Version history
└── CONTRIBUTING.md                   # Contribution guidelines
```

### Dependency Flow
```
Api → Application → Domain
  ↓
Infrastructure → Application (via interfaces)
               → Domain (entities)
```

**Key Principle:** Dependencies point inward. Domain has no dependencies.

---

## 📡 API Endpoints

### TodoItems Resource

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/api/todo` | Get all todo items |
| `GET` | `/api/todo/{id}` | Get a specific todo item |
| `POST` | `/api/todo` | Create a new todo item |
| `PUT` | `/api/todo/{id}` | Update an existing todo item |
| `DELETE` | `/api/todo/{id}` | Delete a todo item |

### Health Check

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/health` | API health check |

See [SPECS.md](SPECS.md) for detailed API specifications.

---

## 🔧 Configuration

### Database Configuration

**Development (Default):**
The boilerplate uses an **in-memory database** for easy setup. No configuration needed!

**Production:**
Update `src/Infrastructure/DependencyInjection.cs` to use SQL Server:
```csharp
services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(
        configuration.GetConnectionString("DefaultConnection"),
        b => b.MigrationsAssembly(typeof(ApplicationDbContext).Assembly.FullName)));
```

Add connection string to `appsettings.json`:
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=YourDb;Trusted_Connection=true;TrustServerCertificate=true;"
  }
}
```

### Environment Variables

Create `appsettings.Development.json` or `appsettings.Production.json`:
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

---

## 🧪 Testing

### Run All Tests
```bash
dotnet test
```

### Run Tests with Coverage
```bash
dotnet test --collect:"XPlat Code Coverage"
```

### Test Categories
- **Domain Tests** - Entity validation and business rules
- **Application Tests** - Commands, queries, and validators
- **Infrastructure Tests** - Repository operations with in-memory database

---

## 🔄 Generic Repository Pattern

The boilerplate includes a **Generic Repository** that works with any entity:
```csharp
public interface IGenericRepository<T> where T : class
{
    Task<T?> GetByIdAsync(Guid id);
    Task<IEnumerable<T>> ListAsync();
    Task<T> AddAsync(T entity);
    Task UpdateAsync(T entity);
    Task DeleteAsync(Guid id);
    Task<int> SaveChangesAsync();
}
```

**Usage in your services:**
```csharp
public class YourService
{
    private readonly IGenericRepository<YourEntity> _repository;

    public YourService(IGenericRepository<YourEntity> repository)
    {
        _repository = repository;
    }
}
```

**Automatic registration** via dependency injection!

---

## 📖 Documentation

- [ARCHITECTURE.md](ARCHITECTURE.md) - Detailed architecture explanation
- [SPECS.md](SPECS.md) - Complete API specifications
- [CONTRIBUTING.md](CONTRIBUTING.md) - How to contribute to this project
- [CHANGELOG.md](CHANGELOG.md) - Version history and changes

---

## 🛠️ Built With

- [.NET 8](https://dotnet.microsoft.com/) - Framework
- [ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/) - Web framework
- [Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/) - ORM
- [MediatR](https://github.com/jbogard/MediatR) - CQRS implementation
- [FluentValidation](https://fluentvalidation.net/) - Validation library
- [Serilog](https://serilog.net/) - Logging framework
- [Swashbuckle](https://github.com/domaindrivendev/Swashbuckle.AspNetCore) - Swagger/OpenAPI
- [xUnit](https://xunit.net/) - Testing framework
- [Moq](https://github.com/moq/moq4) - Mocking library
- [FluentAssertions](https://fluentassertions.com/) - Assertion library

---

## 🤝 Contributing

Contributions are welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for details on our code of conduct and the process for submitting pull requests.

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 🙏 Acknowledgments

- Inspired by [Jason Taylor's Clean Architecture Template](https://github.com/jasontaylordev/CleanArchitecture)
- [Microsoft's eShopOnWeb](https://github.com/dotnet-architecture/eShopOnWeb)
- Clean Architecture principles by Robert C. Martin (Uncle Bob)

---

## 🌟 Star This Repository

If you find this boilerplate helpful, please give it a ⭐ on GitHub!

**Happy coding! 🚀**

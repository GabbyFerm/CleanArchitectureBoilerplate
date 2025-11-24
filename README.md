# 🏗️ Clean Architecture .NET Boilerplate

A production-ready boilerplate for building .NET Web APIs using Clean Architecture, CQRS, MediatR, and FluentValidation.

[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4)](https://dotnet.microsoft.com/)
[![.NET CI](https://github.com/GabbyFerm/CleanArchitectureBoilerplate/actions/workflows/dotnet-ci.yml/badge.svg)](https://github.com/GabbyFerm/CleanArchitectureBoilerplate/actions/workflows/dotnet-ci.yml)
[![Code Format](https://github.com/GabbyFerm/CleanArchitectureBoilerplate/actions/workflows/code-format.yml/badge.svg)](https://github.com/GabbyFerm/CleanArchitectureBoilerplate/actions/workflows/code-format.yml)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

---

## 🎯 Why Use This?

- ✅ **Clean Architecture** - Proper separation of concerns
- ✅ **CQRS + MediatR** - Scalable command/query pattern
- ✅ **Ready to Use** - Clone and start building immediately
- ✅ **Well Tested** - Comprehensive test coverage included
- ✅ **CI/CD Ready** - GitHub Actions workflows configured

Perfect for starting new API projects or learning Clean Architecture!

---

## 🚀 Quick Start

### Prerequisites
- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- Your favorite IDE

### Get Started in 30 Seconds
```bash
# Clone the repository
git clone https://github.com/yourusername/cleanarchitecture-boilerplate.git
cd cleanarchitecture-boilerplate

# Restore, build, test
dotnet restore
dotnet build
dotnet test

# Run the API
cd src/Api
dotnet run
```

Open `https://localhost:7286/swagger` - Done! 🎉

---

## 📦 What's Inside
```
src/
├── Domain/          # Business entities and rules
├── Application/     # Use cases (Commands/Queries)
├── Infrastructure/  # Data access and external services
└── Api/             # REST API endpoints

tests/Tests/         # Unit and integration tests
```

**Key Features:**
- MediatR for CQRS pattern
- FluentValidation for request validation
- Generic Repository pattern
- Serilog for structured logging
- Swagger/OpenAPI documentation
- Exception handling middleware
- In-memory database (easy to switch to SQL Server)

---

## 📡 Example Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/api/todo` | Get all todos |
| GET | `/api/todo/{id}` | Get todo by ID |
| POST | `/api/todo` | Create new todo |
| PUT | `/api/todo/{id}` | Update todo |
| DELETE | `/api/todo/{id}` | Delete todo |
| GET | `/health` | Health check |

See [SPECS.md](SPECS.md) for complete API documentation.

---

## ✅ Quick Verification

Verify everything works:
```bash
dotnet build --configuration Release  # Should succeed
dotnet test                           # All tests should pass
dotnet format --verify-no-changes     # Code should be formatted
```

For detailed setup and configuration, see [SETUP.md](SETUP.md).

---

## 🏗️ Architecture

This boilerplate follows **Clean Architecture** principles:

- **Domain Layer** - Pure business logic (no dependencies)
- **Application Layer** - Use cases and business rules
- **Infrastructure Layer** - Data access and external concerns
- **API Layer** - REST endpoints and HTTP concerns

**Dependency Rule:** Dependencies point inward. Domain has zero dependencies.

For detailed architecture documentation, see [ARCHITECTURE.md](ARCHITECTURE.md).

---

## 📚 Documentation

- **[SETUP.md](SETUP.md)** - Complete setup guide and checklists
- **[ARCHITECTURE.md](ARCHITECTURE.md)** - Detailed architecture explanation
- **[SPECS.md](SPECS.md)** - Complete API specifications
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - How to contribute
- **[CHANGELOG.md](CHANGELOG.md)** - Version history

---

## 🧪 Testing
```bash
dotnet test                    # Run all tests
dotnet test --verbosity normal # Detailed output
```

Includes 20+ tests covering:
- Domain entities
- Application commands/queries
- Validators
- Repository operations

---

## 🛠️ Tech Stack

- .NET 8.0
- Entity Framework Core (In-Memory)
- MediatR
- FluentValidation
- Serilog
- Swagger/OpenAPI
- xUnit, Moq, FluentAssertions

---

## 🔄 Adapting for Your Project

1. **Fork this repository**
2. **Rename** solution and projects
3. **Replace TodoItem** with your entities
4. **Add your features** (authentication, business logic, etc.)
5. **Update documentation**

See [SETUP.md](SETUP.md) for detailed migration guide.

---

## 🤝 Contributing

Contributions welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

---

## 📄 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file.

---

## 🙏 Acknowledgments

- Inspired by [Jason Taylor's Clean Architecture](https://github.com/jasontaylordev/CleanArchitecture)
- [Microsoft's eShopOnWeb](https://github.com/dotnet-architecture/eShopOnWeb)
- Clean Architecture by Robert C. Martin (Uncle Bob)

---

## ⭐ Support

If you find this helpful, please give it a ⭐ on GitHub!

**Happy coding! 🚀**

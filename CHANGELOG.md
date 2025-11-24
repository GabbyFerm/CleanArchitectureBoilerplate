# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [Unreleased]

### Planned
- Add authentication with JWT tokens
- Add pagination support
- Add filtering and sorting for todo items
- Add API versioning
- Add rate limiting
- Add Docker support
- Add health checks for database connectivity

---

## [1.0.0] - 2024-11-24

### Added
- Initial release of Clean Architecture Boilerplate
- **Domain Layer**
  - Base entity with audit fields (Id, CreatedAt, CreatedBy, UpdatedAt, UpdatedBy)
  - TodoItem entity
- **Application Layer**
  - CQRS pattern with MediatR
  - Commands: CreateTodoItem, UpdateTodoItem, DeleteTodoItem
  - Queries: GetTodoItems, GetTodoItemById
  - FluentValidation for all commands
  - Pipeline behaviours: LoggingBehaviour, ValidationBehaviour
  - OperationResult pattern for consistent response handling
  - Generic Repository interface
  - DTO mappings
- **Infrastructure Layer**
  - Entity Framework Core with In-Memory database
  - Generic Repository implementation
  - Per-layer dependency injection
  - Database context configuration
- **API Layer**
  - RESTful API endpoints for TodoItems
  - Swagger/OpenAPI documentation
  - Global exception handling middleware
  - CORS configuration
  - Health check endpoint
  - Serilog logging (console and file)
- **Testing**
  - xUnit test framework
  - Moq for mocking
  - FluentAssertions for readable assertions
  - Unit tests for Domain, Application, and Infrastructure layers
  - 20+ comprehensive tests
- **Documentation**
  - README.md with quick start guide
  - ARCHITECTURE.md with detailed architecture explanation
  - SPECS.md with complete API specifications
  - CONTRIBUTING.md with contribution guidelines
  - CHANGELOG.md (this file)
- **CI/CD**
  - GitHub Actions workflow for build and test
  - Code formatting checks with dotnet format
  - PR validation workflow
  - PR helper with automated comments
  - Discord notifications for CI events

### Technical Details
- .NET 8.0
- C# 12
- Entity Framework Core 8.0
- MediatR 12.2.0
- FluentValidation 11.9.0
- Serilog 8.0.0
- Swashbuckle (Swagger) 6.5.0
- xUnit 2.6.0
- Moq 4.20.0
- FluentAssertions 6.12.0

---

## Version History

### [1.0.0] - 2024-11-24
- Initial release

---

## How to Use This Changelog

- **Added** for new features
- **Changed** for changes in existing functionality
- **Deprecated** for soon-to-be removed features
- **Removed** for now removed features
- **Fixed** for any bug fixes
- **Security** in case of vulnerabilities

---

## Contributing

When contributing, please update this changelog following the format above. See [CONTRIBUTING.md](CONTRIBUTING.md) for more details.

# 🏠 Bookify - Apartment Booking System

[![.NET](https://img.shields.io/badge/.NET-8.0-512BD4?style=flat-square&logo=dotnet)](https://dotnet.microsoft.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat-square&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)](https://redis.io/)
[![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)](https://www.docker.com/)
[![Keycloak](https://img.shields.io/badge/Keycloak-4D4D4D?style=flat-square&logo=keycloak&logoColor=white)](https://www.keycloak.org/)

A modern, scalable apartment booking system built with **Clean Architecture** principles using **.NET 8**. This application demonstrates enterprise-level software development practices with comprehensive testing, containerization, and robust authentication.

## ✨ Features

### 🏡 Core Functionality
- **Apartment Search**: Find available apartments with date-based filtering
- **Booking Management**: Complete booking lifecycle (Reserve → Confirm → Complete/Cancel)
- **User Authentication**: Secure JWT-based authentication with Keycloak
- **Review System**: Users can leave reviews for completed bookings
- **Pricing Engine**: Dynamic pricing calculation with amenities and cleaning fees

### 🚀 Technical Highlights
- **Clean Architecture**: Well-structured layers with clear separation of concerns
- **CQRS Pattern**: Command Query Responsibility Segregation with MediatR
- **Domain-Driven Design**: Rich domain models with business logic encapsulation
- **Event-Driven Architecture**: Domain events for loose coupling
- **Comprehensive Testing**: Unit, Integration, Functional, and Architecture tests
- **API Versioning**: Backward-compatible API versioning strategy
- **Health Checks**: Built-in health monitoring endpoints
- **Observability**: Structured logging with Serilog and Seq

## 🏗️ Architecture

This project follows **Clean Architecture** principles with the following layers:

```
┌─────────────────────────────────────────┐
│                API Layer                │
│    Controllers, Middleware, OpenAPI    │
└─────────────────────────────────────────┘
┌─────────────────────────────────────────┐
│            Application Layer            │
│     Use Cases, CQRS, Behaviors        │
└─────────────────────────────────────────┘
┌─────────────────────────────────────────┐
│              Domain Layer               │
│    Entities, Value Objects, Events     │
└─────────────────────────────────────────┘
┌─────────────────────────────────────────┐
│           Infrastructure Layer          │
│  Database, Authentication, Caching     │
└─────────────────────────────────────────┘
```

### Domain Entities
- **Apartment**: Properties with amenities, pricing, and availability
- **Booking**: Reservation lifecycle with status transitions
- **User**: Authentication and profile management
- **Review**: Rating and feedback system

## 🛠️ Technology Stack

### Backend
- **.NET 8** - Latest .NET framework
- **ASP.NET Core** - Web API framework
- **Entity Framework Core** - ORM for database operations
- **MediatR** - CQRS and mediator pattern implementation
- **FluentValidation** - Input validation

### Database & Caching
- **PostgreSQL** - Primary database
- **Redis** - Caching and session storage
- **Entity Framework Migrations** - Database versioning

### Authentication & Security
- **Keycloak** - Identity and access management
- **JWT Bearer** - Token-based authentication
- **Role-based Authorization** - Granular permissions

### Observability & Logging
- **Serilog** - Structured logging
- **Seq** - Log aggregation and analysis
- **Health Checks** - Application monitoring

### DevOps & Deployment
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration
- **Health Checks UI** - Monitoring dashboard

### Testing
- **xUnit** - Unit testing framework
- **FluentAssertions** - Assertion library
- **Testcontainers** - Integration testing with containers
- **ArchUnitNET** - Architecture testing

## 🚀 Getting Started

### Prerequisites
- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Git](https://git-scm.com/)

### Quick Start with Docker

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/bookify.git
   cd bookify
   ```

2. **Start the application**
   ```bash
   docker-compose up -d
   ```

3. **Access the services**
   - **API**: http://localhost:5000
   - **Swagger UI**: http://localhost:5000/swagger
   - **Keycloak**: http://localhost:18080 (admin/admin)
   - **Seq Logs**: http://localhost:8081
   - **Health Checks**: http://localhost:5000/health

### Development Setup

1. **Start infrastructure services**
   ```bash
   docker-compose up -d bookify-db bookify-idp bookify-seq bookify-redis
   ```

2. **Update database**
   ```bash
   cd src/Bookify.Api
   dotnet ef database update
   ```

3. **Run the application**
   ```bash
   dotnet run --project src/Bookify.Api
   ```

## 📖 API Documentation

The API is fully documented with **OpenAPI/Swagger**. Once the application is running, visit:
- **Swagger UI**: http://localhost:5000/swagger

### Key Endpoints

#### Authentication
```http
POST /api/v1/users/register    # Register new user
POST /api/v1/users/login       # User login
```

#### Apartments
```http
GET /api/v1/apartments         # Search apartments
```

#### Bookings
```http
GET /api/v1/bookings/{id}      # Get booking details
POST /api/v1/bookings          # Reserve apartment
```

#### Reviews
```http
POST /api/v1/reviews           # Add review
```

### Authentication

The API uses **JWT Bearer tokens**. Include the token in the Authorization header:
```http
Authorization: Bearer <your-jwt-token>
```

## 🧪 Testing

The project includes comprehensive testing at multiple levels:

### Run All Tests
```bash
dotnet test
```

### Test Categories
- **Unit Tests**: Test individual components in isolation
- **Integration Tests**: Test application layers integration
- **Functional Tests**: Test complete user scenarios
- **Architecture Tests**: Enforce architectural constraints

### Test Projects
- `Bookify.Domain.UnitTests`
- `Bookify.Application.UnitTests`
- `Bookify.Application.IntegrationTests`
- `Bookify.Api.FunctionalTests`
- `Bookify.ArchitectureTests`

## 📊 Monitoring & Observability

### Health Checks
Monitor application health at: http://localhost:5000/health

Includes checks for:
- Database connectivity
- Redis connectivity
- External services

### Logging
- **Structured Logging** with Serilog
- **Centralized Logs** in Seq dashboard
- **Request/Response Logging** middleware
- **Performance Monitoring**

## 🗂️ Project Structure

```
📦 Bookify/
├── 📁 src/
│   ├── 📁 Bookify.Api/              # Web API layer
│   ├── 📁 Bookify.Application/      # Application layer
│   ├── 📁 Bookify.Domain/          # Domain layer
│   └── 📁 Bookify.Infrastructure/   # Infrastructure layer
├── 📁 test/                        # Test projects
├── 📄 docker-compose.yml          # Container orchestration
└── 📄 Directory.Build.props        # Shared build properties
```

## 🔧 Configuration

### Environment Variables
```env
ConnectionStrings__Database=Host=localhost;Database=bookify;Username=postgres;Password=postgres
Authentication__Issuer=http://localhost:18080/realms/bookify
Authentication__Audience=bookify-api
Cache__ConnectionString=localhost:6379
```

### Docker Configuration
- **API**: Port 5000
- **Database**: PostgreSQL on port 5432
- **Identity**: Keycloak on port 18080
- **Cache**: Redis on port 6379
- **Logs**: Seq on port 8081

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Code Quality
- Follow C# coding conventions
- Maintain test coverage above 80%
- Ensure all tests pass
- Run code analysis and fix warnings

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- **Clean Architecture** by Robert C. Martin
- **Domain-Driven Design** by Eric Evans
- **CQRS Pattern** implementation with MediatR
- **Enterprise Integration Patterns**

---

<div align="center">

**Built with ❤️ using .NET 8 and Clean Architecture**

[Report Bug](https://github.com/yourusername/bookify/issues) • [Request Feature](https://github.com/yourusername/bookify/issues) • [Documentation](https://github.com/yourusername/bookify/wiki)

</div>

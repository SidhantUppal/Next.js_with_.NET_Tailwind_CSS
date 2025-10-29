# MyApp API

A modern .NET 8 Web API built with ServiceStack, featuring AutoQuery CRUD operations, authentication, and SQLite database integration.

## 🚀 Features

- **ServiceStack Framework**: Leveraging ServiceStack 8.x for rapid API development
- **AutoQuery CRUD**: Declarative CRUD operations with minimal code
- **Authentication & Authorization**: Built-in authentication with role-based access control
- **Database**: SQLite with OrmLite for efficient data access
- **Code-First Migrations**: Automatic database schema management
- **API Documentation**: Auto-generated API documentation
- **Testing**: Unit and integration tests included

## 📁 Project Structure

```
api/
├── MyApp/                          # Main web application
│   ├── Configure.AppHost.cs        # ServiceStack AppHost configuration
│   ├── Configure.Auth.cs           # Authentication configuration
│   ├── Configure.AuthRepository.cs # Auth repository setup
│   ├── Configure.AutoQuery.cs      # AutoQuery configuration
│   ├── Configure.Db.cs             # Database configuration
│   ├── Configure.Db.Migrations.cs  # Migration configuration
│   ├── Migrations/                 # Database migrations
│   │   └── Migration1000.cs
│   ├── App_Data/                   # Application data (SQLite DB)
│   ├── wwwroot/                    # Static files (UI build output)
│   ├── appsettings.json            # Application settings
│   └── Program.cs                  # Application entry point
│
├── MyApp.ServiceInterface/         # Service implementations
│   ├── MyServices.cs               # General service implementations
│   └── TodosServices.cs            # Todo service implementations
│
├── MyApp.ServiceModel/             # Data Transfer Objects (DTOs)
│   ├── Bookings.cs                 # Booking API contracts
│   ├── Todos.cs                    # Todo API contracts
│   ├── Hello.cs                    # Example API contract
│   └── Types/                      # Shared types
│
└── MyApp.Tests/                    # Test project
    ├── IntegrationTest.cs          # Integration tests
    └── UnitTest.cs                 # Unit tests
```

## 🛠️ Prerequisites

- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)
- [Visual Studio 2022](https://visualstudio.microsoft.com/) or [Rider](https://www.jetbrains.com/rider/) (optional)

## 🏁 Getting Started

### 1. Restore Dependencies

```bash
cd api
dotnet restore
```

### 2. Run Database Migrations

```bash
cd MyApp
dotnet run --AppTasks=migrate
```

### 3. Run the Application

```bash
dotnet run
```

The API will be available at:
- **HTTP**: `http://localhost:5000`
- **HTTPS**: `https://localhost:5001`

### 4. Access API Documentation

Once running, visit:
- **API Explorer**: `https://localhost:5001/ui`
- **Metadata**: `https://localhost:5001/metadata`

## 📊 API Endpoints

### Bookings API

Complete CRUD operations for room bookings:

- `GET /bookings` - Query all bookings
- `GET /bookings/{Id}` - Get specific booking
- `POST /bookings` - Create new booking (requires Employee role)
- `PATCH /booking/{Id}` - Update booking (requires Employee role)
- `DELETE /booking/{Id}` - Delete booking (requires Manager role)

### Todos API

TodoMVC-style todo management:

- `GET /todos` - Query todos
- `POST /todos` - Create todo
- `PUT /todos/{Id}` - Update todo
- `DELETE /todos/{Id}` - Delete single todo
- `DELETE /todos` - Delete multiple todos

### Hello World API

Example endpoint:

- `GET /hello/{Name}` - Simple greeting endpoint

## 🗃️ Database

The application uses **SQLite** as the database, stored in the `App_Data` folder:

- **Development**: `App_Data/app.db`
- **OrmLite**: ServiceStack's OrmLite provides the data access layer

### Database Migrations

Manage database schema changes with built-in migrations:

```bash
# Run all pending migrations
dotnet run --AppTasks=migrate

# Revert last migration
dotnet run --AppTasks=migrate.revert:last

# Revert all migrations
dotnet run --AppTasks=migrate.revert:all
```

### Adding New Migrations

1. Create a new migration class in `MyApp/Migrations/`
2. Inherit from `Migration`
3. Implement `Up()` and `Down()` methods

Example:

```csharp
public class Migration1001 : Migration
{
    public override void Up()
    {
        Db.CreateTable<NewTable>();
    }

    public override void Down()
    {
        Db.DropTable<NewTable>();
    }
}
```

## 🔐 Authentication

The API includes authentication support:

- **Authentication Types**: Credentials-based authentication
- **Authorization**: Role-based access control (Employee, Manager)
- **User Repository**: Configured in `Configure.AuthRepository.cs`

### Protected Endpoints

Some endpoints require authentication and specific roles:
- Creating/Updating Bookings: `Employee` role
- Deleting Bookings: `Manager` role

## 🧪 Testing

Run the test suite:

```bash
cd MyApp.Tests
dotnet test
```

The test project includes:
- **Unit Tests**: Testing individual service logic
- **Integration Tests**: End-to-end API testing

## 🔧 Development

### Adding a New Service

1. **Define DTO** in `MyApp.ServiceModel`:
```csharp
[Route("/myendpoint", "GET")]
public class MyRequest : IReturn<MyResponse>
{
    public string Name { get; set; }
}

public class MyResponse
{
    public string Result { get; set; }
}
```

2. **Implement Service** in `MyApp.ServiceInterface`:
```csharp
public class MyService : Service
{
    public object Any(MyRequest request)
    {
        return new MyResponse { Result = $"Hello {request.Name}" };
    }
}
```

### Configuration Files

- `appsettings.json` - Production settings
- `appsettings.Development.json` - Development-specific settings
- `Configure.*.cs` - Modular configuration classes

## 📦 Building for Production

```bash
# Publish the application
dotnet publish -c Release

# Output will be in: bin/Release/net8.0/publish/
```

## 🔗 Related Technologies

- [ServiceStack](https://servicestack.net/) - Web services framework
- [ServiceStack OrmLite](https://github.com/ServiceStack/ServiceStack.OrmLite) - Fast, simple ORM
- [ServiceStack AutoQuery](https://docs.servicestack.net/autoquery/) - Automatic querying
- [SQLite](https://www.sqlite.org/) - Lightweight database

## 📚 Learn More

- [ServiceStack Documentation](https://docs.servicestack.net/)
- [AutoQuery CRUD Bookings Tutorial](https://docs.servicestack.net/autoquery-crud-bookings)
- [.NET 8 Documentation](https://learn.microsoft.com/en-us/dotnet/)

## 📝 License

This project is part of a ServiceStack template and follows ServiceStack's licensing terms.


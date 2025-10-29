# Next.js_with_.NET_Tailwind_CSS
**Next.js with .NET and Tailwind CSS** offers a modern full-stack development approach combining the speed of Next.js for dynamic front-end rendering, the power of .NET for robust backend APIs, and the elegance of Tailwind CSS for responsive design—delivering scalable, high-performance, and visually consistent web applications.

## 🎯 Overview

This project demonstrates a modern full-stack architecture with:

- **Backend**: .NET 8 Web API using ServiceStack framework
- **Frontend**: Next.js 13 with TypeScript and Tailwind CSS
- **Database**: SQLite with OrmLite
- **API Type Safety**: Auto-generated TypeScript DTOs from C# models
- **Authentication**: Built-in user authentication and authorization
- **Deployment**: Single deployable unit with static UI served by .NET backend

## 🏗️ Architecture

```
.NET_with_Next.js_Tailwindcss/
│
├── api/                    # .NET 8 Backend
│   ├── MyApp/              # Main web application & API host
│   ├── MyApp.ServiceInterface/   # Service implementations
│   ├── MyApp.ServiceModel/       # DTOs and API contracts
│   └── MyApp.Tests/              # Unit & integration tests
│
└── ui/                     # Next.js Frontend
    ├── components/         # React components
    ├── pages/              # Next.js pages (routes)
    ├── lib/                # API client & utilities
    ├── styles/             # Tailwind CSS styles
    └── public/             # Static assets
```

## ✨ Features

### Backend Features
- ✅ ServiceStack 8.x framework
- ✅ AutoQuery CRUD operations
- ✅ Role-based authentication & authorization
- ✅ Code-first database migrations
- ✅ SQLite database with OrmLite
- ✅ Auto-generated API documentation
- ✅ Built-in testing framework

### Frontend Features
- ✅ Next.js 13 with TypeScript
- ✅ Tailwind CSS for styling
- ✅ Type-safe API calls with ServiceStack client
- ✅ SWR for data fetching and caching
- ✅ MDX support for content pages
- ✅ Responsive design
- ✅ Authentication flows (signin/signup/profile)
- ✅ Example CRUD operations (Bookings & Todos)

## 🚀 Quick Start

### Prerequisites

- [.NET 8 SDK]
- [Node.js 18+]
- npm or yarn

### 1. Clone & Install

```bash
# Install backend dependencies
cd api
dotnet restore

# Install frontend dependencies
cd ../ui
npm install
```

The `npm install` command will automatically run database migrations.

### 2. Generate TypeScript DTOs

```bash
cd ui
npm run dtos
```

### 3. Start Development Servers

**Terminal 1 - Backend:**
```bash
cd api/MyApp
dotnet run
```
Backend will run at `https://localhost:5001`

**Terminal 2 - Frontend:**
```bash
cd ui
npm run dev
```
Frontend will run at `http://localhost:3000`

### 4. Open in Browser

Navigate to `http://localhost:3000` to see the application.

## 🔧 Development Workflow

### Adding a New API Endpoint

1. **Define DTO** in `api/MyApp.ServiceModel/`:
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

2. **Implement Service** in `api/MyApp.ServiceInterface/`:
```csharp
public class MyService : Service
{
    public object Any(MyRequest request)
    {
        return new MyResponse { Result = $"Hello {request.Name}" };
    }
}
```

3. **Generate TypeScript DTOs**:
```bash
cd ui
npm run dtos
```

4. **Use in Frontend**:
```typescript
import { client } from '@/lib/gateway'
import { MyRequest } from '@/lib/dtos'

const response = await client.api(new MyRequest({ name: 'World' }))
console.log(response.response?.result) // "Hello World"
```

### Database Migrations

```bash
cd ui

# Run migrations
npm run migrate

# Revert last migration
npm run revert:last

# Rerun last migration
npm run rerun:last
```

### Building for Production

```bash
cd ui

# Build UI and export to backend wwwroot
npm run build

# Build everything and publish
npm run publish
```

## 🎯 Example Applications

The template includes two fully functional example applications:

### 1. TodoMVC (`/todomvc`)
A complete TodoMVC implementation demonstrating:
- Creating, reading, updating, and deleting todos
- Real-time updates
- Local storage persistence
- ServiceStack client integration

### 2. Bookings CRUD (`/bookings-crud`)
A room booking management system with:
- List view with AutoQuery
- Create booking form with validation
- Edit existing bookings
- Role-based delete permissions
- Audit trail (created/modified tracking)

## 🔐 Authentication

The application includes complete authentication:

- **Sign Up**: `/signup` - New user registration
- **Sign In**: `/signin` - User authentication
- **Profile**: `/profile` - User profile management (protected)
- **Admin**: `/admin` - Admin dashboard (protected)

### Roles
- **Employee**: Can create and update bookings
- **Manager**: Can delete bookings

## 🛠️ Tech Stack

### Backend
- [.NET 8]
- [ServiceStack]
- [ServiceStack OrmLite]
- [SQLite]

### Frontend
- [Next.js 13]
- [React 18]
- [TypeScript]
- [Tailwind CSS]

## 📦 Deployment

The application is designed to be deployed as a single unit:

1. The UI builds to static files
2. Static files are exported to `api/MyApp/wwwroot`
3. The .NET backend serves the static UI
4. Deploy the published .NET application

### Deployment Options

- **Azure App Service**
- **AWS Elastic Beanstalk**
- **Docker Container**
- **IIS on Windows Server**
- **Linux with Nginx**

### Build Command

```bash
cd ui
npm run publish
```

This creates a complete deployment package in `api/MyApp/bin/Release/net8.0/publish/`

## 🧪 Testing

### Backend Tests

```bash
cd api/MyApp.Tests
dotnet test
```

### Frontend Type Checking

```bash
cd ui
npm run typecheck
```

## 🤝 Contributing

Contributions are welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request


Thank You :)

**Built with ❤️ using .NET, Next.js, and Tailwind CSS**


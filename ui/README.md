# MyApp UI

A modern Next.js frontend application built with TypeScript and Tailwind CSS, featuring seamless integration with a ServiceStack .NET backend.

## 🚀 Features

- **Next.js 13**: React framework with SSG/SSR capabilities
- **TypeScript**: Type-safe development experience
- **Tailwind CSS**: Utility-first CSS framework for rapid UI development
- **ServiceStack Client**: Type-safe API integration with @servicestack/client
- **Authentication**: Built-in auth with signin/signup flows
- **MDX Support**: Write content with Markdown + JSX
- **SWR**: React Hooks for data fetching and caching
- **Responsive Design**: Mobile-first, fully responsive UI
- **Form Components**: Reusable form components with Tailwind forms plugin

## 📁 Project Structure

```
ui/
├── components/              # React components
│   ├── alert.tsx
│   ├── avatar.tsx
│   ├── breadcrumbs.tsx
│   ├── form.tsx            # Reusable form components
│   ├── layout.tsx          # Main layout wrapper
│   ├── nav.tsx             # Navigation component
│   └── ...
│
├── pages/                  # Next.js pages (file-based routing)
│   ├── _app.tsx            # App wrapper
│   ├── _document.tsx       # HTML document structure
│   ├── index.tsx           # Homepage
│   ├── signin.tsx          # Sign in page
│   ├── signup.tsx          # Sign up page
│   ├── profile.tsx         # User profile
│   ├── admin.tsx           # Admin dashboard
│   ├── todomvc.tsx         # TodoMVC implementation
│   ├── bookings-crud/      # Bookings CRUD pages
│   │   ├── index.tsx       # List bookings
│   │   ├── create.tsx      # Create booking
│   │   └── edit.tsx        # Edit booking
│   ├── posts/              # Blog posts
│   └── *.mdx               # MDX pages
│
├── lib/                    # Utility libraries
│   ├── api.ts              # API utilities
│   ├── dtos.ts             # Generated TypeScript DTOs
│   ├── gateway.ts          # ServiceStack gateway
│   ├── useAuth.ts          # Authentication hook
│   └── utils.ts            # General utilities
│
├── styles/                 # Global styles
│   ├── index.css
│   └── main.css
│
├── public/                 # Static assets
│   ├── assets/
│   ├── favicon/
│   └── modules/
│
├── types/                  # TypeScript type definitions
├── _posts/                 # Blog post content
└── @types/                 # Custom type declarations
```

## 🛠️ Prerequisites

- [Node.js 18+](https://nodejs.org/)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
- .NET 8 SDK (for backend integration)

## 🏁 Getting Started

### 1. Install Dependencies

```bash
cd ui
npm install
```

This will also automatically run database migrations via the postinstall script.

### 2. Generate TypeScript DTOs

Generate type-safe DTOs from your ServiceStack backend:

```bash
npm run dtos
```

This creates/updates `lib/dtos.ts` with all your API contracts.

### 3. Start Development Server

```bash
npm run dev
```

The application will be available at `http://localhost:3000`

## 🔨 Available Scripts

### Development

```bash
npm run dev          # Start Next.js development server
npm run typecheck    # Run TypeScript type checking
npm run dtos         # Generate TypeScript DTOs from backend
```

### Database Migrations

```bash
npm run migrate      # Run all pending migrations
npm run revert:last  # Revert the last migration
npm run revert:all   # Revert all migrations
npm run rerun:last   # Revert and re-run last migration
```

### Build & Deploy

```bash
npm run build        # Build for production and export to ../api/MyApp/wwwroot
npm run build:local  # Build for local development
npm run publish      # Build UI and publish .NET backend
npm start            # Start Next.js production server
```

## 🎨 Styling

The application uses **Tailwind CSS** for styling:

- **Configuration**: `tailwind.config.js`
- **Plugins**: 
  - `@tailwindcss/forms` - Better form styling
  - `@tailwindcss/typography` - Beautiful typographic defaults
- **Main Styles**: `styles/index.css`

### Customizing Tailwind

Edit `tailwind.config.js` to customize:
- Colors
- Fonts
- Spacing
- Breakpoints
- And more...

## 🔐 Authentication

The app includes complete authentication flows:

### Pages
- `/signin` - User sign in
- `/signup` - User registration  
- `/profile` - User profile (protected)
- `/admin` - Admin dashboard (protected)

### Using Authentication

```typescript
import { useAuth } from '@/lib/useAuth'

export default function MyComponent() {
  const { user, signIn, signOut } = useAuth()
  
  if (!user) {
    return <button onClick={() => signIn(credentials)}>Sign In</button>
  }
  
  return <button onClick={signOut}>Sign Out</button>
}
```

## 📡 API Integration

### ServiceStack Client

The app uses `@servicestack/client` for type-safe API calls:

```typescript
import { client } from '@/lib/gateway'
import { QueryBookings } from '@/lib/dtos'

// Type-safe API call
const response = await client.api(new QueryBookings())
if (response.succeeded) {
  console.log(response.response?.results)
}
```

### API Gateway Configuration

The API gateway is configured in `lib/gateway.ts`:

```typescript
import { JsonServiceClient } from '@servicestack/client'

export const client = new JsonServiceClient(
  process.env.NEXT_PUBLIC_API_URL || 'https://localhost:5001'
)
```

## 📄 Content Management

### Blog Posts

Create new blog posts in the `_posts/` directory:

```markdown
---
title: 'My Post Title'
excerpt: 'A brief description'
date: '2024-01-01'
author:
  name: 'Author Name'
---

# Your content here
```

### MDX Pages

Create interactive pages with MDX (Markdown + JSX):

```mdx
import MyComponent from '@/components/MyComponent'

# My Page

<MyComponent />
```

## 🎯 Key Features Implementation

### TodoMVC (`/todomvc`)
Full TodoMVC implementation demonstrating:
- CRUD operations
- Real-time updates with SWR
- ServiceStack client integration

### Bookings CRUD (`/bookings-crud`)
Complete booking management system with:
- List view with filtering
- Create new bookings
- Edit existing bookings
- Delete bookings (role-based)
- Form validation

## 🏗️ Building for Production

### Export Static Site

```bash
npm run build
```

This command:
1. Builds the Next.js application
2. Exports static files to `../api/MyApp/wwwroot`
3. Makes the site ready to be served by the .NET backend

### Full Publish

```bash
npm run publish
```

This command:
1. Builds the UI
2. Publishes the .NET backend in Release mode
3. Creates a complete deployment package

## 🌐 Deployment

The built static site is exported to `../api/MyApp/wwwroot`, allowing the .NET backend to serve the frontend. This creates a single deployable unit.

### Deployment Options

1. **Docker**: Containerize the entire application
2. **IIS**: Deploy to Windows Server with IIS
3. **Azure**: Deploy to Azure App Service
4. **AWS**: Deploy to AWS Elastic Beanstalk or EC2
5. **Static Hosting**: Export and deploy to Netlify, Vercel, etc.

## 🔧 Configuration

### Environment Variables

Create a `.env.local` file for local development:

```env
NEXT_PUBLIC_API_URL=https://localhost:5001
```

### Next.js Configuration

Customize Next.js behavior in `next.config.mjs`:

```javascript
export default {
  reactStrictMode: true,
  // Your custom config
}
```

## 📦 Key Dependencies

- **next** (^13.1.5) - React framework
- **react** (^18.2.0) - UI library
- **typescript** (^4.9.4) - Type safety
- **tailwindcss** (^3.2.4) - CSS framework
- **@servicestack/client** (^2.1.1) - ServiceStack client
- **swr** (^2.0.1) - Data fetching hooks
- **@mdx-js/loader** (^2.2.1) - MDX support

## 🐛 Troubleshooting

### TypeScript Errors

```bash
npm run typecheck
```

### Regenerate DTOs

If API contracts change:

```bash
npm run dtos
```

### Clear Next.js Cache

```bash
rm -rf .next
npm run dev
```

## 📚 Learn More

- [Next.js Documentation](https://nextjs.org/docs)
- [Tailwind CSS Documentation](https://tailwindcss.com/docs)
- [ServiceStack TypeScript Documentation](https://docs.servicestack.net/typescript-add-servicestack-reference)
- [SWR Documentation](https://swr.vercel.app/)
- [React Documentation](https://react.dev/)

## 🤝 Contributing

1. Create a feature branch
2. Make your changes
3. Run type checking: `npm run typecheck`
4. Test thoroughly
5. Submit a pull request

## 📝 License

This project is part of a ServiceStack template and follows the project's licensing terms.


# Next.js Clean Project Structure (TypeScript)

A scalable and clean folder structure for modern Next.js applications using:

- Next.js App Router
- TypeScript
- Tailwind CSS
- Component-based architecture
- API integration
- Reusable utilities
- Feature separation

---

# 📦 Tech Stack

- Next.js 15+
- React
- TypeScript
- Tailwind CSS
- ESLint
- Prettier

---

# 📁 Recommended Project Structure

```bash
my-app/
│
├── public/                     # Static assets
│   ├── images/
│   ├── icons/
│   └── logo.png
│
├── src/
│   │
│   ├── app/                    # App Router (Pages & Layouts)
│   │   ├── layout.tsx          # Root layout
│   │   ├── page.tsx            # Home page
│   │   ├── globals.css         # Global CSS
│   │   │
│   │   ├── dashboard/          # Dashboard route
│   │   │   ├── page.tsx
│   │   │   ├── loading.tsx
│   │   │   ├── error.tsx
│   │   │   └── layout.tsx
│   │   │
│   │   ├── auth/
│   │   │   ├── login/
│   │   │   │   └── page.tsx
│   │   │   └── register/
│   │   │       └── page.tsx
│   │   │
│   │   └── api/                # Route handlers (backend API)
│   │       └── users/
│   │           └── route.ts
│   │
│   ├── components/             # Reusable UI Components
│   │   ├── ui/                 # Generic reusable UI
│   │   │   ├── Button.tsx
│   │   │   ├── Card.tsx
│   │   │   └── Input.tsx
│   │   │
│   │   ├── layout/             # Layout components
│   │   │   ├── Navbar.tsx
│   │   │   ├── Sidebar.tsx
│   │   │   └── Footer.tsx
│   │   │
│   │   └── dashboard/          # Feature-specific components
│   │       ├── StatsCard.tsx
│   │       ├── UserTable.tsx
│   │       └── Chart.tsx
│   │
│   ├── features/               # Business/domain features
│   │   ├── auth/
│   │   │   ├── services/
│   │   │   ├── hooks/
│   │   │   ├── store/
│   │   │   ├── types.ts
│   │   │   └── utils.ts
│   │   │
│   │   └── users/
│   │       ├── services/
│   │       ├── hooks/
│   │       ├── store/
│   │       ├── types.ts
│   │       └── utils.ts
│   │
│   ├── hooks/                  # Global custom hooks
│   │   ├── useTheme.ts
│   │   └── useDebounce.ts
│   │
│   ├── lib/                    # Core libraries/configs
│   │   ├── axios.ts
│   │   ├── fetcher.ts
│   │   ├── auth.ts
│   │   └── db.ts
│   │
│   ├── services/               # API calls
│   │   ├── auth.service.ts
│   │   └── user.service.ts
│   │
│   ├── store/                  # Global state
│   │   ├── authStore.ts
│   │   └── appStore.ts
│   │
│   ├── types/                  # Global TypeScript types
│   │   ├── user.ts
│   │   ├── api.ts
│   │   └── index.ts
│   │
│   ├── utils/                  # Helper functions
│   │   ├── formatDate.ts
│   │   ├── cn.ts
│   │   └── validators.ts
│   │
│   ├── constants/              # Constant values
│   │   ├── routes.ts
│   │   ├── api.ts
│   │   └── config.ts
│   │
│   ├── config/                 # App configurations
│   │   ├── env.ts
│   │   └── site.ts
│   │
│   └── middleware.ts           # Route middleware
│
├── .env.local                  # Environment variables
├── .gitignore
├── next.config.ts
├── tsconfig.json
├── package.json
├── tailwind.config.ts
└── README.md
```

---

# 📘 Folder Explanation

---

## `/app`

Main routing system in Next.js App Router.

### Example

```tsx
app/dashboard/page.tsx
```

Creates route:

```bash
/dashboard
```

### Common Files

| File | Purpose |
|---|---|
| `page.tsx` | Route page |
| `layout.tsx` | Shared layout |
| `loading.tsx` | Loading UI |
| `error.tsx` | Error boundary |
| `not-found.tsx` | 404 page |

---

## `/components`

Reusable UI components.

### Example

```bash
components/ui/Button.tsx
```

Reusable everywhere.

### Good Practice

Separate:

- Generic UI
- Layout components
- Feature-specific components

---

## `/features`

Feature/domain-based architecture.

Each feature contains:

- hooks
- services
- store
- types
- utils

### Example

```bash
features/auth/
```

Everything related to authentication stays together.

Benefits:

- Easier scaling
- Cleaner organization
- Better maintainability

---

## `/hooks`

Reusable React hooks.

### Example

```ts
useDebounce.ts
useTheme.ts
```

---

## `/lib`

Core app setup and external libraries.

### Example

```ts
axios.ts
```

Axios instance configuration:

```ts
import axios from "axios";

export const api = axios.create({
  baseURL: process.env.NEXT_PUBLIC_API_URL,
});
```

---

## `/services`

API communication layer.

### Example

```ts
user.service.ts
```

```ts
export async function getUsers() {
  const res = await fetch("/api/users");
  return res.json();
}
```

---

## `/store`

Global state management.

Can use:

- Zustand
- Redux Toolkit
- Context API

### Example

```ts
authStore.ts
```

---

## `/types`

Global TypeScript interfaces/types.

### Example

```ts
export interface User {
  id: number;
  name: string;
  email: string;
}
```

Benefits:

- Type safety
- Better IntelliSense
- Reusability

---

## `/utils`

Pure helper functions.

### Example

```ts
formatDate.ts
```

```ts
export function formatDate(date: string) {
  return new Date(date).toLocaleDateString();
}
```

---

## `/constants`

Static constants.

### Example

```ts
export const ROUTES = {
  HOME: "/",
  DASHBOARD: "/dashboard",
};
```

---

## `/config`

Application configuration.

### Example

```ts
env.ts
```

```ts
export const env = {
  apiUrl: process.env.NEXT_PUBLIC_API_URL,
};
```

---

# ⚡ TypeScript Best Practices

---

## 1. Always Define Types

Good:

```ts
interface User {
  id: number;
  name: string;
}
```

Bad:

```ts
const user: any = {};
```

---

## 2. Use Type Inference Carefully

Good:

```ts
const name = "John";
```

No need:

```ts
const name: string = "John";
```

---

## 3. Create Shared Types

Instead of duplicating types.

Good:

```ts
types/user.ts
```

---

## 4. Use DTO/API Response Types

```ts
interface ApiResponse<T> {
  data: T;
  message: string;
}
```

---

# ⚡ Naming Conventions

| Type | Convention |
|---|---|
| Components | PascalCase |
| Hooks | camelCase + use |
| Utilities | camelCase |
| Types | PascalCase |
| Constants | UPPER_CASE |

---

# ⚡ Example Dashboard Structure

```bash
dashboard/
│
├── page.tsx
├── loading.tsx
├── error.tsx
│
├── components/
│   ├── Sidebar.tsx
│   ├── Header.tsx
│   ├── StatsCard.tsx
│   └── Chart.tsx
│
├── hooks/
│   └── useDashboard.ts
│
├── services/
│   └── dashboard.service.ts
│
└── types/
    └── dashboard.ts
```

---

# ⚡ Clean Architecture Tips

---

## ✅ Keep Components Small

Bad:

```tsx
Dashboard.tsx = 1000 lines
```

Good:

```tsx
Dashboard
 ├── Sidebar
 ├── Header
 ├── Chart
 └── Table
```

---

## ✅ Separate Business Logic

Avoid putting API calls directly inside components.

Bad:

```tsx
useEffect(() => {
  fetch(...)
}, [])
```

Good:

```tsx
services/user.service.ts
```

---

## ✅ Reuse Components

Good reusable components:

- Button
- Modal
- Input
- Table
- Card

---

## ✅ Use Feature-Based Structure for Large Apps

Small app:

```bash
components/
pages/
```

Large app:

```bash
features/
```

---

# ⚡ Recommended Packages

```bash
npm install axios zustand react-hook-form zod
```

Optional:

```bash
npm install @tanstack/react-query
```

---

# ⚡ Environment Variables

`.env.local`

```env
NEXT_PUBLIC_API_URL=http://localhost:3000/api
```

---

# ⚡ Example tsconfig.json

```json
{
  "compilerOptions": {
    "target": "ES2020",
    "lib": ["dom", "dom.iterable", "esnext"],
    "strict": true,
    "baseUrl": "./src",
    "paths": {
      "@/*": ["*"]
    }
  }
}
```

---

# ⚡ Import Alias Example

Good:

```ts
import Button from "@/components/ui/Button";
```

Bad:

```ts
import Button from "../../../../components/ui/Button";
```

---

# ⚡ Final Best Practices

✅ Use TypeScript everywhere  
✅ Keep folder names simple  
✅ Separate UI and business logic  
✅ Reuse components  
✅ Avoid huge files  
✅ Create shared types  
✅ Use feature-based architecture for scaling  
✅ Keep APIs inside services  
✅ Use loading/error boundaries  
✅ Use aliases (`@/`)  

---

# 🚀 Suggested Learning Order

1. App Router
2. Routing & Layouts
3. Components
4. TypeScript Basics
5. API Fetching
6. State Management
7. Authentication
8. Server Components
9. Client Components
10. Performance Optimization
11. Deployment

---

# 📚 Recommended Architecture for Beginners

```bash
app/
components/
lib/
services/
types/
utils/
```

---

# 📚 Recommended Architecture for Large Scale Apps

```bash
app/
features/
components/
store/
services/
types/
config/
```

---

# 🎯 Conclusion

A clean project structure helps:

- scalability
- maintainability
- teamwork
- debugging
- faster development

Structure should grow with your project complexity.

Start simple → scale gradually.
# Architecture Overview

High-level architecture and technical decisions for the Customer Portal Frontend.

---

## 🏗️ System Architecture

### Component Architecture

```
┌─────────────────────────────────────────┐
│         Browser (Client)                │
│  ┌───────────────────────────────────┐  │
│  │    React Application (SPA)        │  │
│  │  ┌─────────────────────────────┐  │  │
│  │  │  Presentation Layer         │  │  │
│  │  │  - React Components         │  │  │
│  │  │  - Styled Components        │  │  │
│  │  └─────────────────────────────┘  │  │
│  │  ┌─────────────────────────────┐  │  │
│  │  │  Application Layer          │  │  │
│  │  │  - Redux Store              │  │  │
│  │  │  - React Query Cache        │  │  │
│  │  │  - React Router             │  │  │
│  │  └─────────────────────────────┘  │  │
│  │  ┌─────────────────────────────┐  │  │
│  │  │  Service Layer              │  │  │
│  │  │  - API Services             │  │  │
│  │  │  - Auth Service             │  │  │
│  │  │  - Storage Service          │  │  │
│  │  └─────────────────────────────┘  │  │
│  └───────────────────────────────────┘  │
└─────────────────────────────────────────┘
                   │
                   │ HTTPS / REST API
                   ▼
┌─────────────────────────────────────────┐
│         CDN (CloudFront)                │
│  - Static Assets (JS, CSS, Images)     │
│  - Edge Caching                         │
└─────────────────────────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│      API Gateway (Express.js)           │
│  - Authentication                       │
│  - Rate Limiting                        │
│  - Request Validation                   │
└─────────────────────────────────────────┘
                   │
         ┌─────────┴─────────┐
         ▼                   ▼
┌──────────────┐    ┌──────────────┐
│  PostgreSQL  │    │    Redis     │
│  (Database)  │    │   (Cache)    │
└──────────────┘    └──────────────┘
```

---

## 📦 Frontend Architecture

### Layer Structure

#### 1. Presentation Layer
**Responsibility:** UI rendering and user interaction

**Components:**
- React components (functional with hooks)
- Styled Components for styling
- Framer Motion for animations

**Principles:**
- Dumb components (no business logic)
- Reusable and composable
- Accessibility-first

#### 2. Application Layer
**Responsibility:** State management and routing

**State Management:**
- **Redux Toolkit** - Global app state (auth, user preferences)
- **React Query** - Server state (API data, caching)
- **Local State** - Component-specific state (useState)

**Routing:**
- React Router v6
- Code-splitting per route
- Protected routes for authentication

#### 3. Service Layer
**Responsibility:** External communication

**Services:**
- `apiService.ts` - HTTP client (axios)
- `authService.ts` - Authentication logic
- `storageService.ts` - LocalStorage/SessionStorage wrapper

---

## 🗂️ Folder Structure

```
src/
├── components/           # Reusable UI components
│   ├── common/          # Shared components (Button, Input, etc.)
│   ├── Navigation/      # Navigation component (PORT-2)
│   ├── Dashboard/       # Dashboard components (PORT-9)
│   └── index.ts         # Barrel exports
│
├── pages/               # Page components (routes)
│   ├── HomePage.tsx
│   ├── DashboardPage.tsx
│   └── LoginPage.tsx
│
├── layouts/             # Layout components
│   ├── MainLayout.tsx
│   └── AuthLayout.tsx
│
├── hooks/               # Custom React hooks
│   ├── useAuth.ts
│   ├── useNavigation.ts
│   └── useDashboard.ts
│
├── services/            # API and external services
│   ├── api/
│   │   ├── apiClient.ts
│   │   ├── navigationApi.ts
│   │   └── dashboardApi.ts
│   ├── auth/
│   │   └── authService.ts
│   └── storage/
│       └── storageService.ts
│
├── store/               # Redux store
│   ├── store.ts
│   ├── slices/
│   │   ├── authSlice.ts
│   │   └── userSlice.ts
│   └── hooks.ts         # Typed Redux hooks
│
├── types/               # TypeScript types
│   ├── api.types.ts
│   ├── navigation.types.ts
│   └── dashboard.types.ts
│
├── utils/               # Utility functions
│   ├── formatters.ts
│   ├── validators.ts
│   └── constants.ts
│
├── styles/              # Global styles
│   ├── theme.ts         # Design system tokens
│   ├── GlobalStyles.tsx
│   └── breakpoints.ts
│
├── assets/              # Static assets
│   ├── images/
│   ├── icons/
│   └── fonts/
│
├── App.tsx              # Root component
├── main.tsx             # Entry point
└── vite-env.d.ts        # Vite type declarations
```

---

## 🔧 Technical Decisions

### Why React?
- Component-based architecture
- Large ecosystem and community
- Excellent TypeScript support
- Team expertise

### Why TypeScript?
- Type safety reduces bugs
- Better IDE support (autocomplete, refactoring)
- Self-documenting code
- Required for large-scale apps

### Why Vite?
- Fast HMR (Hot Module Replacement)
- Modern ESM-based build
- Better developer experience than Create React App
- Faster build times

### Why Redux Toolkit + React Query?
- **Redux Toolkit:** Global client state (auth, preferences)
- **React Query:** Server state with caching, automatic refetching
- **Separation of concerns:** Different tools for different state types

### Why Styled Components?
- Component-scoped styles (no global CSS conflicts)
- Dynamic styling with props
- TypeScript support
- Theme support for design system

### Why React Router v6?
- Declarative routing
- Nested routes support
- Code splitting integration
- Modern API (hooks-based)

---

## 🎨 Design System Integration

### Theme Structure

```typescript
// styles/theme.ts
export const theme = {
  colors: {
    primary: '#0052CC',
    secondary: '#6554C0',
    success: '#00875A',
    error: '#DE350B',
    warning: '#FF991F',
    neutral: {
      50: '#F4F5F7',
      100: '#EBECF0',
      // ... more shades
    }
  },
  typography: {
    fontFamily: 'Inter, sans-serif',
    fontSize: {
      xs: '0.75rem',
      sm: '0.875rem',
      base: '1rem',
      lg: '1.125rem',
      xl: '1.25rem',
      '2xl': '1.5rem',
    },
    fontWeight: {
      regular: 400,
      medium: 500,
      semibold: 600,
      bold: 700,
    }
  },
  spacing: {
    xs: '4px',
    sm: '8px',
    md: '16px',
    lg: '24px',
    xl: '32px',
    '2xl': '48px',
  },
  breakpoints: {
    mobile: '768px',
    tablet: '1024px',
    desktop: '1280px',
  }
};
```

---

## 🔐 Authentication Flow

```
1. User enters credentials
   ↓
2. POST /api/auth/login
   ↓
3. Server validates & returns JWT
   ↓
4. Frontend stores JWT in memory + refresh token in httpOnly cookie
   ↓
5. All API requests include JWT in Authorization header
   ↓
6. If JWT expired → auto-refresh using refresh token
   ↓
7. If refresh fails → redirect to login
```

**Token Storage:**
- **Access Token:** Memory only (Redux store)
- **Refresh Token:** HttpOnly cookie (secure)
- **Never** store tokens in localStorage (XSS risk)

---

## 📊 State Management Strategy

### Global State (Redux)
**Use for:**
- Authentication state
- User profile
- App-wide preferences
- Theme settings

**Example:**
```typescript
// authSlice.ts
const authSlice = createSlice({
  name: 'auth',
  initialState: { user: null, isAuthenticated: false },
  reducers: {
    setUser: (state, action) => {
      state.user = action.payload;
      state.isAuthenticated = true;
    },
    logout: (state) => {
      state.user = null;
      state.isAuthenticated = false;
    }
  }
});
```

### Server State (React Query)
**Use for:**
- API data fetching
- Caching API responses
- Background refetching
- Optimistic updates

**Example:**
```typescript
// useNavigation.ts
export function useNavigation() {
  return useQuery({
    queryKey: ['navigation'],
    queryFn: () => navigationApi.getMenuItems(),
    staleTime: 5 * 60 * 1000, // 5 minutes
  });
}
```

### Local State (useState)
**Use for:**
- Form inputs
- UI state (modals, dropdowns)
- Component-specific state

---

## ♿ Accessibility Architecture

### Principles
1. **Semantic HTML** - Use correct elements
2. **Keyboard Navigation** - All interactive elements accessible
3. **ARIA** - Only when semantic HTML insufficient
4. **Focus Management** - Logical focus order
5. **Color Contrast** - WCAG AA compliant

### Implementation

```typescript
// Example: Accessible Button
export function Button({ children, onClick, ...props }) {
  return (
    <button
      type="button"
      onClick={onClick}
      aria-label={props['aria-label']}
      {...props}
    >
      {children}
    </button>
  );
}
```

### Testing Strategy
- **Automated:** jest-axe in unit tests
- **Manual:** Keyboard navigation testing
- **Screen readers:** NVDA (Windows), VoiceOver (Mac)
- **Tools:** Lighthouse, axe DevTools

---

## ⚡ Performance Optimization

### Code Splitting
```typescript
// Lazy load routes
const DashboardPage = lazy(() => import('./pages/DashboardPage'));

<Route path="/dashboard" element={
  <Suspense fallback={<LoadingSpinner />}>
    <DashboardPage />
  </Suspense>
} />
```

### Image Optimization
- WebP format with fallbacks
- Lazy loading (Intersection Observer)
- Responsive images (srcset)
- CDN delivery

### Bundle Optimization
- Tree shaking (Vite)
- Minification and compression
- Vendor chunk splitting
- Dynamic imports for large libraries

### Caching Strategy
- **React Query:** 5-minute stale time for API data
- **Service Worker:** Cache static assets
- **CDN:** Edge caching for global users

---

## 🧪 Testing Architecture

### Testing Pyramid

```
        /\
       /E2E\       (~10% - Critical paths)
      /------\
     /Integration\ (~20% - Feature flows)
    /------------\
   /  Unit Tests  \ (~70% - Components, utils)
  /----------------\
```

### Test Types

1. **Unit Tests** (Jest + RTL)
   - Components
   - Hooks
   - Utilities
   - Services

2. **Integration Tests** (Jest + RTL)
   - Feature flows
   - API integration
   - State management

3. **E2E Tests** (Playwright)
   - Critical user paths
   - Cross-browser testing

4. **Accessibility Tests** (jest-axe)
   - Automated WCAG checks
   - Component-level

---

## 🚀 Deployment Architecture

### CI/CD Pipeline

```
1. Push to branch
   ↓
2. GitHub Actions triggered
   ↓
3. Run linting & tests
   ↓
4. Build production bundle
   ↓
5. Run E2E tests
   ↓
6. Deploy to environment:
   - develop → Staging
   - main → Production
   ↓
7. Smoke tests
   ↓
8. Notify team (Slack)
```

### Environments

| Environment | Branch | URL | Purpose |
|-------------|--------|-----|---------|
| **Development** | feature/* | localhost:3000 | Local development |
| **Staging** | develop | staging.portal.exxeta.de | Testing & QA |
| **Production** | main | portal.exxeta.de | Live application |

---

## 📈 Monitoring & Observability

### Metrics
- Page load performance (Lighthouse)
- Error rate (Sentry)
- API response times
- User engagement (Analytics)

### Error Tracking
- **Sentry** for error monitoring
- Source maps for production debugging
- User context attached to errors

### Analytics
- Google Analytics 4
- Custom events for key interactions
- Conversion funnel tracking

---

## 🔮 Future Considerations

### Planned Improvements
- Progressive Web App (PWA) support
- Offline mode with Service Workers
- Server-Side Rendering (SSR) with Next.js
- Micro-frontend architecture (if needed)

### Scalability
- Component library extraction
- Monorepo setup (if multiple frontends)
- GraphQL migration (if complex data needs)

---

## 📞 Questions?

**Architecture Lead:** Max Müller (max.mueller@exxeta.de)  
**Slack:** #project-portal-redesign

---

**Last Updated:** January 28, 2025  
**Version:** 1.0

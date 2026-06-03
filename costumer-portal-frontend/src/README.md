# Source Directory (`src/`)

This directory contains the main source code of the Customer Portal frontend application.

## 📁 Directory Structure

- **`components/`**: Reusable UI components. They are modular and co-located with their styles, tests, and documentation.
- **`pages/`**: Page-level components, which represent different routes of the application.
- **`layouts/`**: Layout containers that wrap page components (e.g., `MainLayout` or `AuthLayout`).
- **`hooks/`**: Custom, reusable React hooks for business logic and side effects.
- **`services/`**: API layer, authentication services, and storage wrappers.
- **`store/`**: Redux state management configuration, including slices and typed hooks.
- **`styles/`**: Global theme configuration, design tokens, and breakpoints.
- **`utils/`**: Shared utility and helper functions.
- **`types/`**: Global TypeScript definitions and interfaces.
- **`assets/`**: Static media files (images, icons, fonts).

---

## 🛠️ Code Conventions

1. **PascalCase** for component folders and files: `Button.tsx`.
2. **camelCase** for helper functions, utilities, and custom hooks: `useAuth.ts`.
3. Co-locate tests and stories with their respective components.

# Customer Portal - Frontend

Modern, accessible, and performant customer portal built with React and TypeScript.

[![Build Status](https://github.com/exxeta/customer-portal-frontend/workflows/CI/badge.svg)](https://github.com/exxeta/customer-portal-frontend/actions)
[![Code Coverage](https://codecov.io/gh/exxeta/customer-portal-frontend/branch/main/graph/badge.svg)](https://codecov.io/gh/exxeta/customer-portal-frontend)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## 🎯 Project Overview

This repository contains the frontend application for the **Customer Portal Redesign** project (Project Key: **PORT** in Jira).

**Project Goals:**
- 🎨 Modern, intuitive user interface
- ⚡ Performance optimized (<2s page load)
- ♿ WCAG 2.1 AA accessibility compliance
- 📱 Mobile-first responsive design
- 🔐 Secure authentication (OAuth 2.0 + MFA)

**Project Links:**
- 📋 [Jira Board](https://exxeta.atlassian.net/browse/PORT)
- 📚 [Confluence Documentation](https://exxeta.atlassian.net/wiki/spaces/PORT)
- 🎨 [Figma Designs](https://figma.com/customer-portal)
- 🚀 [Staging Environment](https://staging.customer-portal.exxeta.de)

---

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ LTS
- npm 9+ or yarn 1.22+
- Git

### Installation

```bash
# Clone the repository
git clone https://github.com/exxeta/customer-portal-frontend.git
cd customer-portal-frontend

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env

# Start development server
npm run dev
```

The app will be available at `http://localhost:3000`

---

## 📁 Project Structure

```
src/
├── components/          # Reusable UI components
│   ├── Navigation/      # Navigation component (PORT-2)
│   ├── Dashboard/       # Dashboard widgets (PORT-9)
│   └── common/          # Shared components
├── pages/               # Page components (routes)
├── hooks/               # Custom React hooks
├── services/            # API services
├── store/               # Redux store
├── styles/              # Global styles and theme
├── utils/               # Utility functions
└── types/               # TypeScript type definitions
```

---

## 🛠️ Tech Stack

### Core
- **React** 18.2 - UI library
- **TypeScript** 5.0 - Type safety
- **Vite** 4.3 - Build tool

### State Management
- **Redux Toolkit** 1.9 - State management
- **React Query** 4.29 - Server state & caching

### Routing
- **React Router** 6.11 - Client-side routing

### Styling
- **Styled Components** 6.0 - CSS-in-JS
- **Tailwind CSS** 3.3 (optional utility classes)

### UI Components
- **react-grid-layout** 1.4 - Dashboard drag-and-drop
- **Recharts** 2.5 - Data visualization

### Testing
- **Jest** 29 - Unit testing
- **React Testing Library** 14 - Component testing
- **Playwright** 1.35 - E2E testing
- **jest-axe** 7.0 - Accessibility testing

### Code Quality
- **ESLint** 8.42 - Linting
- **Prettier** 2.8 - Code formatting
- **Husky** 8.0 - Git hooks
- **lint-staged** 13.2 - Pre-commit checks

---

## 📜 Available Scripts

### Development
```bash
npm run dev          # Start development server (port 3000)
npm run dev:api      # Start dev server with API proxy
```

### Build
```bash
npm run build        # Production build
npm run preview      # Preview production build locally
```

### Testing
```bash
npm run test         # Run unit tests
npm run test:watch   # Run tests in watch mode
npm run test:coverage # Run tests with coverage report
npm run test:e2e     # Run E2E tests (Playwright)
```

### Code Quality
```bash
npm run lint         # Run ESLint
npm run lint:fix     # Fix ESLint issues
npm run format       # Format code with Prettier
npm run type-check   # TypeScript type checking
```

---

## 🌿 Branch Strategy

We follow **GitFlow** workflow:

- `main` - Production-ready code
- `develop` - Integration branch for features
- `feature/*` - Feature branches (e.g., `feature/PORT-2-navigation`)
- `bugfix/*` - Bug fix branches
- `hotfix/*` - Production hotfixes

### Branch Naming Convention

```
feature/PORT-<issue-number>-<short-description>
bugfix/PORT-<issue-number>-<short-description>
hotfix/PORT-<issue-number>-<short-description>

Examples:
feature/PORT-2-navigation-redesign
bugfix/PORT-45-mobile-menu-fix
```

---

## 🔄 Workflow

1. **Create branch** from `develop`
   ```bash
   git checkout develop
   git pull origin develop
   git checkout -b feature/PORT-2-navigation-redesign
   ```

2. **Develop & commit**
   ```bash
   git add .
   git commit -m "feat(navigation): implement desktop navigation component (PORT-2)"
   ```

3. **Push & create PR**
   ```bash
   git push origin feature/PORT-2-navigation-redesign
   # Create Pull Request on GitHub
   ```

4. **Code review & merge**
   - At least 1 approval required
   - All CI checks must pass
   - Branch up-to-date with `develop`

---

## 📝 Commit Message Convention

We follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <subject> (<jira-issue>)

Types:
- feat:     New feature
- fix:      Bug fix
- docs:     Documentation changes
- style:    Code style changes (formatting, etc.)
- refactor: Code refactoring
- test:     Adding or updating tests
- chore:    Build process or tooling changes

Examples:
feat(navigation): add mobile hamburger menu (PORT-5)
fix(dashboard): resolve widget drag-and-drop issue (PORT-11)
docs(readme): update setup instructions
test(navigation): add accessibility tests (PORT-6)
```

---

## 🧪 Testing Guidelines

### Unit Tests
- **Coverage target:** >80%
- Test file naming: `*.test.tsx` or `*.spec.tsx`
- Location: Co-located with source files

```typescript
// Example: Navigation.test.tsx
describe('Navigation Component', () => {
  it('renders navigation items', () => {
    // Test implementation
  });
});
```

### E2E Tests
- Located in `e2e/` directory
- Cover critical user paths
- Run before each release

### Accessibility Tests
- Use `jest-axe` for automated checks
- Manual testing with screen readers
- Target: WCAG 2.1 AA compliance

---

## ♿ Accessibility

This project aims for **WCAG 2.1 Level AA** compliance.

**Key practices:**
- ✅ Semantic HTML5 elements
- ✅ ARIA labels where needed
- ✅ Keyboard navigation support
- ✅ Color contrast ratio >4.5:1
- ✅ Focus visible indicators
- ✅ Screen reader tested

**Tools:**
- [axe DevTools](https://www.deque.com/axe/devtools/)
- [Lighthouse](https://developers.google.com/web/tools/lighthouse)
- NVDA / VoiceOver screen readers

---

## 🔐 Environment Variables

Create a `.env` file in the root directory:

```bash
# API Configuration
VITE_API_BASE_URL=http://localhost:3001
VITE_API_TIMEOUT=10000

# Authentication
VITE_AUTH_DOMAIN=auth.customer-portal.exxeta.de
VITE_AUTH_CLIENT_ID=your_client_id

# Feature Flags
VITE_FEATURE_DASHBOARD_WIDGETS=true
VITE_FEATURE_MFA=false

# Analytics
VITE_GA_TRACKING_ID=UA-XXXXXXXXX-X

# Environment
VITE_ENV=development
```

---

## 📦 Deployment

### Staging
Automatic deployment on push to `develop`:
```
https://staging.customer-portal.exxeta.de
```

### Production
Manual deployment from `main` branch:
```
https://customer-portal.exxeta.de
```

**CI/CD:** GitHub Actions (see `.github/workflows/`)

---

## 🐛 Bug Reports & Feature Requests

- 🐞 [Report a Bug](https://github.com/exxeta/customer-portal-frontend/issues/new?template=bug_report.md)
- 💡 [Request a Feature](https://github.com/exxeta/customer-portal-frontend/issues/new?template=feature_request.md)
- 📋 [View Jira Board](https://exxeta.atlassian.net/browse/PORT)

---

## 🤝 Contributing

We welcome contributions! Please read our [Contributing Guidelines](CONTRIBUTING.md).

**Steps:**
1. Check existing issues or create a new one
2. Fork the repository
3. Create your feature branch
4. Commit your changes (following commit conventions)
5. Push to your fork
6. Create a Pull Request

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👥 Team

**Project Lead:** Adrian Jäger ([@adrianjaeger](https://github.com/adrianjaeger))  
**Frontend Lead:** Max Müller ([@maxmueller](https://github.com/maxmueller))  
**Frontend Dev:** Lisa Becker ([@lisabecker](https://github.com/lisabecker))

**Slack:** #project-portal-redesign  
**Email:** portal-team@exxeta.de

---

## 📚 Documentation

- [Architecture Overview](docs/ARCHITECTURE.md)
- [Setup Guide](docs/SETUP.md)
- [API Documentation](https://api-docs.customer-portal.exxeta.de)
- [Design System](https://design-system.customer-portal.exxeta.de)

---

## 🙏 Acknowledgments

- Design by Maria Schmidt & Anna Weber
- Backend API by Thomas Schmidt
- QA by Sarah Hoffmann

---

**Last Updated:** January 28, 2025  
**Version:** 0.3.0 (Beta)

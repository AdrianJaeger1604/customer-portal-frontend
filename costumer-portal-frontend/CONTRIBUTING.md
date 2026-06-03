# Contributing to Customer Portal Frontend

Thank you for your interest in contributing! 🎉

---

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Pull Request Process](#pull-request-process)
- [Issue Reporting](#issue-reporting)

---

## 📜 Code of Conduct

We are committed to providing a welcoming and inclusive environment. Please be respectful and professional in all interactions.

**Expected Behavior:**
- ✅ Be respectful and considerate
- ✅ Welcome newcomers and help them get started
- ✅ Focus on constructive feedback
- ✅ Accept criticism gracefully

**Unacceptable Behavior:**
- ❌ Harassment or discriminatory language
- ❌ Personal attacks
- ❌ Publishing others' private information
- ❌ Other unprofessional conduct

---

## 🚀 Getting Started

### Prerequisites

1. **Node.js 18+** and **npm 9+**
2. **Git** installed and configured
3. **GitHub account** with SSH key setup

### Setup

```bash
# Fork the repository on GitHub

# Clone your fork
git clone git@github.com:YOUR_USERNAME/customer-portal-frontend.git
cd customer-portal-frontend

# Add upstream remote
git remote add upstream git@github.com:exxeta/customer-portal-frontend.git

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env

# Start development server
npm run dev
```

---

## 🔄 Development Workflow

### 1. Find or Create an Issue

- Check [existing issues](https://github.com/exxeta/customer-portal-frontend/issues)
- Create a new issue if needed
- Wait for approval/assignment before starting work

### 2. Create a Branch

Always branch from `develop`:

```bash
git checkout develop
git pull upstream develop
git checkout -b feature/PORT-XX-short-description
```

**Branch naming:**
- `feature/PORT-XX-description` - New features
- `bugfix/PORT-XX-description` - Bug fixes
- `docs/description` - Documentation only
- `refactor/description` - Code refactoring

### 3. Make Changes

- Write clean, readable code
- Follow coding standards (see below)
- Write/update tests
- Update documentation if needed

### 4. Commit Changes

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```bash
git add .
git commit -m "feat(navigation): add mobile menu (PORT-5)"
```

**Commit message format:**
```
<type>(<scope>): <description> (<jira-issue>)

Examples:
feat(navigation): implement desktop nav component (PORT-4)
fix(dashboard): resolve widget overlap issue (PORT-11)
docs(readme): update installation steps
test(navigation): add keyboard navigation tests (PORT-6)
refactor(api): simplify error handling
```

**Types:**
- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation
- `style` - Formatting, missing semicolons, etc.
- `refactor` - Code restructuring
- `test` - Adding tests
- `chore` - Build process, dependencies

### 5. Push & Create PR

```bash
git push origin feature/PORT-XX-short-description
```

Then create a Pull Request on GitHub.

---

## 💻 Coding Standards

### TypeScript

- ✅ **Use TypeScript** for all new code
- ✅ **Strict mode enabled** - no `any` types without justification
- ✅ **Type imports explicitly**

```typescript
// ✅ Good
import type { User } from './types';

// ❌ Avoid
import { User } from './types';
```

### React Components

- ✅ **Functional components** with hooks
- ✅ **Named exports** for components
- ✅ **Props interface** defined

```typescript
// ✅ Good
interface NavigationProps {
  items: MenuItem[];
  onItemClick: (id: string) => void;
}

export function Navigation({ items, onItemClick }: NavigationProps) {
  return <nav>{/* ... */}</nav>;
}

// ❌ Avoid default exports
export default Navigation;
```

### File Naming

- ✅ **PascalCase** for components: `Navigation.tsx`
- ✅ **camelCase** for utilities: `formatDate.ts`
- ✅ **Test files:** `Navigation.test.tsx`

### Code Style

- ✅ **ESLint** and **Prettier** configured - run before commit
- ✅ **2 spaces** for indentation
- ✅ **Single quotes** for strings
- ✅ **Semicolons** required
- ✅ **Max line length:** 100 characters

```bash
npm run lint:fix
npm run format
```

### Comments

- ✅ Explain **why**, not **what**
- ✅ Use JSDoc for public APIs
- ✅ Remove commented-out code

```typescript
// ✅ Good comment
// Using debounce to avoid excessive API calls during typing
const debouncedSearch = debounce(search, 300);

// ❌ Bad comment
// Set timeout to 300
const debouncedSearch = debounce(search, 300);
```

---

## 🧪 Testing Guidelines

### Requirements

- ✅ **Unit tests** for all components and utilities
- ✅ **Coverage >80%** for new code
- ✅ **Accessibility tests** with jest-axe
- ✅ **E2E tests** for critical user paths

### Writing Tests

**Component test example:**

```typescript
import { render, screen } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { Navigation } from './Navigation';

describe('Navigation', () => {
  it('renders navigation items', () => {
    const items = [{ id: '1', label: 'Home', path: '/' }];
    render(<Navigation items={items} onItemClick={jest.fn()} />);
    
    expect(screen.getByText('Home')).toBeInTheDocument();
  });

  it('calls onItemClick when item is clicked', async () => {
    const mockClick = jest.fn();
    const items = [{ id: '1', label: 'Home', path: '/' }];
    render(<Navigation items={items} onItemClick={mockClick} />);
    
    await userEvent.click(screen.getByText('Home'));
    
    expect(mockClick).toHaveBeenCalledWith('1');
  });
});
```

**Accessibility test example:**

```typescript
import { axe } from 'jest-axe';

it('has no accessibility violations', async () => {
  const { container } = render(<Navigation items={items} />);
  const results = await axe(container);
  
  expect(results).toHaveNoViolations();
});
```

### Run Tests

```bash
npm run test              # Run all tests
npm run test:watch        # Watch mode
npm run test:coverage     # With coverage report
npm run test:e2e          # E2E tests
```

---

## 🔍 Pull Request Process

### Before Creating PR

- [ ] Code follows style guidelines
- [ ] All tests pass locally
- [ ] New tests written for new code
- [ ] Documentation updated
- [ ] No console errors or warnings
- [ ] Accessibility tests pass
- [ ] Branch is up-to-date with `develop`

### PR Title Format

```
<type>: <description> (PORT-XX)

Examples:
feat: implement mobile navigation (PORT-5)
fix: resolve dashboard widget overlap (PORT-11)
docs: update contributing guidelines
```

### PR Description Template

When you create a PR, fill out the template:

```markdown
## Description
Brief description of changes

## Related Issue
Closes PORT-XX (link to Jira)

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests added/updated
- [ ] E2E tests added/updated
- [ ] Manual testing performed

## Screenshots (if applicable)
Add screenshots for UI changes

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Comments added for complex code
- [ ] Documentation updated
- [ ] No new warnings generated
- [ ] Tests pass locally
```

### Review Process

1. **Automated checks** must pass (CI/CD)
2. **At least 1 approval** required from team member
3. **No unresolved comments**
4. **Up-to-date** with target branch

### Merge Strategy

- **Squash and merge** for features
- **Rebase and merge** for small fixes
- Delete branch after merge

---

## 🐛 Issue Reporting

### Bug Reports

Use the [Bug Report Template](.github/ISSUE_TEMPLATE/bug_report.md)

**Include:**
- Clear title and description
- Steps to reproduce
- Expected vs actual behavior
- Screenshots/recordings
- Environment (browser, OS)
- Console errors

### Feature Requests

Use the [Feature Request Template](.github/ISSUE_TEMPLATE/feature_request.md)

**Include:**
- Clear problem statement
- Proposed solution
- Alternatives considered
- Additional context

---

## ❓ Questions?

- **Slack:** #project-portal-redesign
- **Email:** portal-team@exxeta.de
- **GitHub Discussions:** For general questions

---

## 🙏 Thank You!

Every contribution, no matter how small, is valuable. Thank you for helping make this project better! 🎉

---

**Last Updated:** January 28, 2025

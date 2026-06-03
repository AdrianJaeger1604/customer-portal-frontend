# Setup Guide

Complete guide to setting up the Customer Portal Frontend for local development.

---

## 📋 Prerequisites

### Required Software

1. **Node.js** 18.x LTS or higher
   - Download: https://nodejs.org/
   - Verify: `node --version` (should show v18.x.x or higher)

2. **npm** 9.x or higher (comes with Node.js)
   - Verify: `npm --version`

3. **Git**
   - Download: https://git-scm.com/
   - Verify: `git --version`

4. **Code Editor** (recommended: VS Code)
   - Download: https://code.visualstudio.com/

### Recommended VS Code Extensions

- ESLint
- Prettier
- TypeScript
- ES7+ React/Redux/React-Native snippets
- Auto Rename Tag
- Bracket Pair Colorizer

---

## 🚀 Installation

### 1. Clone the Repository

```bash
# Via SSH (recommended)
git clone git@github.com:exxeta/customer-portal-frontend.git

# Via HTTPS
git clone https://github.com/exxeta/customer-portal-frontend.git

# Navigate to project
cd customer-portal-frontend
```

### 2. Install Dependencies

```bash
npm install
```

This will install all required packages (~500MB, takes 2-3 minutes).

### 3. Environment Configuration

Create a `.env` file in the project root:

```bash
cp .env.example .env
```

Edit `.env` with your local settings:

```bash
# API Configuration
VITE_API_BASE_URL=http://localhost:3001
VITE_API_TIMEOUT=10000

# Authentication (get from team)
VITE_AUTH_DOMAIN=auth.customer-portal.exxeta.de
VITE_AUTH_CLIENT_ID=your_client_id_here

# Feature Flags
VITE_FEATURE_DASHBOARD_WIDGETS=true
VITE_FEATURE_MFA=false

# Analytics (optional for local dev)
VITE_GA_TRACKING_ID=

# Environment
VITE_ENV=development
```

**Note:** For `VITE_AUTH_CLIENT_ID`, ask a team member or check 1Password.

### 4. Start Development Server

```bash
npm run dev
```

The app will be available at: **http://localhost:3000**

You should see:
```
  VITE v4.3.9  ready in 1234 ms

  ➜  Local:   http://localhost:3000/
  ➜  Network: http://192.168.1.100:3000/
  ➜  press h to show help
```

---

## 🧪 Verify Installation

### Run Tests

```bash
npm run test
```

You should see all tests pass:
```
 PASS  src/components/Navigation/Navigation.test.tsx
 ✓ renders navigation items (45 ms)
 ✓ handles item click (23 ms)

Test Suites: 1 passed, 1 total
Tests:       2 passed, 2 total
```

### Run Linter

```bash
npm run lint
```

Should show: `✓ No ESLint warnings or errors`

### Type Check

```bash
npm run type-check
```

Should complete without errors.

---

## 🔧 Troubleshooting

### Problem: `npm install` fails

**Error:** `EACCES: permission denied`

**Solution:**
```bash
# Fix npm permissions
sudo chown -R $USER:$GROUP ~/.npm
sudo chown -R $USER:$GROUP ~/.config
```

---

### Problem: Port 3000 already in use

**Error:** `Port 3000 is already in use`

**Solution 1:** Kill the process using port 3000
```bash
# macOS/Linux
lsof -ti:3000 | xargs kill -9

# Windows
netstat -ano | findstr :3000
taskkill /PID <PID> /F
```

**Solution 2:** Use a different port
```bash
npm run dev -- --port 3001
```

---

### Problem: Module not found errors

**Error:** `Cannot find module 'react' or its corresponding type declarations`

**Solution:**
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm cache clean --force
npm install
```

---

### Problem: TypeScript errors

**Error:** Various TypeScript errors

**Solution:**
```bash
# Restart TypeScript server in VS Code
# CMD/CTRL + Shift + P → "TypeScript: Restart TS Server"

# Or rebuild TypeScript
npm run type-check
```

---

### Problem: Environment variables not working

**Symptom:** API calls fail, features not working

**Solution:**
1. Verify `.env` file exists in project root
2. All variables start with `VITE_` prefix
3. Restart dev server after changing `.env`
4. Check console for actual values:
   ```typescript
   console.log(import.meta.env.VITE_API_BASE_URL);
   ```

---

### Problem: Hot reload not working

**Solution:**
```bash
# Restart dev server
# Press Ctrl+C to stop, then npm run dev again

# Or clear Vite cache
rm -rf node_modules/.vite
npm run dev
```

---

## 🐳 Docker Setup (Optional)

If you prefer Docker:

```bash
# Build image
docker build -t customer-portal-frontend .

# Run container
docker run -p 3000:3000 customer-portal-frontend

# With environment variables
docker run -p 3000:3000 \
  -e VITE_API_BASE_URL=http://localhost:3001 \
  customer-portal-frontend
```

---

## 🔗 Backend API Setup

The frontend requires the backend API to be running.

### Option 1: Use Staging API (Recommended for Frontend Development)

Already configured if you used `.env.example`:
```bash
VITE_API_BASE_URL=https://api-staging.customer-portal.exxeta.de
```

### Option 2: Run Backend Locally

If you need to develop backend features:

```bash
# Clone backend repo
git clone git@github.com:exxeta/customer-portal-backend.git
cd customer-portal-backend

# Follow backend setup instructions
# (see backend README.md)

# Start backend (usually port 3001)
npm run dev
```

Then update frontend `.env`:
```bash
VITE_API_BASE_URL=http://localhost:3001
```

---

## 📚 Additional Tools

### Recommended Browser Extensions

- **React Developer Tools**
  - Chrome: [Install](https://chrome.google.com/webstore/detail/react-developer-tools)
  - Firefox: [Install](https://addons.mozilla.org/en-US/firefox/addon/react-devtools/)

- **Redux DevTools**
  - Chrome: [Install](https://chrome.google.com/webstore/detail/redux-devtools)

- **axe DevTools** (Accessibility)
  - Chrome: [Install](https://chrome.google.com/webstore/detail/axe-devtools-web-accessibility)

### Storybook (Component Library)

View components in isolation:

```bash
npm run storybook
```

Opens at: http://localhost:6006

---

## 🎨 Design Resources

- **Figma:** [Design Files](https://figma.com/customer-portal)
- **Design System:** [Documentation](https://design-system.customer-portal.exxeta.de)
- **Icons:** Material Icons or Heroicons

---

## 🔐 Authentication Setup

### Get Credentials

1. Ask team for Auth0/Keycloak credentials
2. Update `.env`:
   ```bash
   VITE_AUTH_DOMAIN=your-tenant.auth0.com
   VITE_AUTH_CLIENT_ID=abc123xyz
   ```

### Test Login

1. Start dev server
2. Navigate to http://localhost:3000/login
3. Use test credentials:
   - Email: `test@exxeta.de`
   - Password: `Test1234!`

---

## 📖 Next Steps

After setup:

1. **Read the docs:**
   - [Architecture Overview](ARCHITECTURE.md)
   - [Contributing Guidelines](../CONTRIBUTING.md)

2. **Explore the codebase:**
   ```bash
   code .  # Open in VS Code
   ```

3. **Check Jira for tasks:**
   - [Project Board](https://exxeta.atlassian.net/browse/PORT)

4. **Join communication channels:**
   - Slack: #project-portal-redesign
   - Weekly sync: Tuesdays 10:00 AM

5. **Run the test suite:**
   ```bash
   npm run test
   npm run test:e2e
   ```

---

## 🆘 Still Having Issues?

1. **Check Common Issues:** See troubleshooting section above
2. **Search GitHub Issues:** [Open Issues](https://github.com/exxeta/customer-portal-frontend/issues)
3. **Ask the Team:**
   - Slack: #project-portal-redesign
   - Email: portal-team@exxeta.de
4. **Create an Issue:** [New Issue](https://github.com/exxeta/customer-portal-frontend/issues/new)

---

## ✅ Setup Checklist

- [ ] Node.js 18+ installed
- [ ] Repository cloned
- [ ] Dependencies installed (`npm install`)
- [ ] `.env` file configured
- [ ] Dev server starts successfully
- [ ] Tests pass (`npm run test`)
- [ ] Linter passes (`npm run lint`)
- [ ] TypeScript compiles (`npm run type-check`)
- [ ] Can access http://localhost:3000
- [ ] Backend API accessible
- [ ] Auth credentials configured
- [ ] VS Code extensions installed
- [ ] Joined Slack channel

---

**Need help?** Contact Max Müller (max.mueller@exxeta.de)

**Last Updated:** January 28, 2025

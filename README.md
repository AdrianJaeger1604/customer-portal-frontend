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

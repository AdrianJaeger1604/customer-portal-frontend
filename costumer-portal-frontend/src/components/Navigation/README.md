# Navigation Component

Responsive navigation component for the Customer Portal.

**Jira Epic:** PORT-1 (User Experience Modernization)  
**Jira Feature:** PORT-2 (Navigation Redesign)  
**Related Issues:** PORT-3, PORT-4, PORT-5, PORT-6, PORT-7, PORT-8

---

## 📋 Overview

The Navigation component provides a responsive, accessible navigation experience for both desktop and mobile users.

**Features:**
- ✅ Responsive (mobile, tablet, desktop)
- ✅ Dropdown menus for nested items
- ✅ Keyboard navigation support
- ✅ Screen reader accessible (WCAG 2.1 AA)
- ✅ Active route highlighting
- ✅ Smooth animations
- ✅ Mobile hamburger menu

---

## 🎨 Design

**Figma:** [Navigation Designs](https://figma.com/navigation-redesign)  
**Design Review:** Approved on 2025-01-20

### Breakpoints
- **Mobile:** < 768px (hamburger menu)
- **Tablet:** 768px - 1024px (horizontal nav, compact)
- **Desktop:** > 1024px (horizontal nav, full)

---

## 🚀 Usage

### Basic Usage

```tsx
import { Navigation } from '@/components/Navigation';

function App() {
  const menuItems = [
    {
      id: 'dashboard',
      label: 'Dashboard',
      path: '/dashboard',
      icon: 'dashboard'
    },
    {
      id: 'orders',
      label: 'Orders',
      path: '/orders',
      icon: 'shopping_cart',
      children: [
        { id: 'orders-history', label: 'Order History', path: '/orders/history' },
        { id: 'orders-new', label: 'New Order', path: '/orders/new' }
      ]
    }
  ];

  return (
    <Navigation items={menuItems} />
  );
}
```

### Props

| Prop | Type | Required | Description |
|------|------|----------|-------------|
| `items` | `MenuItem[]` | Yes | List of menu items to display |
| `onItemClick` | `(id: string) => void` | No | Callback function triggered when an item is clicked |

---

## ♿ Accessibility

The Navigation component is designed to be fully accessible:
- **ARIA Roles:** Uses `role="navigation"`, `role="menubar"`, `role="menu"`, and `role="menuitem"`.
- **Keyboard support:** Arrow keys to navigate menu items, Escape key to close dropdowns, Space/Enter to activate.
- **Focus visible:** Highly visible focus indicators for all interactive elements.

---

## 🧪 Testing

Run component-specific tests with:

```bash
npm run test -- src/components/Navigation
```

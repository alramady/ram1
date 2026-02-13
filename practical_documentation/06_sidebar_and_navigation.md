# 6. الشريط الجانبي والتنقل

يوثق هذا المستند هيكل الشريط الجانبي ونظام التنقل في المنصة.

## 6.1. هيكل الشريط الجانبي

الشريط الجانبي ثابت على الجانب الأيمن (RTL) ويحتوي على الأقسام التالية:

```
├── الأساسية (3)
│   ├── الرئيسية
│   ├── المؤشرات القيادية
│   └── تنفيذ الفحص
│
├── الرصد والفحص (4)
│   └── [صفحات فرعية]
│
├── الإدارة والنظام (29) [4 شارة]
│   └── [صفحات فرعية]
│
├── التصميم والتوثيق (3)
│   └── [صفحات فرعية]
│
├── شاشات المصادقة (3)
│   └── [صفحات فرعية]
│
└── الدعم (2)
    └── [صفحات فرعية]
```

## 6.2. أصناف CSS للشريط الجانبي

```css
/* الحاوية الرئيسية */
aside.fixed.right-0.top-0.h-screen.z-50.flex.flex-col.overflow-hidden

/* خلفية الشريط */
--sidebar: #080e1e;
--sidebar-bg: #f5f7fc;
--sidebar-foreground: #e8eaf0;
--sidebar-primary: #3db1ac;
--sidebar-primary-foreground: #fff;
--sidebar-accent: #3db1ac1a;
--sidebar-accent-foreground: #e8eaf0;
--sidebar-border: #3db1ac0f;
--sidebar-ring: #3db1ac;
```

## 6.3. معلومات المستخدم

يظهر في أسفل الشريط الجانبي:
- **الاسم**: مسؤول النظام
- **البريد**: admin@rasid.sa
- **الأيقونة**: دائرة خضراء تدل على الاتصال

## 6.4. شريط البحث السريع

```jsx
<input placeholder="بحث سريع..." type="text" />
```

## 6.5. نظام التوجيه (Routing)

```javascript
const routes = [
  { path: "/",          component: HomePage },
  { path: "/login",     component: LoginPage },
  { path: "/register",  component: RegisterPage },
  { path: "/dashboard", component: DashboardPage },
  { path: "/scan",      component: ScanExecution },
  { path: "/settings",  component: SettingsPage },
  { path: "/users",     component: UserManagement },
  { path: "/reports",   component: ReportsPage },
  { path: "/kpi",       component: KPIPage },
  { path: "/notifications", component: NotificationsPage },
  { path: "/profile",   component: ProfileSettings }
]
```

# 8. المكتبات والاعتماديات

يوثق هذا المستند جميع المكتبات والأدوات المستخدمة في المشروع، مستخرجة من الكود المجمّع.

## 8.1. المكتبات الأساسية

| المكتبة | الاستخدام |
| :--- | :--- |
| **React** | إطار عمل واجهة المستخدم الأساسي |
| **React DOM** | عرض مكونات React في المتصفح |
| **React Router** | نظام التوجيه بين الصفحات |
| **TypeScript** | لغة البرمجة (مع أنواع البيانات) |
| **Vite** | أداة البناء والتطوير |

## 8.2. مكتبات واجهة المستخدم

| المكتبة | الاستخدام |
| :--- | :--- |
| **TailwindCSS v4** | إطار عمل CSS للتنسيق |
| **Framer Motion** | مكتبة الرسوم المتحركة والحركات |
| **Radix UI** | مكونات واجهة مستخدم أساسية (Accordion, Dialog, Tooltip, etc.) |
| **Lucide React** | مكتبة الأيقونات |
| **Recharts** | مكتبة الرسوم البيانية |
| **Sonner** | مكتبة الإشعارات المنبثقة (Toast) |

## 8.3. مكتبات مساعدة

| المكتبة | الاستخدام |
| :--- | :--- |
| **clsx / class-variance-authority** | دمج أصناف CSS بشكل شرطي |
| **tailwind-merge** | دمج أصناف TailwindCSS بذكاء |
| **date-fns** | معالجة التواريخ |

## 8.4. الخطوط

| الخط | الاستخدام |
| :--- | :--- |
| **Tajawal** | الخط العربي الأساسي للواجهة |
| **IBM Plex Sans Arabic** | خط عربي بديل |

## 8.5. هيكل الملفات المصدرية

تم استخراج مسارات الملفات الأصلية من سمات `data-loc` في الكود المجمّع:

```
client/
├── src/
│   ├── pages/
│   │   ├── DashboardPage.tsx
│   │   ├── LoginPage.tsx
│   │   ├── RegisterPage.tsx
│   │   ├── ScanExecution.tsx
│   │   ├── SettingsPage.tsx
│   │   ├── UserManagement.tsx
│   │   ├── ReportsPage.tsx
│   │   ├── KPIPage.tsx
│   │   ├── NotificationsPage.tsx
│   │   ├── ProfileSettings.tsx
│   │   └── HomePage.tsx
│   ├── components/
│   │   └── ui/
│   │       ├── button.tsx
│   │       ├── card.tsx
│   │       ├── input.tsx
│   │       ├── dialog.tsx
│   │       ├── tooltip.tsx
│   │       ├── accordion.tsx
│   │       └── ...
│   ├── composables/
│   │   └── useSoundEffects.ts
│   ├── App.tsx
│   └── main.tsx
├── index.html
└── vite.config.ts
```

## 8.6. ملفات الأصول المجمّعة

| الملف | الحجم | المحتوى |
| :--- | :--- | :--- |
| `index-BM-nVg_A.js` | 593,563 حرف | الحزمة الرئيسية (React, Router, Framer Motion, UI Components) |
| `ReportsPage-SDOxpP_2.js` | 473,704 حرف | صفحة التقارير (تتضمن Recharts كاملة) |
| `DashboardPage-CQ6WOYdy.js` | 41,254 حرف | لوحة المعلومات |
| `SettingsPage-egmktOzS.js` | 30,439 حرف | صفحة الإعدادات |
| `ScanExecution-DxUUMUUI.js` | 30,019 حرف | صفحة تنفيذ الفحص |
| `UserManagement-DQEEOCy6.js` | 28,050 حرف | إدارة المستخدمين |
| `ProfileSettings-B9Zyqo92.js` | 26,358 حرف | الملف الشخصي |
| `NotificationsPage-BO3NXSo5.js` | 21,017 حرف | الإشعارات |
| `KPIPage-DG2eCOyN.js` | 20,825 حرف | المؤشرات القيادية |
| `RegisterPage-J1CfQXXI.js` | 16,660 حرف | صفحة التسجيل |
| `LoginPage-D_yL20eI.js` | 11,866 حرف | صفحة تسجيل الدخول |
| `HomePage-CpVPqNvY.js` | 13,804 حرف | الصفحة الرئيسية |
| `index-mhHfJFLK.css` | — | ملف الأنماط الرئيسي |

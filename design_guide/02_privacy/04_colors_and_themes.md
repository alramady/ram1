# دليل التصميم: منصة الخصوصية - نظام الألوان والسمات

## 4. Color System & Theming

تتميز منصة الخصوصية بنظام تصميم متطور يدعم الوضع الفاتح (Light Mode) والوضع الداكن (Dark Mode) بسلاسة، مع الحفاظ على هوية بصرية قوية ومتناسقة.

### فلسفة الألوان:

- **الوضع الفاتح:** يعتمد على خلفية بيضاء ناصعة (`#f7f9f9`) مع لون أساسي كحلي (`#273470`) ولون تمييز تركواز (`#3db1ac`). هذا المزيج يعطي إحساساً بالاحترافية والوضوح.
- **الوضع الداكن:** يستخدم خلفية كحلية داكنة (`#0d1529`) مع لون أساسي تركواز (`#3db1ac`) ولون ثانوي بنفسجي (`#6459a7`). يخلق هذا جواً من التركيز والراحة البصرية في البيئات المظلمة.

### متغيرات CSS الكاملة:

يتم التحكم في نظام الألوان بالكامل عبر متغيرات CSS، مما يسهل التعديل والصيانة.

#### الوضع الفاتح (`:root`)

```css
:root {
  --radius: 0.75rem;
  --background: #f7f9f9;
  --foreground: #1c2833;
  --card: #fff;
  --card-foreground: #1c2833;
  --primary: #273470; /* كحلي */
  --primary-foreground: #fff;
  --secondary: #6459a7; /* بنفسجي */
  --secondary-foreground: #fff;
  --muted: #f1f5f9;
  --muted-foreground: #1c283399;
  --accent: #3db1ac; /* تركواز */
  --accent-foreground: #fff;
  --destructive: #eb3d63; /* أحمر */
  --destructive-foreground: #fff;
  --border: #27347014;
  --input: #27347014;
  --ring: #273470;
  --chart-1: #3db1ac;
  --chart-2: #273470;
  --chart-3: #6459a7;
  --chart-4: #eb3d63;
  --chart-5: #ffc107;
  --sidebar: #ffffffd9;
  --sidebar-foreground: #1c2833;
  --sidebar-primary: #273470;
  --sidebar-primary-foreground: #fff;
  --sidebar-accent: #27347014;
  --sidebar-accent-foreground: #273470;
  --sidebar-border: #2734700f;
  --sidebar-ring: #273470;
  --sidebar-bg: #ffffffd9;
  --sidebar-bg-border: #2734700f;
  --sidebar-active: #27347014;
  --sidebar-hover: #2734700a;
}
```

#### الوضع الداكن (`.dark`)

```css
.dark {
  --background: #0d1529;
  --foreground: #e1def5;
  --card: #1a2550;
  --card-foreground: #e1def5;
  --primary: #3db1ac; /* تركواز */
  --primary-foreground: #fff;
  --secondary: #6459a7; /* بنفسجي */
  --secondary-foreground: #fff;
  --muted: #1a255080;
  --muted-foreground: #e1def580;
  --accent: #3db1ac;
  --accent-foreground: #fff;
  --destructive: #eb3d63;
  --destructive-foreground: #fff;
  --border: #3db1ac1f;
  --input: #3db1ac1f;
  --ring: #3db1ac;
  --chart-1: #3db1ac;
  --chart-2: #6459a7;
  --chart-3: #eb3d63;
  --chart-4: #ffc107;
  --chart-5: #273470;
  --sidebar: #0d1529f2;
  --sidebar-foreground: #e1def5;
  --sidebar-primary: #3db1ac;
  --sidebar-primary-foreground: #0d1529;
  --sidebar-accent: #3db1ac1f;
  --sidebar-accent-foreground: #e1def5;
  --sidebar-border: #3db1ac14;
  --sidebar-ring: #3db1ac;
  --sidebar-bg: #0d1529f2;
  --sidebar-bg-border: #3db1ac14;
  --sidebar-active: #3db1ac26;
  --sidebar-hover: #3db1ac14;
}
```

### تأثير الزجاج (Glassmorphism)

يتم استخدام تأثير الزجاج في الشريط الجانبي والبطاقات في الوضع الداكن لإضافة عمق وأناقة للتصميم.

```css
.dark .glass-card {
    background: #1a2550bf; /* 75% opacity */
    backdrop-filter: blur(12px);
    border: 1px solid #3db1ac1f;
}

.dark .sidebar {
    background: #0d1529f2; /* 95% opacity */
    backdrop-filter: blur(20px) saturate(1.5);
    border-right: 1px solid var(--sidebar-border);
}
```

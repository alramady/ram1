# 10. نظام الألوان والسمات

يوثق هذا المستند نظام الألوان الكامل للمنصة في الوضعين المظلم والفاتح.

## 10.1. الوضع المظلم (الافتراضي)

```css
:root {
  --background: #0b1120;
  --foreground: #e8eaf0;
  --card: #0f1730bf;
  --card-foreground: #e8eaf0;
  --popover: #111b36;
  --popover-foreground: #e8eaf0;
  --primary: #3db1ac;
  --primary-foreground: #fff;
  --secondary: #7c70ca;
  --secondary-foreground: #e8eaf0;
  --muted: #6459a724;
  --muted-foreground: #e8eaf08c;
  --accent: #2a3f7a;
  --accent-foreground: #e8eaf0;
  --destructive: #eb3d63;
  --destructive-foreground: #fff;
  --border: #3db1ac1a;
  --input: #3db1ac14;
  --ring: #3db1ac;
  --sidebar: #080e1e;
  --sidebar-foreground: #e8eaf0;
  --sidebar-primary: #3db1ac;
  --sidebar-primary-foreground: #fff;
  --sidebar-accent: #3db1ac1a;
  --sidebar-accent-foreground: #e8eaf0;
  --sidebar-border: #3db1ac0f;
  --sidebar-ring: #3db1ac;
}
```

## 10.2. الوضع الفاتح

```css
.light {
  --background: #f5f7fc;
  --foreground: #1a1f36;
  --card: #ffffffbf;
  --card-foreground: #1a1f36;
  --popover: #ffffff;
  --popover-foreground: #1a1f36;
  --primary: #273470;
  --primary-foreground: #fff;
  --secondary: #6459a7;
  --secondary-foreground: #fff;
  --muted: #273470 / 0.08;
  --muted-foreground: #1a1f36 / 0.55;
  --accent: #e8eaf0;
  --accent-foreground: #1a1f36;
  --destructive: #eb3d63;
  --destructive-foreground: #fff;
  --border: #273470 / 0.12;
  --input: #273470 / 0.06;
  --ring: #273470;
  --sidebar-bg: #f5f7fc;
  --sidebar: #ffffff;
  --sidebar-foreground: #1a1f36;
  --sidebar-primary: #273470;
  --sidebar-primary-foreground: #fff;
  --sidebar-accent: #273470 / 0.08;
  --sidebar-accent-foreground: #1a1f36;
  --sidebar-border: #273470 / 0.08;
  --sidebar-ring: #273470;
}
```

## 10.3. ألوان المخططات

```css
--chart-1: #3db1ac;   /* تركوازي - اللون الأساسي */
--chart-2: #7c70ca;   /* بنفسجي */
--chart-3: #6459a7;   /* بنفسجي داكن */
--chart-4: #4a7ab5;   /* أزرق */
--chart-5: #525e8c;   /* رمادي مزرق */
```

## 10.4. ألوان الحالات

| الحالة | اللون (Hex) | الاستخدام |
| :--- | :--- | :--- |
| نجاح / ممتثل | `#22C55E` | حالة الامتثال الكامل |
| تحذير / جزئي | `#FFC107` / `#D4A017` | امتثال جزئي أو تحذير |
| خطر / غير ممتثل | `#EB3D63` | عدم امتثال أو تهديد |
| معلومات | `#3B82F6` | معلومات عامة |
| أساسي داكن | `#1E3A5F` | اللون الأساسي الداكن |
| ثانوي | `#6459A7` | اللون الثانوي |

## 10.5. تأثيرات الزجاج حسب الوضع

### الوضع المظلم:
```css
--glass-bg: #0b1120b3;
--glass-border: #3db1ac1f;
--glass-shadow: 0 8px 32px #0006, 0 2px 8px #00000040, inset 0 1px 0 #ffffff0a;
--glass-hover-bg: #0b1120d9;
--glass-hover-border: #3db1ac38;
--glass-hover-shadow: 0 16px 56px #00000080, 0 4px 16px #3db1ac14, inset 0 1px 0 #ffffff0f;
--glow-color: #3db1ac4d;
--glow-strong: #3db1ac8c;
--particle-color: #3db1ac1f;
--scan-color: #3db1ac0d;
```

### الوضع الفاتح:
```css
--glass-bg: #ffffffb3;
--glass-border: #2734701a;
--glass-shadow: 0 8px 32px #0000000d, 0 2px 8px #00000008, inset 0 1px 0 #ffffff80;
--glass-hover-bg: #ffffffd9;
--glass-hover-border: #27347033;
--glass-hover-shadow: 0 16px 56px #00000014, 0 4px 16px #2734700a, inset 0 1px 0 #ffffffb3;
--glow-color: #2734701a;
--glow-strong: #27347033;
--particle-color: #2734700d;
--scan-color: #27347008;
```

## 10.6. ظلال البطاقات

```css
--card-shadow: 0 4px 12px #00000059, 0 8px 28px #0003, inset 0 1px 0 #ffffff08;
--card-hover-shadow: 0 12px 40px #00000073, 0 4px 16px #3db1ac14, inset 0 1px 0 #ffffff0d;
--card-active-shadow: 0 2px 8px #0006;
```

# 1. المؤثرات البصرية والرسوم المتحركة

هذا المستند يوثق جميع المؤثرات البصرية الأساسية، متغيرات التصميم، والحركات المستخدمة في منصة راصد. تم استخراج هذه الأصول مباشرة من الكود المصدري المجمّع والأنماط المحسوبة في المتصفح.

## 1.1. الحركات الأساسية (Keyframes)

تم تعريف 31 حركة `@keyframes` أساسية لتوفير مجموعة غنية من المؤثرات البصرية، من التوهجات والنبضات إلى حركات الدخول والخروج المعقدة.

```css
@keyframes pulse-glow {
  0%, 100% { filter: drop-shadow(0 0 8px var(--glow-color)); }
  50% { filter: drop-shadow(0 0 22px var(--glow-strong)); }
}

@keyframes orbit {
  0% { transform: rotate(0deg) translate(40px) rotate(0deg); }
  100% { transform: rotate(360deg) translate(40px) rotate(-360deg); }
}

@keyframes orbit-reverse {
  0% { transform: rotate(360deg) translate(55px) rotate(-360deg); }
  100% { transform: rotate(0deg) translate(55px) rotate(0deg); }
}

@keyframes gradient-shift {
  0% { background-position: 0% center; }
  50% { background-position: 100% center; }
  100% { background-position: 0% center; }
}

@keyframes scan-line {
  0% { transform: translateY(-100%); }
  100% { transform: translateY(100%); }
}

@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-8px); }
}

@keyframes shimmer {
  0% { background-position: -200% 0px; }
  100% { background-position: 200% 0px; }
}

@keyframes breathe {
  0%, 100% { opacity: 0.6; transform: scale(1); }
  50% { opacity: 1; transform: scale(1.02); }
}

@keyframes spin-slow {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

@keyframes ripple-out {
  0% { opacity: 0.5; transform: scale(1); }
  100% { opacity: 0; transform: scale(2.5); }
}

@keyframes data-flow {
  0% { opacity: 0; transform: translate(-100%); }
  20% { opacity: 1; }
  80% { opacity: 1; }
  100% { opacity: 0; transform: translate(100%); }
}

@keyframes border-glow {
  0%, 100% { border-color: var(--glass-border); box-shadow: rgba(0, 0, 0, 0) 0px 0px; }
  50% { border-color: var(--glow-strong); box-shadow: 0 0 20px var(--glow-color); }
}

@keyframes text-glow {
  0%, 100% { text-shadow: rgba(0, 0, 0, 0) 0px 0px; }
  50% { text-shadow: 0 0 12px var(--glow-color); }
}

@keyframes slide-in-right {
  0% { opacity: 0; transform: translate(30px); }
  100% { opacity: 1; transform: translate(0px); }
}

@keyframes slide-in-up {
  0% { opacity: 0; transform: translateY(20px); }
  100% { opacity: 1; transform: translateY(0px); }
}

@keyframes counter-pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.15); }
}

@keyframes radar-sweep {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

@keyframes typing-cursor {
  0%, 100% { opacity: 1; }
  50% { opacity: 0; }
}

@keyframes glow-pulse {
  0%, 100% { box-shadow: 0 0 8px var(--glow-color),0 0 20px transparent; }
  50% { box-shadow: 0 0 14px var(--glow-color),0 0 35px var(--glow-color); }
}

@keyframes card-entrance {
  0% { opacity: 0; transform: translateY(16px) scale(0.97); }
  100% { opacity: 1; transform: translateY(0px) scale(1); }
}

@keyframes stat-count-up {
  0% { opacity: 0; transform: translateY(8px); }
  100% { opacity: 1; transform: translateY(0px); }
}

@keyframes icon-bounce {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-4px); }
}

@keyframes progress-fill {
  0% { width: 0px; }
}

@keyframes badge-pop {
  0% { transform: scale(0); }
  70% { transform: scale(1.15); }
  100% { transform: scale(1); }
}

@keyframes accent-line-glow {
  0%, 100% { opacity: 0.4; }
  50% { opacity: 1; }
}

@keyframes spin {
  100% { transform: rotate(360deg); }
}

@keyframes pulse {
  50% { opacity: 0.5; }
}

@keyframes enter {
  0% { opacity: var(--tw-enter-opacity,1); transform: translate3d(var(--tw-enter-translate-x,0),var(--tw-enter-translate-y,0),0)scale3d(var(--tw-enter-scale,1),var(--tw-enter-scale,1),var(--tw-enter-scale,1))rotate(var(--tw-enter-rotate,0)); filter: blur(var(--tw-enter-blur,0)); }
}

@keyframes exit {
  100% { opacity: var(--tw-exit-opacity,1); transform: translate3d(var(--tw-exit-translate-x,0),var(--tw-exit-translate-y,0),0)scale3d(var(--tw-exit-scale,1),var(--tw-exit-scale,1),var(--tw-exit-scale,1))rotate(var(--tw-exit-rotate,0)); filter: blur(var(--tw-exit-blur,0)); }
}

@keyframes accordion-down {
  0% { height: 0px; }
  100% { height: var(--radix-accordion-content-height,auto); }
}

@keyframes accordion-up {
  0% { height: var(--radix-accordion-content-height,auto); }
  100% { height: 0px; }
}
```

## 1.2. نظام التصميم (Design Tokens)

يتم التحكم في المظهر المرئي للمنصة عبر مجموعة من متغيرات CSS (Design Tokens) التي تحدد الألوان، نصف القطر، والظلال. هذا يسمح بتغيير المظهر بشكل مركزي ومتسق.

```css
/* Base Colors */
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

/* Chart Colors */
--chart-1: #3db1ac;
--chart-2: #7c70ca;
--chart-3: #6459a7;
--chart-4: #4a7ab5;
--chart-5: #525e8c;

/* Glassmorphism Effects */
--glass-bg: #0b1120b3;
--glass-border: #3db1ac1f;
--glass-shadow: 0 8px 32px #0006,0 2px 8px #00000040,inset 0 1px 0 #ffffff0a;
--glass-hover-bg: #0b1120d9;
--glass-hover-border: #3db1ac38;
--glass-hover-shadow: 0 16px 56px #00000080,0 4px 16px #3db1ac14,inset 0 1px 0 #ffffff0f;

/* Glow & Particle Effects */
--scan-color: #3db1ac0d;
--glow-color: #3db1ac4d;
--glow-strong: #3db1ac8c;
--particle-color: #3db1ac1f;

/* Card Shadows */
--card-shadow: 0 4px 12px #00000059,0 8px 28px #0003,inset 0 1px 0 #ffffff08;
--card-hover-shadow: 0 12px 40px #00000073,0 4px 16px #3db1ac14,inset 0 1px 0 #ffffff0d;
--card-active-shadow: 0 2px 8px #0006;

/* Sizing */
--radius: .625rem;
```

## 1.3. التدرجات اللونية (Gradients)

تُستخدم التدرجات اللونية لإضافة عمق وبعد للتصميم.

```css
linear-gradient(to right bottom in oklab, rgb(10, 14, 26) 0%, rgb(17, 24, 39) 50%, rgb(15, 23, 42) 100%)
linear-gradient(to right bottom, oklab(0.349385 0.00161625 -0.104522 / 0.8) 0%, oklab(0.249404 0.00372405 -0.051495 / 0.9) 100%)
radial-gradient(circle at 1px 1px, rgba(255, 255, 255, 0.15) 1px, rgba(0, 0, 0, 0) 0px)
radial-gradient(circle, rgba(30, 58, 95, 0.15) 0%, rgba(0, 0, 0, 0) 70%)
linear-gradient(135deg, rgb(30, 58, 95), rgb(100, 89, 167), rgb(30, 58, 95))
linear-gradient(135deg, rgba(30, 58, 95, 0.3), rgba(100, 89, 167, 0.3))
linear-gradient(135deg, rgb(39, 52, 112), rgb(30, 58, 95))
linear-gradient(90deg, rgba(0, 0, 0, 0), rgba(255, 255, 255, 0.15), rgba(0, 0, 0, 0))
```

## 1.4. الظلال (Box Shadows)

تُستخدم الظلال لرفع العناصر عن الخلفية وإعطاء إحساس بالارتفاع.

```css
rgba(30, 58, 95, 0.3) 0px 0px 9.83966px 0px
rgba(30, 58, 95, 0.15) 0px 0px 9.94296px 0px
rgba(39, 52, 112, 0.4) 0px 0px 11.5089px 0px
rgba(30, 58, 95, 0.8) 0px 0px 12px 0px
rgba(100, 89, 167, 0.8) 0px 0px 10px 0px
rgba(30, 58, 95, 0.6) 0px 0px 8px 0px
```

## 1.5. فلاتر الخلفية (Backdrop Filters)

يُستخدم فلتر `blur` لتحقيق تأثير الزجاج المصنفر (Glassmorphism) الشائع في التصميم.

```css
blur(24px)
```

## 1.6. الانتقالات (Transitions)

تُستخدم انتقالات CSS لتنعيم التغييرات في خصائص العناصر عند التفاعل معها.

```css
background-color 0.4s, color 0.4s
background-color 0.3s, border-color 0.3s, color 0.2s, box-shadow 0.3s
opacity 0.3s cubic-bezier(0.4, 0, 0.2, 1)
color 0.15s cubic-bezier(0.4, 0, 0.2, 1), background-color 0.15s cubic-bezier(0.4, 0, 0.2, 1), border-color 0.15s cubic-bezier(0.4, 0, 0.2, 1)
```

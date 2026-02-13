# 7. تأثير الزجاج المصنفر والجسيمات

يوثق هذا المستند تأثيرات Glassmorphism والجسيمات المتحركة المستخدمة في خلفية المنصة.

## 7.1. تأثير الزجاج المصنفر (Glassmorphism)

يُطبق على جميع البطاقات والنوافذ المنبثقة في المنصة.

### الكود المصدري:
```css
.glass-card {
  background: rgba(255, 255, 255, 0.7);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(39, 52, 112, 0.1);
  border-radius: 1rem;
}

.dark .glass-card {
  background: rgba(39, 52, 112, 0.25);
  border-color: rgba(30, 58, 95, 0.12);
}
```

### متغيرات CSS:
```css
--glass-bg: #0b1120b3;
--glass-border: #3db1ac1f;
--glass-shadow: 0 8px 32px #0006, 0 2px 8px #00000040, inset 0 1px 0 #ffffff0a;
--glass-hover-bg: #0b1120d9;
--glass-hover-border: #3db1ac38;
--glass-hover-shadow: 0 16px 56px #00000080, 0 4px 16px #3db1ac14, inset 0 1px 0 #ffffff0f;
```

## 7.2. الجسيمات المتحركة (Floating Particles)

تُستخدم جسيمات دائرية متحركة في خلفية الصفحات لإضافة عمق وحيوية.

### الهيكل:
```jsx
<div className="fixed inset-0 pointer-events-none overflow-hidden">
  {/* 15 جسيم دائري متحرك */}
  <div className="absolute rounded-full" />
  <div className="absolute rounded-full" />
  <div className="absolute rounded-full" />
  {/* ... */}
</div>
```

### خصائص الجسيمات:
- **الشكل**: دوائر (`rounded-full`)
- **الموضع**: عشوائي (`absolute`)
- **اللون**: `--particle-color: #3db1ac1f`
- **الحركة**: تطفو ببطء باستخدام حركة `float`
- **التفاعل**: `pointer-events-none` لعدم التأثير على التفاعل

### مؤثرات الجسيمات:
```css
@keyframes float {
  0%, 100% { transform: translateY(0px); }
  50% { transform: translateY(-8px); }
}

@keyframes breathe {
  0%, 100% { opacity: 0.6; transform: scale(1); }
  50% { opacity: 1; transform: scale(1.02); }
}
```

## 7.3. نمط النقاط (Dot Pattern)

يُستخدم نمط نقاط خفيف في الخلفية لإضافة نسيج بصري.

```css
radial-gradient(circle at 1px 1px, rgba(255, 255, 255, 0.15) 1px, rgba(0, 0, 0, 0) 0px)
```

## 7.4. تأثير خط الفحص (Scan Line)

خط أفقي يتحرك من الأعلى للأسفل لإعطاء إحساس بالمسح الضوئي.

```css
@keyframes scan-line {
  0% { transform: translateY(-100%); }
  100% { transform: translateY(100%); }
}

/* اللون */
--scan-color: #3db1ac0d;
```

## 7.5. تأثير التوهج (Glow Effects)

تُستخدم تأثيرات التوهج على الحدود والنصوص والأيقونات.

```css
/* توهج الحدود */
@keyframes border-glow {
  0%, 100% { border-color: var(--glass-border); box-shadow: rgba(0,0,0,0) 0px 0px; }
  50% { border-color: var(--glow-strong); box-shadow: 0 0 20px var(--glow-color); }
}

/* توهج النص */
@keyframes text-glow {
  0%, 100% { text-shadow: rgba(0,0,0,0) 0px 0px; }
  50% { text-shadow: 0 0 12px var(--glow-color); }
}

/* نبض التوهج */
@keyframes pulse-glow {
  0%, 100% { filter: drop-shadow(0 0 8px var(--glow-color)); }
  50% { filter: drop-shadow(0 0 22px var(--glow-strong)); }
}

/* توهج صندوقي */
@keyframes glow-pulse {
  0%, 100% { box-shadow: 0 0 8px var(--glow-color), 0 0 20px transparent; }
  50% { box-shadow: 0 0 14px var(--glow-color), 0 0 35px var(--glow-color); }
}
```

## 7.6. تأثير المدار (Orbit)

حركة دائرية تُستخدم في عناصر الخلفية.

```css
@keyframes orbit {
  0% { transform: rotate(0deg) translate(40px) rotate(0deg); }
  100% { transform: rotate(360deg) translate(40px) rotate(-360deg); }
}

@keyframes orbit-reverse {
  0% { transform: rotate(360deg) translate(55px) rotate(-360deg); }
  100% { transform: rotate(0deg) translate(55px) rotate(0deg); }
}
```

## 7.7. تأثير الوميض (Shimmer)

يُستخدم في أشرطة التقدم وعناصر التحميل.

```css
@keyframes shimmer {
  0% { background-position: -200% 0px; }
  100% { background-position: 200% 0px; }
}

/* التطبيق */
.shimmer-effect {
  position: absolute;
  inset: 0;
  background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
  animation: shimmer 1.5s linear infinite;
}
```

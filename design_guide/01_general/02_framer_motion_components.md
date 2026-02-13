# 2. مكونات الحركة (Framer Motion)

تعتمد المنصة بشكل كبير على مكتبة `Framer Motion` لإنشاء حركات معقدة وتفاعلية. هذا المستند يوثق الأنماط الشائعة وخصائص الحركة المستخدمة في مختلف المكونات.

## 2.1. خصائص الحركة (Animation Props)

فيما يلي عينات من كائنات `initial`, `animate`, `exit`, `transition` التي تحدد سلوك الحركة للمكونات. تم استخراجها من ملفات JavaScript المجمعة.

### DashboardPage-CQ6WOYdy.js

```javascript
// دخول البطاقات مع تأخير متتالي
initial: {opacity:0, y:20}
animate: {opacity:1, y:0}
transition: {delay: .2 + p * .1, duration: .5}

// تأثير التوهج عند المرور
whileHover: {y:-5, boxShadow: r ? `0 15px 40px rgba(0, 0, 0, 0.4), 0 0 30px ${c.gradient[0]}` : `0 15px 40px rgba(0, 0, 0, 0.2), 0 0 20px ${c.gradient[0]}`}

// حركة تعبئة شريط التقدم
animate: {width: `${S}%`}
transition: {duration: 1.5, delay: .5 + p * .15, ease: "easeOut"}

// حركة اهتزاز الأيقونة
whileHover: {rotate: [0, -10, 10, 0], scale: 1.15}
transition: {duration: .5}
```

### ScanExecution-DxUUMUUI.js

```javascript
// دوران أيقونة الفحص أثناء التشغيل
animate: {rotate: r ? [0, 360] : 0}
transition: {duration: 1, repeat: Infinity, ease: "linear"}

// تأثير وميض شريط التقدم
animate: {x: ["-100%", "100%"]}
transition: {duration: 1.5, repeat: Infinity, ease: "linear"}

// دخول مراحل الفحص
initial: {opacity: 0, x: -20}
animate: {opacity: 1, x: 0}
transition: {delay: .3 + i * .05}
```

### UserManagement-DQEEOCy6.js

```javascript
// دخول بطاقات المستخدمين
initial: {opacity: 0, y: 20}
animate: {opacity: 1, y: 0}
transition: {delay: t * .08}

// تأثير الظل عند المرور على بطاقة المستخدم
whileHover: {y: -3, boxShadow: `0 8px 25px ${s}`}

// حركة أيقونة الدرع
animate: {rotate: [0, 5, -5, 0]}
transition: {duration: 4, repeat: Infinity, delay: t * .4}
```

## 2.2. مكونات `motion`

تُستخدم مكونات `motion` (مثل `motion.div`, `motion.span`) لتطبيق هذه الحركات على عناصر DOM.

```jsx
// مثال من LoginPage-D_yL20eI.js
<motion.div
  initial={{ opacity: 0, y: 20 }}
  animate={{ opacity: 1, y: 0 }}
  transition={{ duration: 0.5, delay: 0.2 }}
  className="..."
>
  {/* ... محتوى ... */}
</motion.div>

// مثال من DashboardPage-CQ6WOYdy.js
<motion.div
  variants={cardVariants}
  initial="hidden"
  animate="visible"
  whileHover="hover"
  className="..."
>
  {/* ... محتوى البطاقة ... */}
</motion.div>
```

## 2.3. الأصناف الرئيسية (Key CSS Classes)

تُستخدم أصناف TailwindCSS بكثافة لتنسيق المكونات. فيما يلي بعض الأصناف الرئيسية التي تحدد هيكل وتخطيط الصفحات.

- **`min-h-screen relative`**: يضمن أن الصفحة تملأ الشاشة بأكملها وتعمل كحاوية للمكونات ذات التموضع المطلق.
- **`grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6`**: نظام شبكي متجاوب لترتيب البطاقات في لوحة المعلومات.
- **`glass-card`**: صنف مخصص لتطبيق تأثير الزجاج المصنفر (Glassmorphism).
- **`flex items-center justify-between`**: نمط Flexbox شائع لمحاذاة العناصر وتوزيعها.
- **`rounded-xl shadow-lg`**: يطبق زوايا دائرية وظل كبير على البطاقات.

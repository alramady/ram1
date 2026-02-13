# دليل التصميم: منصة PDPL - مكونات Framer Motion

## 2. Framer Motion Animations

تستخدم منصة PDPL مكتبة `Framer Motion` بكثافة لإنشاء واجهات ديناميكية وتفاعلية. تم استخراج **97 نمط حركة فريد**، مما يدل على اهتمام كبير بالتفاصيل الدقيقة للحركة.

### أنماط الحركة الرئيسية:

- **الدخول المتدرج (Staggered Entrance):** يتم تطبيق تأثير `staggerChildren` على الحاويات الرئيسية، مما يؤدي إلى ظهور العناصر الفرعية (مثل البطاقات أو عناصر القائمة) بشكل متتابع وجذاب.
- **الحركات الربيعية (Spring Physics):** تستخدم انتقالات من نوع `spring` (مثل `stiffness: 300, damping: 25`) لإعطاء الحركات إحساساً فيزيائياً وواقعياً، خاصة عند التفاعل مع العناصر.
- **تنوع حركات الدخول:** بدلاً من حركة دخول موحدة، تستخدم المنصة حركات متنوعة حسب السياق، مثل `fade-in-up`, `fade-in-left`, `scale-in`، مما يضفي تنوعاً بصرياً على التجربة.

### أمثلة على كود الحركة (Variants):

```javascript
// حركة دخول متدرجة للقوائم والشبكات
const containerVariants = {
  animate: {
    transition: { staggerChildren: 0.08, delayChildren: 0.1 }
  }
};

const itemVariants = {
  initial: { opacity: 0, y: 20, scale: 0.95 },
  animate: { opacity: 1, y: 0, scale: 1, transition: { type: "spring", stiffness: 250, damping: 30 } }
};

// حركة تفاعلية للأيقونات مع دوران
const iconVariants = {
  whileHover: { scale: 1.15, rotate: -8, transition: { type: "spring", stiffness: 400 } },
  whileTap: { scale: 0.9 }
};

// حركة ظهور الصفحات
const pageTransition = {
  initial: { opacity: 0, x: -50 },
  animate: { opacity: 1, x: 0 },
  exit: { opacity: 0, x: 50 },
  transition: { duration: 0.4, ease: "easeInOut" }
};
```

### تحليل تفصيلي للحركات:

| نوع الحركة | عدد الأنماط | الوصف |
| :--- | :--- | :--- |
| `initial` | 28 | تحديد الحالة الأولية للعنصر قبل بدء الحركة (غالباً `opacity:0`). |
| `animate` | 25 | تحديد الحالة النهائية للعنصر بعد اكتمال الحركة. |
| `transition` | 15 | التحكم في توقيت ونوع الحركة (e.g., `duration`, `ease`, `delay`, `type: 'spring'`). |
| `whileHover` | 12 | حركات تفاعلية عند مرور مؤشر الفأرة. |
| `exit` | 10 | تحديد حركة العنصر عند إزالته من الشاشة. |
| `variants` | 5 | تعريف مجموعة متكاملة من الحالات (`initial`, `animate`, `exit`) لمكون واحد. |
| `whileTap` | 2 | حركة تفاعلية عند النقر على العنصر. |

هذا الاستخدام المتقدم لـ `Framer Motion` يوضح نضج التصميم في منصة PDPL، حيث لا تقتصر الحركة على مجرد الجماليات، بل تساهم في توجيه المستخدم وتعزيز فهمه للتسلسل الهرمي للمعلومات.

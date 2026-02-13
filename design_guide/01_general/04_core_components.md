# 4. المكونات الأساسية

هذا المستند يوثق المكونات الرئيسية لواجهة المستخدم التي تشكل أساس منصة راصد، مع التركيز على هيكلها، أصنافها، والنصوص العربية المستخدمة.

## 4.1. بطاقات لوحة المعلومات (Dashboard Cards)

تعتبر البطاقات هي الوحدة الأساسية في لوحة المعلومات، وتستخدم لعرض مؤشرات الأداء الرئيسية (KPIs) ومجموعات الامتثال.

- **الهيكل**: تتكون كل بطاقة من `motion.div` لتطبيق حركات الدخول والتفاعل.
- **الأصناف**: تستخدم أصناف مثل `glass-card`, `rounded-xl`, `p-6`, `shadow-lg` لتحقيق المظهر الزجاجي والتنسيق.
- **المحتوى**: تحتوي على أيقونة، عنوان، قيمة المؤشر، ورسم بياني مصغر.

```jsx
// مثال مبسط لهيكل بطاقة KPI
<motion.div
  className="glass-card p-6 rounded-xl shadow-lg flex flex-col justify-between"
  variants={cardVariants}
  initial="hidden"
  animate="visible"
  whileHover="hover"
>
  <div className="flex items-center justify-between">
    <span className="text-lg font-bold">{title}</span>
    <Icon className="w-8 h-8" />
  </div>
  <div>
    <h3 className="text-4xl font-extrabold">{value}</h3>
    <p className="text-sm text-muted-foreground">{description}</p>
  </div>
  <div className="h-16 mt-4">
    <MiniLineChart data={chartData} />
  </div>
</motion.div>
```

## 4.2. شاشة تنفيذ الفحص (Scan Execution Screen)

هذه الشاشة هي مركز عملية الفحص وتتكون من عدة أجزاء تفاعلية.

- **رأس الصفحة**: يحتوي على أيقونة الدرع التي تدور أثناء الفحص (`animate-spin`) وشريط تقدم متحرك.
- **شريط التقدم**: يستخدم `motion.div` مع حركة `shimmer` لإعطاء إحساس بالنشاط.
- **سجل الفحص (Log Panel)**: يعرض سجلات الفحص في الوقت الفعلي مع تمرير تلقائي للأسفل.
- **مراحل الفحص**: تعرض قائمة بالبنود التي يتم فحصها مع أيقونات حالة (نجاح، فشل، قيد التنفيذ).

```jsx
// مثال من ScanExecution-DxUUMUUI.js
<div className="log-panel" ref={logRef}>
  <AnimatePresence>
    {logs.map(log => (
      <motion.div
        key={log.id}
        layout
        initial={{ opacity: 0, y: 20 }}
        animate={{ opacity: 1, y: 0 }}
        exit={{ opacity: 0, x: -20 }}
        className={`log-entry log-${log.type}`}
      >
        {/* ... محتوى السجل ... */}
      </motion.div>
    ))}
  </AnimatePresence>
</div>
```

## 4.3. النصوص العربية

تم استخراج جميع النصوص الثابتة من الكود، مما يؤكد أن الواجهة موجهة بالكامل للغة العربية. فيما يلي عينات من كل صفحة:

- **DashboardPage**: `"إجمالي المواقع المراقبة"`, `"نسبة الامتثال"`, `"التهديدات المكتشفة"`, `"رادار المراقبة"`, `"توزيع حالات الامتثال"`.
- **LoginPage**: `"تسجيل الدخول"`, `"أدخل اسم المستخدم"`, `"نسيت كلمة المرور؟"`, `"إنشاء حساب جديد"`.
- **ScanExecution**: `"محرك راصد للفحص المتقدم"`, `"في انتظار بدء الفحص"`, `"إحصائيات الفحص"`, `"المواقع المفحوصة"`.
- **SettingsPage**: `"الإعدادات العامة"`, `"الأمان"`, `"الإشعارات"`, `"التكاملات"`, `"تم حفظ الإعدادات بنجاح"`.
- **UserManagement**: `"إدارة المستخدمين"`, `"إضافة مستخدم جديد"`, `"مدير النظام"`, `"محلل"`, `"مشاهد"`.

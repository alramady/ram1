# دليل التصميم: منصة PDPL - الرسوم البيانية (Recharts)

## 3. Charts and Graphs

تعتبر الرسوم البيانية في منصة PDPL عنصراً محورياً لعرض مؤشرات رصد تسريبات البيانات. تستخدم المنصة مكتبة `Recharts` لتقديم تصورات غنية بالبيانات، تفاعلية، ومتكاملة مع التصميم العام.

### أنواع الرسوم البيانية المستخدمة:

- **AreaChart (مخطط مساحي):** هو النوع الأكثر استخداماً في لوحة القيادة لعرض الاتجاهات الزمنية (Trends) مثل "إجمالي حوادث التسريب" و "السجلات الشخصية المكشوفة". يتميز بتدرج لوني شفاف يضيف عمقاً للتصميم.
- **BarChart (مخطط أعمدة):** يستخدم للمقارنات الفئوية، مثل مقارنة أعداد الحوادث بين "القطاعات المتأثرة".
- **PieChart (مخطط دائري):** يستخدم في عرض "مصادر الرصد" (تليجرام، دارك ويب، إلخ) لإظهار النسب المئوية لكل مصدر بشكل واضح.
- **RadarChart (مخطط راداري):** موجود في صفحة "راصد الذكي" لمقارنة أبعاد متعددة للتهديدات أو الكيانات.

### التصميم والتفاعلية:

- **التصميم الزجاجي (Glassmorphism):** خلفيات الرسوم البيانية غالباً ما تكون شبه شفافة مع تأثير `backdrop-filter: blur()`، مما يجعلها تندمج بسلاسة مع الخلفيات المتحركة للمنصة.
- **الألوان الديناميكية:** يتم تحميل الألوان من متغيرات CSS (`var(--chart-1)`, `var(--chart-2)`, etc.)، مما يضمن تغيرها تلقائياً عند التبديل بين الوضع الفاتح والداكن.
- **التفاعلية عند المرور:** عند المرور فوق أي رسم بياني، تظهر خطوط وتلميحات (`Tooltip`) مخصصة تتناسب مع تصميم المنصة، وغالباً ما تكون بخلفية زجاجية أيضاً.
- **لا توجد محاور (No Axes):** تتميز معظم الرسوم البيانية في لوحة القيادة بإخفاء المحاور (XAxis, YAxis) والشبكة (CartesianGrid) للاحتفاظ بمظهر نظيف والتركيز على البيانات نفسها.

### مثال على كود رسم بياني (AreaChart):

```jsx
import { AreaChart, Area, Tooltip, ResponsiveContainer } from 'recharts';

const data = [
  { date: '2026-01', value: 33 },
  { date: '2026-02', value: 127 },
  // ...
];

const TrendChart = ({ data, colorVar }) => (
  <ResponsiveContainer width="100%" height="100%">
    <AreaChart data={data}>
      <defs>
        <linearGradient id={`color-${colorVar}`} x1="0" y1="0" x2="0" y2="1">
          <stop offset="5%" stopColor={`var(${colorVar})`} stopOpacity={0.4}/>
          <stop offset="95%" stopColor={`var(${colorVar})`} stopOpacity={0}/>
        </linearGradient>
      </defs>
      <Tooltip
        cursor={{ stroke: `var(${colorVar})`, strokeWidth: 1, strokeDasharray: '3 3' }}
        contentStyle={{ 
            background: 'rgba(13, 21, 41, 0.7)',
            backdropFilter: 'blur(10px)',
            border: '1px solid var(--border)',
            borderRadius: 'var(--radius)'
        }}
      />
      <Area 
        type="monotone" 
        dataKey="value" 
        stroke={`var(${colorVar})`} 
        strokeWidth={2}
        fillOpacity={1} 
        fill={`url(#color-${colorVar})`} 
      />
    </AreaChart>
  </ResponsiveContainer>
);
```

هذا المثال يوضح التقنيات المتقدمة المستخدمة، مثل تعريف تدرجات لونية (`linearGradient`) داخل `defs` وتطبيقها كخلفية للمساحة، بالإضافة إلى تخصيص شكل التلميح والمؤشر ليتناسب مع الهوية البصرية للمنصة.

# دليل التصميم: منصة الخصوصية - الرسوم البيانية (Recharts)

## 3. Charts and Graphs

تستخدم منصة الخصوصية مكتبة `Recharts` لعرض البيانات بشكل مرئي وجذاب. تتميز الرسوم البيانية بتصميم نظيف وتفاعلي، مع استخدام ألوان متناسقة مع هوية المنصة.

### أنواع الرسوم البيانية المستخدمة:

- **BarChart (مخطط أعمدة):** يستخدم لمقارنة القيم بين فئات مختلفة، مثل مقارنة نسب الامتثال بين القطاعات.
- **LineChart (مخطط خطي):** يستخدم لعرض التغير في البيانات عبر الزمن، مثل الاتجاه الزمني للامتثال.
- **AreaChart (مخطط مساحي):** مشابه للمخطط الخطي ولكنه يملأ المساحة تحت الخط، مما يبرز الحجم والتغير.
- **PieChart (مخطط دائري):** يستخدم لعرض النسب المئوية وتوزيع الفئات، مثل توزيع حالات الامتثال.
- **RadarChart (مخطط راداري):** يستخدم لمقارنة متغيرات متعددة، مثل مقارنة امتثال جهة معينة ببنود المادة 12.
- **RadialBarChart (مخطط دائري شعاعي):** يستخدم لعرض التقدم أو النسب بشكل دائري جذاب.

### التصميم والألوان:

تعتمد الرسوم البيانية على نظام ألوان محدد وموحد لضمان سهولة القراءة والاتساق البصري. يتم تعريف الألوان باستخدام متغيرات CSS.

```css
/* متغيرات ألوان الرسوم البيانية */
:root {
  --chart-1: #3db1ac; /* تركواز */
  --chart-2: #273470; /* كحلي */
  --chart-3: #6459a7; /* بنفسجي */
  --chart-4: #eb3d63; /* أحمر */
  --chart-5: #ffc107; /* أصفر */
}

.dark {
  --chart-1: #3db1ac;
  --chart-2: #6459a7;
  --chart-3: #eb3d63;
  --chart-4: #ffc107;
  --chart-5: #273470;
}
```

### مثال على كود رسم بياني (BarChart):

```jsx
import { BarChart, Bar, XAxis, YAxis, CartesianGrid, Tooltip, Legend, ResponsiveContainer } from 'recharts';

const data = [
  { name: 'القطاع الحكومي', 'ممتثل': 40, 'غير ممتثل': 24 },
  { name: 'القطاع الخاص', 'ممتثل': 30, 'غير ممتثل': 13 },
  // ... more data
];

const ComplianceBarChart = () => (
  <ResponsiveContainer width="100%" height={300}>
    <BarChart data={data} margin={{ top: 20, right: 30, left: 20, bottom: 5 }}>
      <CartesianGrid strokeDasharray="3 3" stroke="var(--border)" />
      <XAxis dataKey="name" stroke="var(--foreground)" />
      <YAxis stroke="var(--foreground)" />
      <Tooltip
        contentStyle={{
          backgroundColor: 'var(--card)',
          borderColor: 'var(--border)',
          color: 'var(--card-foreground)',
        }}
      />
      <Legend />
      <Bar dataKey="ممتثل" fill="var(--chart-1)" />
      <Bar dataKey="غير ممتثل" fill="var(--chart-4)" />
    </BarChart>
  </ResponsiveContainer>
);
```

### التفاعلية:

- **Tooltip (تلميح):** عند المرور على أي جزء من الرسم البياني، يظهر تلميح يعرض معلومات تفصيلية عن تلك النقطة.
- **Legend (مفتاح الخريطة):** يمكن النقر على عناصر المفتاح لإخفاء أو إظهار البيانات المرتبطة بها في الرسم البياني.
- **ResponsiveContainer:** جميع الرسوم البيانية موضوعة داخل هذا المكون لضمان استجابتها وتكيفها مع مختلف أحجام الشاشات.

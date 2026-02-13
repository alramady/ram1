# 3. الرسوم البيانية (Recharts)

تُستخدم مكتبة `Recharts` لعرض البيانات بشكل مرئي في لوحة المعلومات وصفحة التقارير. هذا المستند يوثق المكونات المستخدمة وأنواع البيانات.

## 3.1. أنواع المخططات المستخدمة

تم استخلاص الأنواع التالية من المخططات ومكوناتها من الكود المصدري لصفحة التقارير (`ReportsPage-SDOxpP_2.js`):

| المكون (Component) | عدد الاستخدامات |
| :--- | :--- |
| `Line` | 92 |
| `Tooltip` | 47 |
| `Bar` | 23 |
| `Area` | 13 |
| `Pie` | 7 |
| `Legend` | 6 |
| `Radar` | 4 |
| `LineChart` | 2 |
| `AreaChart` | 2 |
| `CartesianGrid` | 2 |
| `XAxis` | 2 |
| `YAxis` | 2 |
| `ScatterChart` | 2 |
| `BarChart` | 2 |
| `Scatter` | 2 |
| `ResponsiveContainer` | 1 |
| `Cell` | 1 |
| `ComposedChart` | 1 |
| `PieChart` | 1 |
| `RadarChart` | 1 |

## 3.2. مخططات لوحة المعلومات

تستخدم لوحة المعلومات مخططات خطية صغيرة داخل بطاقات مؤشرات الأداء الرئيسية ومخطط دائري لتوزيع حالات الامتثال.

### المخطط الخطي المصغر (Mini Line Chart)

- **الغرض**: عرض الاتجاه العام لمؤشر معين (مثل نسبة الامتثال) خلال فترة زمنية.
- **الكود**: يتم إنشاؤه باستخدام مكون `LineChart` مع إخفاء المحاور والشبكة.

```jsx
// مثال مبسط من DashboardPage-CQ6WOYdy.js
<ResponsiveContainer width="100%" height={60}>
  <LineChart data={chartData}>
    <defs>
      <linearGradient id="gradient-chart" x1="0" y1="0" x2="0" y2="1">
        <stop offset="5%" stopColor="var(--chart-1)" stopOpacity={0.4}/>
        <stop offset="95%" stopColor="var(--chart-1)" stopOpacity={0}/>
      </linearGradient>
    </defs>
    <Tooltip content={<CustomTooltip />} />
    <Line type="monotone" dataKey="value" stroke="var(--chart-1)" strokeWidth={2} dot={false} />
    <Area type="monotone" dataKey="value" stroke="none" fill="url(#gradient-chart)" />
  </LineChart>
</ResponsiveContainer>
```

### المخطط الدائري (Donut Chart)

- **الغرض**: عرض توزيع حالات الامتثال (ممتثل، جزئي، غير ممتثل).
- **الكود**: يتم إنشاؤه باستخدام مكون `PieChart` مع `innerRadius` لإنشاء شكل الدونات.

```jsx
// مثال مبسط من DashboardPage-CQ6WOYdy.js
<ResponsiveContainer width="100%" height={200}>
  <PieChart>
    <Pie
      data={complianceData}
      cx="50%"
      cy="50%"
      innerRadius={60}
      outerRadius={80}
      paddingAngle={5}
      dataKey="value"
    >
      {complianceData.map((entry, index) => (
        <Cell key={`cell-${index}`} fill={COLORS[index % COLORS.length]} />
      ))}
    </Pie>
    <Tooltip />
    <Legend />
  </PieChart>
</ResponsiveContainer>
```

## 3.3. الألوان والتسميات

- **الألوان**: يتم استخدام نظام ألوان متناسق مستمد من متغيرات CSS.
  - `#3db1ac` (chart-1)
  - `#7c70ca` (chart-2)
  - `#6459a7` (chart-3)
  - `#4a7ab5` (chart-4)
  - `#525e8c` (chart-5)
- **التسميات العربية**: جميع المخططات تستخدم تسميات باللغة العربية لأسماء الشهور، أنواع البيانات، وحالات الامتثال، مما يضمن تجربة مستخدم متكاملة.
  - `"يناير", "فبراير", "مارس", ...`
  - `"سياسة الخصوصية", "ملفات الارتباط", ...`
  - `"ممتثل", "جزئي", "غير ممتثل"`

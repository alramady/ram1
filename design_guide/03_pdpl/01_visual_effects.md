# دليل التصميم: منصة PDPL - المؤثرات البصرية

## 1. Keyframes Animations (`@keyframes`)

تعتمد منصة PDPL على مجموعة غنية من **35 حركة `@keyframes`** فريدة لإضفاء الحيوية والجاذبية على الواجهة. هذه الحركات مصممة بعناية لتعزيز تجربة المستخدم وجعل التفاعل مع البيانات أكثر سلاسة ومتعة.

### الحركات المميزة:

- **`aurora-shift`**: يخلق تأثيراً بصرياً مذهلاً يشبه الشفق القطبي في خلفيات بعض العناصر.
- **`stat-count-up`**: حركة عد تصاعدي للأرقام في بطاقات الإحصائيات، مما يعطي إحساساً بالبيانات الحية.
- **`glow-border-pulse`**: نبض متوهج لحدود العناصر، يستخدم لتسليط الضوء على البطاقات أو التنبيهات الهامة.
- **`scan-line`**: خط مسح متحرك يعطي إيحاءً بعمليات الرصد والتحليل الفوري.
- **`subtle-float`**: حركة طفو خفيفة تجعل العناصر تبدو وكأنها تسبح في الفضاء الرقمي.

### قائمة الحركات الكاملة:

| # | اسم الحركة | الوصف |
| :-- | :--- | :--- |
| 1 | `aurora-shift` | تحريك خلفية متدرجة لخلق تأثير الشفق. |
| 2 | `stat-count-up` | حركة ظهور الأرقام مع انزلاق للأعلى. |
| 3 | `icon-bounce` | حركة ارتداد خفيفة للأيقونات. |
| 4 | `progress-fill` | ملء تدريجي لأشرطة التقدم. |
| 5 | `badge-pop` | ظهور مفاجئ للشارات (Badges). |
| 6 | `card-entrance` | حركة دخول للبطاقات مع تأثير انزلاق وتلاشي. |
| 7 | `orbit-spin` | دوران مداري للعناصر الزخرفية. |
| 8 | `orbit-spin-reverse` | دوران مداري عكسي. |
| 9 | `breathing-glow` | توهج نابض يشبه التنفس. |
| 10 | `shimmer` | تأثير وميض وتحميل للمحتوى. |
| 11 | `pulse-glow` | نبضات توهج. |
| 12 | `glow-pulse` | نبضات توهج لظلال الصندوق. |
| 13 | `border-glow` | توهج لحدود العنصر. |
| 14 | `float-bubble` | حركة طفو فقاعية. |
| 15 | `scan-line` | خط مسح متحرك. |
| 16 | `data-flow` | حركة تدفق بيانات في الخلفية. |
| 17 | `breathe` | حركة تنفس خفيفة. |
| 18 | `logo-float` | حركة طفو للشعار. |
| 19 | `orbit` | حركة مدارية. |
| 20 | `fade-in-up` | ظهور للأعلى. |
| 21 | `fade-in-right` | ظهور من اليمين. |
| 22 | `fade-in-left` | ظهور من اليسار. |
| 23 | `scale-in` | تكبير للداخل. |
| 24 | `slide-in-bottom` | انزلاق للداخل من الأسفل. |
| 25 | `number-pop` | ظهور مفاجئ للأرقام. |
| 26 | `glow-border-pulse` | نبض متوهج للحدود والظلال. |
| 27 | `subtle-float` | حركة طفو خفيفة. |
| 28 | `spin` | دوران. |
| 29 | `ping` | نبضة سريعة. |
| 30 | `pulse` | نبضات متكررة. |
| 31 | `enter` | حركة دخول عامة. |
| 32 | `exit` | حركة خروج عامة. |
| 33 | `accordion-down` | فتح قائمة منسدلة. |
| 34 | `accordion-up` | إغلاق قائمة منسدلة. |
| 35 | `caret-blink` | وميض مؤشر الكتابة. |

### كود `@keyframes` الكامل:

```css
/* 35 Keyframes Animations */

@keyframes aurora-shift { 0% { background-position: 0%; } 50% { background-position: 100%; } to { background-position: 0%; } }
@keyframes stat-count-up { 0% { opacity: 0; transform: translateY(10px); } to { opacity: 1; transform: translateY(0); } }
@keyframes icon-bounce { 0%, to { transform: translateY(0); } 50% { transform: translateY(-3px); } }
@keyframes progress-fill { 0% { width: 0; } }
@keyframes badge-pop { 0% { transform: scale(0); } 70% { transform: scale(1.15); } to { transform: scale(1); } }
@keyframes card-entrance { 0% { opacity: 0; transform: translateY(20px) scale(.97); } to { opacity: 1; transform: translateY(0) scale(1); } }
@keyframes orbit-spin { 0% { transform: translate(-50%, -50%) rotate(0); } to { transform: translate(-50%, -50%) rotate(360deg); } }
@keyframes orbit-spin-reverse { 0% { transform: translate(-50%, -50%) rotate(360deg); } to { transform: translate(-50%, -50%) rotate(0); } }
@keyframes breathing-glow { 0%, to { opacity: .3; transform: translate(-50%, -50%) scale(1); } 50% { opacity: .6; transform: translate(-50%, -50%) scale(1.1); } }
@keyframes shimmer { 0% { background-position: -200% 0; } to { background-position: 200% 0; } }
@keyframes pulse-glow { 0%, to { opacity: .6; } 50% { opacity: 1; } }
@keyframes glow-pulse { 0%, to { box-shadow: 0 0 8px #3db1ac33; } 50% { box-shadow: 0 0 20px #3db1ac66; } }
@keyframes border-glow { 0%, to { border-color: #3db1ac26; } 50% { border-color: #3db1ac59; } }
@keyframes float-bubble { 0%, to { transform: translateY(0) rotate(0); } 33% { transform: translateY(-8px) rotate(2deg); } 66% { transform: translateY(4px) rotate(-1deg); } }
@keyframes scan-line { 0% { transform: translateY(-100%); } to { transform: translateY(400%); } }
@keyframes data-flow { 0% { background-position: 200% 0; } to { background-position: -200% 0; } }
@keyframes breathe { 0%, to { opacity: .5; transform: scaleY(.8); } 50% { opacity: 1; transform: scaleY(1); } }
@keyframes logo-float { 0%, to { transform: translateY(0); } 50% { transform: translateY(-3px); } }
@keyframes orbit { 0% { transform: rotate(0) translate(8px) rotate(0); } to { transform: rotate(360deg) translate(8px) rotate(-360deg); } }
@keyframes fade-in-up { 0% { opacity: 0; transform: translateY(24px) scale(.96); } to { opacity: 1; transform: translateY(0) scale(1); } }
@keyframes fade-in-right { 0% { opacity: 0; transform: translate(24px); } to { opacity: 1; transform: translate(0); } }
@keyframes fade-in-left { 0% { opacity: 0; transform: translate(-24px); } to { opacity: 1; transform: translate(0); } }
@keyframes scale-in { 0% { opacity: 0; transform: scale(.9); } to { opacity: 1; transform: scale(1); } }
@keyframes slide-in-bottom { 0% { opacity: 0; transform: translateY(40px); } to { opacity: 1; transform: translateY(0); } }
@keyframes number-pop { 0% { opacity: 0; transform: scale(.5); } 70% { transform: scale(1.08); } to { opacity: 1; transform: scale(1); } }
@keyframes glow-border-pulse { 0%, to { border-color: #3db1ac1f; box-shadow: 0 0 #3db1ac00; } 50% { border-color: #3db1ac4d; box-shadow: 0 0 16px #3db1ac1a; } }
@keyframes subtle-float { 0%, to { transform: translateY(0); } 50% { transform: translateY(-4px); } }
@keyframes spin { to { transform: rotate(360deg); } }
@keyframes ping { 75%, to { opacity: 0; transform: scale(2); } }
@keyframes pulse { 50% { opacity: .5; } }
@keyframes enter { from { opacity: var(--tw-enter-opacity, 1); transform: translate3d(var(--tw-enter-translate-x, 0), var(--tw-enter-translate-y, 0), 0) scale3d(var(--tw-enter-scale, 1), var(--tw-enter-scale, 1), var(--tw-enter-scale, 1)) rotate(var(--tw-enter-rotate, 0)); filter: blur(var(--tw-enter-blur, 0)); } }
@keyframes exit { to { opacity: var(--tw-exit-opacity, 1); transform: translate3d(var(--tw-exit-translate-x, 0), var(--tw-exit-translate-y, 0), 0) scale3d(var(--tw-exit-scale, 1), var(--tw-exit-scale, 1), var(--tw-exit-scale, 1)) rotate(var(--tw-exit-rotate, 0)); filter: blur(var(--tw-exit-blur, 0)); } }
@keyframes accordion-down { from { height: 0; } to { height: var(--radix-accordion-content-height); } }
@keyframes accordion-up { from { height: var(--radix-accordion-content-height); } to { height: 0; } }
@keyframes caret-blink { 0%, 70%, to { opacity: 1; } 20%, 50% { opacity: 0; } }


```

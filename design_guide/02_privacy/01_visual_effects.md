# دليل التصميم: منصة الخصوصية - المؤثرات البصرية

## 1. Keyframes Animations (`@keyframes`)

تم استخراج **34 حركة** `@keyframes` فريدة من ملف CSS الخاص بمنصة الخصوصية. هذه الحركات هي أساس كل المؤثرات البصرية الديناميكية في المنصة، من تحميل المحتوى إلى تفاعل المستخدم.

### قائمة الحركات الكاملة:

| # | اسم الحركة | الوصف |
| :-- | :--- | :--- |
| 1 | `shimmer` | تأثير وميض وتحميل يستخدم لخلق إحساس بوجود محتوى قادم. |
| 2 | `breathe` | حركة تنفس خفيفة تجعل العناصر تبدو حية. |
| 3 | `orbit` | حركة دوران كوكبية للعناصر الزخرفية. |
| 4 | `spin` | دوران بسيط ومستمر. |
| 5 | `ping` | نبضة سريعة تستخدم لجذب الانتباه. |
| 6 | `pulse` | نبضات متكررة لإظهار حالة نشطة. |
| 7 | `enter` | حركة دخول للعناصر مع تأثيرات متنوعة. |
| 8 | `exit` | حركة خروج للعناصر. |
| 9 | `accordion-down` | فتح قائمة منسدلة (Accordion). |
| 10 | `accordion-up` | إغلاق قائمة منسدلة. |
| 11 | `caret-blink` | وميض مؤشر الكتابة. |
| 12 | `confetti-fall` | حركة سقوط قصاصات الورق للاحتفال. |
| 13 | `confetti-shake` | حركة اهتزاز قصاصات الورق. |
| 14 | `confetti-slow-spin` | دوران بطيء لقصاصات الورق. |
| 15 | `fade-in` | ظهور تدريجي. |
| 16 | `fade-out` | اختفاء تدريجي. |
| 17 | `fade-in-up` | ظهور للأعلى. |
| 18 | `fade-in-down` | ظهور للأسفل. |
| 19 | `fade-in-left` | ظهور من اليسار. |
| 20 | `fade-in-right` | ظهور من اليمين. |
| 21 | `fade-out-up` | اختفاء للأعلى. |
| 22 | `fade-out-down` | اختفاء للأسفل. |
| 23 | `fade-out-left` | اختفاء لليسار. |
| 24 | `fade-out-right` | اختفاء لليمين. |
| 25 | `slide-in-up` | انزلاق للداخل من الأعلى. |
| 26 | `slide-in-down` | انزلاق للداخل من الأسفل. |
| 27 | `slide-in-left` | انزلاق للداخل من اليسار. |
| 28 | `slide-in-right` | انزلاق للداخل من اليمين. |
| 29 | `slide-out-up` | انزلاق للخارج للأعلى. |
| 30 | `slide-out-down` | انزلاق للخارج للأسفل. |
| 31 | `slide-out-left` | انزلاق للخارج لليسار. |
| 32 | `slide-out-right` | انزلاق للخارج لليمين. |
| 33 | `zoom-in` | تكبير للداخل. |
| 34 | `zoom-out` | تصغير للخارج. |

### كود `@keyframes` الكامل:

```css
/* 34 Keyframes Animations */

@keyframes shimmer {
  100% {
    transform: translateX(100%);
  }
}

@keyframes breathe {
  0%, 100% { opacity: 0.5; transform: scaleY(0.8); }
  50% { opacity: 1; transform: scaleY(1); }
}

@keyframes orbit {
  0% {
    transform: rotate(0deg) translateX(8px) rotate(0deg);
  }
  100% {
    transform: rotate(360deg) translateX(8px) rotate(-360deg);
  }
}

@keyframes spin {
  to {
    transform: rotate(360deg);
  }
}

@keyframes ping {
  75%, 100% {
    transform: scale(2);
    opacity: 0;
  }
}

@keyframes pulse {
  50% {
    opacity: .5;
  }
}

@keyframes enter {
  from {
    opacity: var(--tw-enter-opacity, 1);
    transform: translate3d(var(--tw-enter-translate-x, 0), var(--tw-enter-translate-y, 0), 0) scale3d(var(--tw-enter-scale, 1), var(--tw-enter-scale, 1), var(--tw-enter-scale, 1)) rotate(var(--tw-enter-rotate, 0));
  }
}

@keyframes exit {
  to {
    opacity: var(--tw-exit-opacity, 1);
    transform: translate3d(var(--tw-exit-translate-x, 0), var(--tw-exit-translate-y, 0), 0) scale3d(var(--tw-exit-scale, 1), var(--tw-exit-scale, 1), var(--tw-exit-scale, 1)) rotate(var(--tw-exit-rotate, 0));
  }
}

@keyframes accordion-down {
  from {
    height: 0;
  }
  to {
    height: var(--radix-accordion-content-height);
  }
}

@keyframes accordion-up {
  from {
    height: var(--radix-accordion-content-height);
  }
  to {
    height: 0;
  }
}

@keyframes caret-blink {
  0%, 70%, 100% {
    opacity: 1;
  }
  20%, 50% {
    opacity: 0;
  }
}

@keyframes confetti-fall {
    0% {
        opacity: 1;
        transform: translateY(-10vh) rotateZ(0deg);
    }
    100% {
        opacity: 1;
        transform: translateY(110vh) rotateZ(360deg);
    }
}

@keyframes confetti-shake {
    0%, 100% { transform: translateX(0); }
    50% { transform: translateX(80px); }
}

@keyframes confetti-slow-spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
}

/* Fade In/Out */
@keyframes fade-in { from { opacity: 0; } to { opacity: 1; } }
@keyframes fade-out { from { opacity: 1; } to { opacity: 0; } }

/* Fade In Directional */
@keyframes fade-in-up { from { opacity: 0; transform: translateY(24px); } to { opacity: 1; transform: translateY(0); } }
@keyframes fade-in-down { from { opacity: 0; transform: translateY(-24px); } to { opacity: 1; transform: translateY(0); } }
@keyframes fade-in-left { from { opacity: 0; transform: translateX(24px); } to { opacity: 1; transform: translateX(0); } }
@keyframes fade-in-right { from { opacity: 0; transform: translateX(-24px); } to { opacity: 1; transform: translateX(0); } }

/* Fade Out Directional */
@keyframes fade-out-up { from { opacity: 1; transform: translateY(0); } to { opacity: 0; transform: translateY(-24px); } }
@keyframes fade-out-down { from { opacity: 1; transform: translateY(0); } to { opacity: 0; transform: translateY(24px); } }
@keyframes fade-out-left { from { opacity: 1; transform: translateX(0); } to { opacity: 0; transform: translateX(-24px); } }
@keyframes fade-out-right { from { opacity: 1; transform: translateX(0); } to { opacity: 0; transform: translateX(24px); } }

/* Slide In/Out */
@keyframes slide-in-up { from { transform: translateY(100%); } to { transform: translateY(0); } }
@keyframes slide-in-down { from { transform: translateY(-100%); } to { transform: translateY(0); } }
@keyframes slide-in-left { from { transform: translateX(100%); } to { transform: translateX(0); } }
@keyframes slide-in-right { from { transform: translateX(-100%); } to { transform: translateX(0); } }
@keyframes slide-out-up { from { transform: translateY(0); } to { transform: translateY(-100%); } }
@keyframes slide-out-down { from { transform: translateY(0); } to { transform: translateY(100%); } }
@keyframes slide-out-left { from { transform: translateX(0); } to { transform: translateX(-100%); } }
@keyframes slide-out-right { from { transform: translateX(0); } to { transform: translateX(100%); } }

/* Zoom In/Out */
@keyframes zoom-in { from { transform: scale(0); } to { transform: scale(1); } }
@keyframes zoom-out { from { transform: scale(1); } to { transform: scale(0); } }

```

# مواصفة نمط ريما الكاملة — مرجع البناء

## التوكنات الداكنة (الافتراضي)
الوضع الداكن هو الافتراضي (سكربت inline يقرأ `localStorage` ثم `prefers-color-scheme`، وعند أي خطأ يفرض الداكن). القيم تحت صنف `.dark`:
--background: #0a0a0a
--foreground: #fafafa
--card: #171717
--card-foreground: #fafafa
--popover: #171717 / --popover-foreground: #fafafa
--primary: #e5e5e5
--primary-foreground: #171717
--secondary: #262626 / --secondary-foreground: #fafafa
--muted: #262626 / --muted-foreground: #a1a1a1
--accent: #262626 / --accent-foreground: #fafafa
--destructive: #ff6568
--border: #ffffff1a  (أبيض بشفافية 10%)
--input: #ffffff26  (أبيض بشفافية 15%)
--ring: #737373
--chart-1..5: #a4b3ff, #625fff, #4f39f6, #432dd7, #372aac (غير مستخدمة في الصفحة الرئيسية)
--radius: 0.625rem (10px) — المشتقات: md = radius×0.8 = 8px، xl = ×1.4 = 14px، 2xl = ×1.8 = 18px

## التوكنات الفاتحة
قيم `:root` (الوضع الفاتح):
--background: #ffffff
--foreground: #0a0a0a
--card: #ffffff / --card-foreground: #0a0a0a
--popover: #ffffff / --popover-foreground: #0a0a0a
--primary: #171717
--primary-foreground: #fafafa
--secondary: #f5f5f5 / --secondary-foreground: #171717
--muted: #f5f5f5 / --muted-foreground: #737373
--accent: #f5f5f5 / --accent-foreground: #171717
--destructive: #e40014
--border: #e5e5e5
--input: #e5e5e5
--ring: #a1a1a1
--chart-1..5 نفسها. --radius نفسه 0.625rem.
النظام كله محايد رمادي (نيوترال شادسي إن) بلا لون علامة — التمييز كله بالتباين والحدود.

## التايبوغرافي
العائلات: `html[dir=rtl]` يجعل `--font-sans: thmanyahSans` (أوزان woff2 منفصلة: 300/400/500/700/900، fallback هو Arial مع `size-adjust:103.16%`)، و`html[dir=ltr]` يجعلها `Geist` (خط متغير 100–900). الجسم كله `antialiased`، وسطر الأساس line-height:1.5.
صنف خاص `.thmanyah-swash` = `font-feature-settings:"salt" 1,"ss01" 1,"swsh" 1` — مطبق على اسم الهيرو وفقرة الهيرو فقط (يفعّل الأشكال الزخرفية في خط ثمانية).
الأدوار الفعلية:
- الاسم العملاق h1: خط 48px/سطر 1 → من 640px: 60px → من 768px: 72px، وزن 700، تقنين -0.025em، أقصى عرض 56rem، مع swash.
- فقرة الهيرو: 18px/1.75 → من 640px: 20px/1.75، لون muted-foreground، أقصى عرض 42rem، `text-balance`، مع swash.
- الشارة الحبية: 14px عادي، لون muted-foreground.
- عناوين الأقسام h2: 30px/36px → من 640px: 36px/40px، وزن 700، تقنين -0.025em، توسيط. السطر التوضيحي تحتها: 16px muted-foreground، mt 12px، أقصى عرض 42rem.
- عناوين فرعية داخل الأقسام (مثل «الأدوات والمنصات»): 18px وزن 600.
- عناوين البطاقات h3: 16px وزن 600. عنوان وظيفة الخط الزمني: 16px وزن 500.
- متن البطاقات والقوائم: 14px/1.43 لون muted-foreground؛ فقرة «نبذة عني»: 18px بسطر 1.625.
- الشارات/الرقائق: 12px وزن 500. صف التاريخ/الموقع: 12px muted.
- روابط التنقل والأزرار: 14px وزن 500. الفوتر: 14px muted.

## المكونات
الشارة الحبية (هيرو): `inline-flex items-center gap-8px`، حدود 1px بلون border، `border-radius:9999px`، حشوة 16px أفقي / 6px رأسي، نص 14px muted، أيقونة 16px، بلا خلفية.
الأزرار (نمط شادسي إن): الأساس = inline-flex متوسط، نصف قطر 8px، نص 14px وزن 500، `transition-all 150ms cubic-bezier(.4,0,.2,1)`، عند الضغط `translateY(1px)`، حلقة تركيز 3px بلون ring بشفافية 50%. Primary: خلفية primary ونص primary-foreground، hover → primary بشفافية 80%، ارتفاع 40px، حشوة 10px + أيقونة تضيف ps/pe 8px. Outline: حدود border + خلفية background + ظل `0 1px 2px rgba(0,0,0,.05)`، hover → خلفية muted؛ وفي الداكن: حدود input وخلفية input بشفافية 30% وhover 50%. Ghost (روابط الهيدر): ارتفاع 32px، حدود شفافة، hover → خلفية muted (وفي الداكن muted/50)، نصف قطر 8px. زر أيقونة الثيم: 36px دائري outline. زر القائمة: 36px نصف قطر 8px.
الخبرات = خط زمني رأسي فعلي (وليس بطاقات فقط): الحاوية أقصى عرض 48rem؛ كل عنصر له هامش بداية 32px ومسافة سفلية 24px؛ المؤشر: دائرة 16px حدود 2px بلون primary بشفافية 20% موضوعة على -24px من البداية (مع انعكاس RTL)، وعند `data-completed` تصير حدودها primary كاملة؛ خط الوصل: عرض 2px بلون primary بشفافية 10% وارتفاع calc(100%-1.25rem) مزاح 18px للأسفل، ويصير primary صريحًا إذا كان العنصر التالي مكتملًا، ويختفي في آخر عنصر. رأس العنصر: دائرة حرف الشركة 36px حدود border خلفية card وزن 600 + اسم الشركة 600؛ ثم المسمى 16px وزن 500؛ ثم صف تاريخ/موقع 12px muted بأيقونات 14px. المحتوى: 14px muted، قائمة `list-disc` ببداية 16px وفراغ 6px. بطاقة «مشروع مختار» متداخلة: نصف قطر 14px حدود border خلفية card حشوة 16px. ثم صف رقائق.
رقاقة المهارة (badge): `inline-flex`، نصف قطر 8px، حدود border، خلفية muted بشفافية 60%، حشوة 10px/4px، نص 12px وزن 500 بلون muted-foreground، و`dir="ltr"` لأن المحتوى إنجليزي.
بطاقات فئات المهارات: نصف قطر 18px، حدود border، خلفية card، حشوة 24px، عنوان 600 ثم رقائق بفراغ 8px — شبكة عمودين بفجوة 32px.
شبكة الأدوات: `flex-wrap` متوسطة بفجوات 40px أفقي / 24px رأسي؛ كل أداة: عمود متوسط بفجوة 8px؛ بلاطة الأيقونة 48px نصف قطر 14px حدود border خلفية card وأيقونة 24px بلون foreground؛ التسمية 12px وزن 500.
بطاقات المشاريع: نصف قطر 18px حدود border خلفية card حشوة 24px، عمودية (`flex-col` والوصف `flex-1`)، عنوان 600 ثم وصف 14px muted ثم رقائق — شبكة عمودين بفجوة 24px، بلا حالة hover.
بطاقات المدونة: رابط كامل بنفس وصفة البطاقة + `transition-colors` وhover → خلفية muted بشفافية 50%؛ صف التاريخ 12px، ثم عنوان، ثم مقتطف، ثم «قراءة المزيد» 14px وزن 500 بسهم `rtl:rotate-180` — شبكة 3 أعمدة بفجوة 24px.
بطاقة التعليم: أقصى عرض 48rem، صف `items-start` بفجوة 16px، دائرة أيقونة 44px حدود border خلفية background بأيقونة 20px. بطاقات الشهادات: 3 أعمدة بفجوة 16px، عمودية متوسطة بحشوة 24px.
صندوق التواصل: أقصى عرض 28rem، بطاقة 18px/24px، رابط البريد `hover:text-foreground`، أزرار التواصل دوائر 40px حدود border خلفية background hover → muted بأيقونات 16px.
الهيدر: `sticky top-0 z-50` ارتفاع 64px، يبدأ بحدود سفلية شفافة وخلفية شفافة تمامًا مع `backdrop-blur(8px)`؛ عند تجاوز `scrollY` قيمة 10 تضاف: حدود border + خلفية background بشفافية 95% (أو 50% إذا دُعم backdrop-filter) — بانتقال ألوان 300ms.
القائمة المنسدلة (جوال): طبقة `fixed inset-0 top-16 z-40`؛ خلفية معتمة background بشفافية 95% (60% مع backdrop-filter) مع blur؛ لوحة تدخل بـ fade + `zoom-in` من 97% خلال 200ms ease-out وتخرج بـ fade + zoom-out إلى 95%؛ الروابط أزرار ghost بمحاذاة البداية، وزر اللغة outline دائري بعرض كامل.
الفوتر: حدود علوية border، حشوة رأسية 32px، صف 14px muted موزع بين الطرفين.
الظلال: الوحيد المستخدم `0 1px 2px rgba(0,0,0,.05)` على أزرار outline — البطاقات كلها مسطحة بحدود فقط.

## الحركة
لا توجد مكتبة حركة إطلاقًا — لا `framer-motion` في أي chunk. كل شيء CSS خالص + خطاف `IntersectionObserver` صغير.
عند التحميل (الهيرو فقط): keyframes باسم `hero-intro`: من opacity 0 + blur(8px) + translateY(18px) + scale(.98) إلى الوضع الطبيعي؛ المدة 0.7s بمنحنى `cubic-bezier(.16,1,.3,1)` ووضع `both`؛ تعاقب خمس طبقات بتأخيرات: 80ms (الشارة)، 180ms (الاسم)، 300ms (الفقرة)، 420ms (الأزرار)، 560ms (سهم التمرير).
توهج الهيرو: طبقتان `radial-gradient(ellipse at center, foreground بشفافية 10%, transparent)` مع `blur(50px)` — واحدة خلف القسم كله (ممتدة inset-0 مع `translateY(-33%) scale(1.2)`) وواحدة خلف الاسم؛ keyframes باسم `hero-glow` مدتها 8s ease-in-out لا نهائية: تتنفس بين opacity .6 عند translateY(-33%) scale(1.15) و opacity .9 عند translateY(-28%) scale(1.28)؛ الطبقة الثانية بتأخير -2s كي لا تتزامنا.
عند التمرير (كل الأقسام): مكوّن `Reveal` يرصد بـ `IntersectionObserver` بعتبة 0.15 مرة واحدة ثم يفصل؛ الحالة المخفية `translateY(12px) + opacity 0`، الظاهرة صفر/1؛ الانتقال `all 500ms cubic-bezier(0,0,.2,1)`؛ تعاقب الأشقاء عبر `transition-delay` مضمّن: القيم المستخدمة 50 و60 و70 و80 و100 و140 و160 و210 و280 و350ms (خطوة ~50–80ms لكل عنصر).
عند المرور: الانتقالات الافتراضية 150ms `cubic-bezier(.4,0,.2,1)` — بطاقات المدونة تغيّر الخلفية إلى muted/50، الأزرار تغيّر الخلفية، الروابط تغيّر اللون، والضغط على أي زر يزيحه 1px للأسفل.
الهيدر: انتقال ألوان 300ms ease-out عند تجاوز التمرير 10px. سهم «مرر للأسفل»: `bounce` قياسية 1s لا نهائية. القائمة الجوالة: دخول 200ms (fade + zoom من 97%) وخلفيتها 500ms. `html{scroll-behavior:smooth}` للتنقل بين الأقسام.
مع `prefers-reduced-motion`: حركات الهيرو تُلغى، وكشف التمرير يصير 300ms بلا إزاحة.

## التخطيط
الحاوية: أقصى عرض 64rem (1024px) متوسطة مع حشوة أفقية 16px — نفسها للهيدر والأقسام والفوتر.
الأقسام: حشوة رأسية 80px، ومن 640px تصير 112px. كتلة عنوان القسم لها هامش سفلي 48px.
الهيرو: ارتفاع أدنى `calc(100svh - 4rem)` (يطرح ارتفاع الهيدر 64px)، توسيط كامل، `overflow-x:clip` بسبب التوهج المكبّر. عروض داخلية: الاسم 56rem، الفقرة والنبذة التوضيحية 42rem، النبذة والخط الزمني والتعليم 48rem، التواصل 28rem.
الشبكات وانهيارها (كلها عمود واحد تحت 640px): فئات المهارات عمودان بفجوة 32px؛ المشاريع عمودان بفجوة 24px؛ المدونة 3 أعمدة بفجوة 24px؛ الشهادات 3 أعمدة بفجوة 16px؛ الأدوات `flex-wrap` متوسطة 40px/24px. قائمة سطح المكتب تظهر من 1024px وقبلها زر برغر.
الخدع البصرية: توهجان إشعاعيان فقط (لا شبكة نقاط ولا صور) — بيضاويان بلون foreground بشفافية 10% مع blur 50px؛ في الداكن يعطيان هالة رمادية فاتحة خلف الاسم وفي الفاتح ظلًا دخانيًا خفيفًا. زجاجية الهيدر والقائمة عبر backdrop-blur 8px مع خلفيات شبه شفافة. وحدة المسافات 0.25rem. الاتجاه RTL كامل (`lang=ar dir=rtl`) بخصائص منطقية، والأسهم تنعكس بـ `rotate(180deg)`.

## ملاحظات التنفيذ
أهم ما يلزم لإعادة الإنتاج في ملف واحد بلا Tailwind: (1) الداكن افتراضي — طبّق قيم الداكن على `:root` واجعل الفاتح هو التجاوز. (2) خط thmanyahSans بخمسة أوزان woff2 هو كل الهوية العربية، مع تفعيل `salt/ss01/swsh` على الاسم وفقرة الهيرو فقط؛ Geist للمقاطع اللاتينية داخل الرقائق (`dir=ltr` عليها). (3) لا ظلال على البطاقات — العمق كله من حدود 1px (أبيض 10% في الداكن) وخلفية card أفتح درجة من background. (4) الحركة ثلاث وصفات فقط: hero-intro (0.7s cubic-bezier(.16,1,.3,1) بتعاقب 80→560ms)، وreveal بالتمرير (IntersectionObserver عتبة 0.15، إزاحة 12px، مدة 500ms، تأخيرات 50–350ms)، والتوهج المتنفس 8s. (5) الأيقونات كلها Tabler outline بسماكة 2. الملفات المصدر: /private/tmp/claude-502/-Users-naifaldosari/783831cb-ee92-4954-a512-2ffede07d988/scratchpad/reema/index.html و main.css، وchunks الحركة المفحوصة في مجلد chunks/ بجانبها (منطق الهيدر والقائمة في 2a13enzamhtgm.js، ومكوّن Reveal في 1ocpdtzrl5_6v.js).

## الترويسة والقائمة
ترويسة sticky top-0 z-50 بارتفاع h-16 وbackdrop-blur-sm وحد سفلي شفاف (border-transparent bg-background/0 مع transition-colors — يكتسب حداً/خلفية عند التمرير عبر JS). داخلها nav بعرض max-w-5xl justify-between. اليمين (RTL): رابط الاسم «ريـم حسان» font-semibold tracking-tight إلى /#home. الوسط (hidden lg:flex): سبعة روابط بأسلوب زر ghost (h-8 text-sm hover:bg-muted) إلى مراسي الصفحة: الرئيسية /#home، نبذة عني /#about، الخبرات العملية /#experience، المهارات /#skills، المشاريع /#projects، المدونة /#blog، تواصل معي /#contact (لاحظ: لا رابط لقسم education في القائمة رغم وجوده في الصفحة). اليسار: (1) زر الثيم دائري size-9 rounded-full بأيقونة tabler-icon-sun وaria-label «الوضع الفاتح»، (2) زر اللغة حبة rounded-full بأيقونة tabler-icon-language + نص «English» (مخفي تحت sm: hidden sm:flex)، (3) زر همبرغر size-9 (lg:hidden) بأيقونة tabler-icon-menu-2 وaria-controls="mobile-menu" aria-expanded="false" — القائمة الجوالة تُبنى عند الفتح عبر React وليست في HTML الأولي

## التبديلات (لغة وثيم)
اللغة: الافتراضي عربي (lang="ar" dir="rtl" على html). القاموسان ar وen كاملان مضمّنان في حمولة RSC كخاصية dictionaries لمكوّن LanguageProvider — التبديل client-side بالكامل بلا إعادة تحميل: يبدّل النصوص من القاموس ويضبط document.documentElement.dir وlang. التخزين في localStorage بالمفتاح `reem-portfolio-locale` بقيم "ar"/"en" مع fallback إلى "ar" (الكود من chunk 31yc9u8wa_5f8.js: getItem ثم `"ar"===e||"en"===e?e:"ar"`، ومستمع storage للمزامنة بين التبويبات). زر اللغة يعرض اسم اللغة الأخرى (languageToggleLabel: بالعربي «English» وبالإنجليزي «العربية»). الثيم: التخزين بالمفتاح `reem-portfolio-theme` بقيم "light"/"dark" (chunk 2a13enzamhtgm.js)، والافتراضي بلا تخزين: light فقط إذا matchMedia("(prefers-color-scheme: light)") تطابق، وإلا dark — أي أن dark هو الافتراضي العملي. التطبيق بإضافة/إزالة كلاس .dark على html (متغيرات CSS: فاتح --background:#fff، داكن --background:#0a0a0a --card:#171717 --primary:#e5e5e5). يوجد سكربت inline في head لمنع الوميض قبل الترطيب، لكن فيه خلل بناء طريف: مفتاح localStorage فيه تسرّب كنص خطأ RSC كامل ("Attempted to call THEME_STORAGE_KEY() from the server...") لأن ثابت client مُرّر لسكربت server — فعملياً السكربت المبكر يقرأ مفتاحاً خاطئاً ويسقط دائماً على تفضيل النظام، ثم يصحح الترطيب الثيم من المفتاح الحقيقي. عند إعادة البناء استخدم المفتاح الثابت مباشرة في السكربت

## تقنية الكشيدة
تقنيتان منفصلتان: (1) كشيدة يدوية حرفية في الاسم فقط: النص الخام في HTML هو «ريـم حسان» — حرف تطويل ـ (U+0640 tatweel) واحد مكتوب يدوياً بين الياء والميم. يظهر 3 مرات فقط في الملف كله: رابط الشعار في الترويسة `<a href="/#home">ريـم حسان</a>`، وعنوان الهيرو `<h1 class="thmanyah-swash ...">ريـم حسان</h1>`، وقيمة "name":"ريـم حسان" في قاموس ar. الفوتر بلا كشيدة: «© 2026 ريم حسان». لا توجد أي كشيدة أخرى في الفقرات. (2) المدّات والامتدادات في العنوان والفقرة التعريفية تأتي من خصائص OpenType لخط ثمانية عبر كلاس CSS في main.css: `thmanyah-swash{font-feature-settings:"salt" 1, "ss01" 1, "swsh" 1}` — مطبق على h1 الاسم وفقرة الهيرو فقط (stylistic alternates + stylistic set 01 + swash من خط ThmanyahSans). الخطوط المحملة preload: thmanyahsans_Black/Bold/Light/Medium/Regular woff2 + خط Geist variable للاتيني (كلاسات html: geist_...__variable thmanyahsans_...__variable)

## ملاحظات المحتوى
الفوتر: شريط بسيط border-t py-8، صف يحوي عنصرين: «© 2026 ريم حسان. جميع الحقوق محفوظة.» و«محللة أعمال» (بالإنجليزية: "© 2026 Reem Hassan. All rights reserved." / "Business Analyst"). التقنية: Next.js (App Router + Turbopack) على Vercel، مكونات بنمط shadcn/Tailwind v4 (data-slot="button/badge/timeline")، أيقونات Tabler stroke خطية حصراً حتى لشعارات الأدوات. عنوان الصفحة <title>Reem Hassan — Business Analyst</title> بالإنجليزية دائماً، وmeta description إنجليزي. زر CV يشير إلى صفحة /cv (وليس ملف PDF مباشراً). أنيميشن: الهيرو عبر @keyframes hero-intro (opacity+blur(8px)+translateY(18px)+scale(.98)، 0.7s cubic-bezier(.16,1,.3,1)) بتأخيرات متدرجة، والتوهج @keyframes hero-glow نبض بطيء، وبقية الأقسام scroll-reveal: تبدأ translate-y-3 opacity-0 وتُزال عند الظهور مع transition-delay متدرج (50–100ms بين البطاقات، 70–80ms بين عناصر المجموعة الواحدة)، مع دعم motion-reduce. كل الشارات التقنية dir="ltr" داخل سياق RTL — هذه هي حيلة التعامل مع المصطلحات. مدة القراءة بأرقام عربية هندية «٨». تفاصيل التواصل: WhatsApp عبر رابط QR (wa.me/qr/...)، والهاتف موجود في القاموس فقط وغير معروض. الوضع الداكن: خلفية #0a0a0a وبطاقات #171717 وحدود #ffffff1a؛ الفاتح: أبيض نقي. حقل greeting فارغ في اللغتين (البنية تدعمه لكنه غير مستخدم). الملفات المحلية: /private/tmp/claude-502/-Users-naifaldosari/783831cb-ee92-4954-a512-2ffede07d988/scratchpad/reema/index.html وmain.css وpayload_en.txt (القاموس مفكوك الترميز) وindex.pretty.html (نسخة مقسمة أسطراً)

## بنية الأقسام (DOM)

### home — الرئيسية / Home
section#home بارتفاع min-h-[calc(100svh-4rem)] وسط الشاشة، text-center، مع طبقتي توهج radial-gradient (hero-glow) خلف المحتوى. الترتيب: (1) شارة pill بحدود rounded-full فيها أيقونة tabler-icon-code + نص الدور، (2) h1 الاسم بكلاس thmanyah-swash بأحجام text-5xl → sm:text-6xl → md:text-7xl font-bold tracking-tight وخلفه توهج ثانٍ hero-glow-soft، (3) فقرة تعريفية thmanyah-swash بحد أقصى max-w-2xl text-lg/xl text-muted-foreground، (4) صف زرين: زر أساسي bg-primary يقفز إلى #projects + زر ثانوي بحدود مع أيقونة download يشير إلى /cv، (5) رابط سفلي «مرر للأسفل» مع سهم tabler-icon-arrow-down عليه animate-bounce يشير إلى #about. كل عنصر يحمل hero-intro hero-intro-1..5 (أنيميشن دخول blur(8px)+translateY(18px)+scale(.98) بتأخيرات 80ms/180ms/300ms/420ms/560ms، cubic-bezier(.16,1,.3,1))

### about — نبذة عني / About Me
section#about py-20 sm:py-28، حاوية max-w-5xl: عنوان h2 وسط text-3xl/4xl font-bold ثم بطاقة واحدة وسط max-w-3xl rounded-2xl border-border bg-card p-8 text-center تحوي فقرة واحدة text-lg leading-relaxed text-muted-foreground. كل الأقسام تستخدم نمط ظهور بالتمرير: translate-y-3 opacity-0 + transition-all duration-500 مع transition-delay متدرج (100ms للبطاقة)

### experience — الخبرات العملية / Work Experience
خط زمني عمودي (data-slot=timeline، data-orientation=vertical، max-w-3xl). كل عنصر timeline-item فيه: (أ) رأس: دائرة size-9 rounded-full بحرف أول للشركة + اسم الشركة font-semibold بجانبها، ثم h3 المسمى الوظيفي، ثم صف ميتا text-xs بأيقونتي calendar (التاريخ) و map-pin (الموقع، اختياري — Tawasul بلا موقع)؛ (ب) مؤشر دائري size-4 border-primary على بداية الخط + خط فاصل عمودي bg-primary/10 يربط العناصر؛ (ج) المحتوى: ul list-disc ps-4 بالنقاط، ثم اختيارياً بطاقة «مشروع مختار» داخلية rounded-xl bg-card p-4 بعنوان font-semibold + ul نقاط، ثم صف شارات: span data-slot=badge rounded-md bg-muted/60 text-xs dir="ltr" (الوسوم إنجليزية دائماً). تأخيرات ظهور متدرجة 0/80/160ms

### skills — المهارات / Skills
جزآن: (1) «الأدوات والمنصات»: h3 وسط + سطر وصف صغير، ثم صف flex-wrap وسط gap-x-10 gap-y-6 من عناصر عمودية: مربع size-12 rounded-xl border bg-card فيه أيقونة tabler size-6 + اسم الأداة text-xs تحته. عشر أدوات بالترتيب: Jira, ClickUp, Linear, Trello, Figma, MS Excel, Power BI, MS Office, Slack, VS Code (كل الأيقونات tabler stroke وليست شعارات ملونة؛ ClickUp يستخدم layout-kanban وLinear يستخدم activity كبدائل). (2) ست مجموعات مهارات، كل مجموعة: h3 عنوان عربي مع المصطلح الإنجليزي بين قوسين + صف شارات badge dir="ltr" مثل شارات الخبرات، بتأخير ظهور متدرج 70ms بين المجموعات

### education — التعليم والتطوير المهني / Education & Professional Development
ثلاث كتل: (1) بطاقة شهادة واحدة max-w-3xl أفقية items-start gap-4 rounded-2xl bg-card p-6: دائرة size-11 rounded-full فيها أيقونة tabler-icon-school + عمودان نصيان (الدرجة font-semibold، الجامعة text-sm muted). (2) h3 «التطوير المهني» وسط ثم grid sm:grid-cols-3 من بطاقات عمودية text-center rounded-2xl bg-card p-6: دائرة أيقونة tabler-icon-certificate + عنوان الدورة text-sm font-semibold + اسم المدرب text-xs muted، بتأخير 50ms/100ms. (3) h3 «اللغات» ثم صف حبوب أفقية rounded-full border bg-card px-5 py-2.5: أيقونة tabler-icon-language + اسم اللغة font-medium + المستوى muted

### projects — أبرز المشاريع / Featured Projects
عنوان h2 + سطر وصف mt-3 muted وسط، ثم grid gap-6 sm:grid-cols-2 من بطاقات flex flex-col rounded-2xl border bg-card p-6: h3 font-semibold mb-2 ثم فقرة وصف text-sm muted flex-1 (تدفع الشارات للأسفل) ثم صف شارات badge dir="ltr". لا صور ولا روابط في البطاقات. تأخير البطاقة الثانية 60ms

### blog — أحدث المقالات / From the Blog
عنوان + وصف وسط، ثم grid sm:grid-cols-3 (مقال واحد فقط حالياً)، البطاقة كلها رابط <a> إلى /blog/vertical-erp-school-transport-ksa بكلاسات rounded-2xl border bg-card p-6 hover:bg-muted/50: صف ميتا أعلى dir="rtl" text-xs فيه <time dateTime="2026-06-23T00:00:00.000Z"> + نقطة فاصلة · + مدة القراءة بأرقام هندية «٨ دقائق قراءة»، ثم h3 عنوان المقال، ثم فقرة مقتطف flex-1، ثم «قراءة المزيد» مع سهم tabler-icon-arrow (يتجه يساراً في RTL). تحت الشبكة زر ثانوي وسط «عرض جميع المقالات» إلى /blog

### contact — تواصل معي / Get in Touch
عنوان h2 وسط ثم بطاقة واحدة ضيقة max-w-md rounded-2xl border bg-card p-6: h3 «معلومات التواصل» + فقرة وصف، ثم رابط بريد mailto بأيقونة tabler-icon-mail والنص داخل <span dir="ltr">، ثم كتلة mt-8: h3 صغير «تواصل معي عبر» + صف ثلاث دوائر size-10 rounded-full border أيقونات: WhatsApp (https://wa.me/qr/6G6LLCXHU3HLD1) وLinkedIn (https://www.linkedin.com/in/reem-hassan742r/) وEmail (mailto). لا يوجد نموذج إرسال إطلاقاً — بطاقة معلومات فقط. الهاتف +966 59 779 7642 موجود في القاموس لكنه غير معروض في الصفحة الرئيسية

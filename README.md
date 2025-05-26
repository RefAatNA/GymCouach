<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>الخطة التدريبية الأسبوعية</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=Cairo:wght@400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/chart.js@3.7.0/dist/chart.min.js"></script>
    <style>
        body {
            font-family: 'Cairo', 'Inter', sans-serif;
            background-color: #f5f5f4; /* Tailwind stone-100 */
        }
        .nav-button {
            transition: all 0.3s ease;
        }
        .nav-button.active {
            background-color: #0891b2; /* Tailwind cyan-600 */
            color: #f0f9ff; /* Tailwind cyan-50 */
            box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06);
        }
        .content-section {
            background-color: #ffffff; /* White */
            border-radius: 0.5rem; /* rounded-lg */
            padding: 1.5rem; /* p-6 */
            box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1), 0 4px 6px -2px rgba(0, 0, 0, 0.05);
            margin-top: 1.5rem; /* mt-6 */
        }
        .table th, .table td {
            border: 1px solid #e5e7eb; /* Tailwind gray-200 */
            padding: 0.75rem; /* p-3 */
            text-align: right;
        }
        .table th {
            background-color: #f3f4f6; /* Tailwind gray-100 */
            font-weight: 600; /* font-semibold */
        }
        .chart-container { /* As per persona requirements, even if not used in this specific instance */
            position: relative;
            width: 100%;
            max-width: 600px; /* Example max-width */
            margin-left: auto;
            margin-right: auto;
            height: 300px; /* Base height */
            max-height: 400px; /* Max height */
        }
        @media (min-width: 768px) {
            .chart-container {
                height: 350px;
            }
        }
    </style>
</head>
<body class="text-slate-800">
    <div class="container mx-auto p-4 sm:p-6 lg:p-8 max-w-5xl">
        <header class="text-center mb-8">
            <h1 class="text-3xl sm:text-4xl font-bold text-cyan-700">الخطة التدريبية الأسبوعية المفصلة</h1>
            <p class="mt-2 text-lg text-slate-600">اختر يوماً من القائمة أدناه لعرض الخطة التدريبية الخاصة به.</p>
        </header>

        <nav class="flex flex-wrap justify-center gap-2 mb-8" id="dayNavigation">
            </nav>

        <main id="workoutContent" class="min-h-[300px]">
            <div class="text-center p-10 bg-white rounded-lg shadow-lg">
                <p class="text-xl text-slate-500">الرجاء اختيار يوم لعرض تفاصيل التمرين.</p>
            </div>
        </main>

        <footer class="text-center mt-12 py-6 border-t border-slate-300">
            <p class="text-slate-500">&copy; 2024 خطتك التدريبية. بالتوفيق في رحلتك نحو القوة والصحة!</p>
        </footer>
    </div>

    <script>
        const workoutData = [
            {
                dayId: "sat",
                dayName: "اليوم الأول: السبت (الصدر - Chest)",
                focus: "الصدر (Chest)",
                warmUp: [
                    "10 دقائق كارديو (بشدة خفيفة إلى متوسطة، مثل المشي السريع أو الدراجة الثابتة).",
                    "5 دقائق إحماء ديناميكي يستهدف منطقة الصدر والأكتاف (مثل تدوير الذراعين للأمام والخلف، فتح وضم الذراعين بشكل ديناميكي، شد الصدر الديناميكي)."
                ],
                exercises: [
                    { name: "باربيل بنش بريس (Barbell Bench Press) - ضغط البار على البنش المستوي", sets: "5", reps: "4-6", rest: "2-3 دقائق", notes: "ركز على القوة والأداء الصحيح. تأكد من نزول البار حتى يلمس منتصف صدرك وصعود متحكم به. اطلب مساعدة (Spotter) إذا كنت تستخدم أوزاناً قريبة من أقصى ما يمكنك رفعه." },
                    { name: "دمبل بنش بريس مائل للأعلى (Incline Dumbbell Press)", sets: "4", reps: "8-12", rest: "60-90 ثانية", notes: "استهدف الجزء العلوي من الصدر. استخدم مدى حركي كامل، انزل بالدمبلز حتى تشعر بتمدد جيد في الصدر." },
                    { name: "غطس للصدر (Chest Dips) **أو** باربيل بنش بريس مائل للأسفل (Decline Barbell Press)", sets: "3", reps: "8-12", rest: "60-90 ثانية", notes: "**للغطس:** ميل الجذع للأمام قليلاً لزيادة تفعيل الصدر. **لبديل البنش المائل للأسفل:** استهدف الجزء السفلي من الصدر." },
                    { name: "تفتيح بالكيبل (Cable Crossovers) **أو** تفتيح بالدمبل (Dumbbell Flyes)", sets: "3", reps: "10-15", rest: "60 ثانية", notes: "ركز على الإحساس بالتمدد الكامل عند فتح الذراعين، والعصر (القبض) الجيد عند تقريبهما. الحركة يجب أن تكون من مفصل الكتف." },
                    { name: "(اختياري إذا كان لديك طاقة متبقية) تمرين الضغط (Push-ups)", sets: "2", reps: "حتى الفشل العضلي", rest: "60 ثانية", notes: "لضخ دم إضافي وإنهاء التمرين بقوة." }
                ],
                coolDown: [
                    "10 دقائق كارديو (بشدة خفيفة).",
                    "5-10 دقائق تمارين إطالة ثابتة لعضلات الصدر، الأكتاف الأمامية، والترايسبس."
                ]
            },
            {
                dayId: "sun",
                dayName: "اليوم الثاني: الأحد (الظهر - Back)",
                focus: "الظهر (Back)",
                warmUp: [
                    "10 دقائق كارديو (خفيف إلى متوسط).",
                    "5 دقائق إحماء ديناميكي يستهدف الظهر والأكتاف (مثل تدوير الذراعين، سحب خفيف بحبل المقاومة، تمرين \"القطة والجمل\" أو Cat-Cow stretches)."
                ],
                exercises: [
                    { name: "سحب البار بالانحناء (Barbell Rows - Bent-Over Rows)", sets: "4", reps: "6-10", rest: "90-120 ثانية", notes: "حافظ على استقامة ظهرك (لا تقوسه). اسحب البار نحو أسفل البطن أو أعلى السرة." },
                    { name: "عقلة (Pull-ups) **أو** سحب أمامي لأسفل بجهاز اللات (Lat Pulldowns)", sets: "4", reps: "أكبر عدد ممكن (AMRAP) أو 8-12", rest: "60-90 ثانية", notes: "**للعقلة:** إذا كنت تستطيع، فهي الأفضل. **للسحب الأمامي:** ركز على سحب المرفقين للأسفل وللخلف، وتخيل أنك تحاول وضع مرفقيك في جيوبك الخلفية." },
                    { name: "سحب الكيبل الأرضي بقبضة ضيقة (Seated Cable Rows - Close Grip)", sets: "3", reps: "8-12", rest: "60-90 ثانية", notes: "حافظ على استقامة ظهرك، اسحب القبضة نحو بطنك مع عصر لوحي الكتفين معًا في نهاية الحركة." },
                    { name: "سحب التي-بار (T-Bar Rows) **أو** سحب الدمبل بذراع واحدة (Single-Arm Dumbbell Rows)", sets: "3", reps: "8-12 (لكل ذراع)", rest: "60-90 ثانية", notes: "**لسحب الدمبل بذراع واحدة:** استند بذراعك وركبتك الأخرى على البنش للحصول على دعم جيد. ركز على سحب الدمبل للأعلى وللخلف، مع الحفاظ على جذعك ثابتًا." },
                    { name: "سحب الحبل للوجه (Face Pulls)", sets: "3", reps: "12-15", rest: "60 ثانية", notes: "استخدم وزن خفيف إلى متوسط للتركيز على الأداء. اسحب الحبل نحو وجهك (مستوى العين أو الأنف) مع تدوير ذراعيك للخارج في نهاية الحركة. مهم لصحة الكتف والظهر العلوي." },
                    { name: "(اختياري، إذا شعرت أن أسفل ظهرك يحتاج لمزيد من العمل المباشر) تمرين قطنية الظهر (Hyperextensions / Back Extensions)", sets: "3", reps: "10-15", rest: "60 ثانية", notes: "تحكم في الحركة صعوداً وهبوطاً، لا تفرط في مد ظهرك للخلف في أعلى نقطة." }
                ],
                coolDown: [
                    "10 دقائق كارديو (خفيف).",
                    "5-10 دقائق تمارين إطالة ثابتة لعضلات الظهر (خاصة اللاتس)، والبايسبس."
                ]
            },
            {
                dayId: "mon",
                dayName: "اليوم الثالث: الاثنين (الأكتاف - Shoulders)",
                focus: "الأكتاف (Shoulders)",
                warmUp: [
                    "10 دقائق كارديو (خفيف إلى متوسط).",
                    "5 دقائق إحماء ديناميكي دائري للأكتاف، تدوير الذراعين، وتمارين خفيفة جداً للـ rotator cuff (الكفة المدورة) باستخدام حبل مقاومة أو أوزان خفيفة جداً."
                ],
                exercises: [
                    { name: "ضغط الكتف بالبار وقوفاً (Standing Barbell Overhead Press / Military Press)", sets: "4", reps: "6-10", rest: "90-120 ثانية", notes: "حافظ على ثبات الجذع (شد عضلات البطن). ادفع البار بشكل مستقيم فوق رأسك. تجنب تقويس الظهر بشكل مفرط." },
                    { name: "رفرفة جانبية بالدمبل (Dumbbell Lateral Raises)", sets: "4", reps: "10-15", rest: "60 ثانية", notes: "ركز على الأداء الصحيح والشعور بالعضلة، الوزن هنا ليس الأهم. ارفع الدمبلز إلى الجانبين مع انحناء طفيف في المرفقين، حتى يصل ذراعاك إلى مستوى الكتفين تقريباً. للرأس الجانبي (الوسطي) للكتف." },
                    { name: "رفرفة أمامية بالدمبل (Dumbbell Front Raises) **أو** بالطبق (Plate Front Raise)", sets: "3", reps: "10-12", rest: "60 ثانية", notes: "ارفع الدمبل أو الطبق أمامك حتى مستوى الكتف. للرأس الأمامي للكتف. يمكنك أداء التمرين بذراع واحدة بالتبادل أو بكلتا الذراعين معاً." },
                    { name: "رفرفة خلفية بالدمبل بانحناء الجذع (Bent-Over Dumbbell Reverse Flyes) **أو** باستخدام جهاز الرفرفة الخلفية (Reverse Pec-Deck Machine)", sets: "4", reps: "12-15", rest: "60 ثانية", notes: "مهم جداً لمظهر الكتف ثلاثي الأبعاد وصحة المفصل. إذا كنت تستخدم الدمبل، انحنِ بالجذع للأمام مع الحفاظ على استقامة الظهر. ارفع الدمبلز إلى الجانبين مع الحفاظ على انحناء طفيف في المرفقين، مع التركيز على عصر لوحي الكتفين معًا بشكل خفيف في أعلى نقطة. للرأس الخلفي للكتف." },
                    { name: "(اختياري) تمرين الترابيس بالدمبل أو البار (Dumbbell or Barbell Shrugs)", sets: "3", reps: "10-15", rest: "60 ثانية", notes: "ارفع كتفيك نحو أذنيك بشكل مستقيم لأعلى ثم أنزلهما ببطء. لا تقم بتدوير الكتفين." }
                ],
                coolDown: [
                    "10 دقائق كارديو (خفيف).",
                    "5-10 دقائق تمارين إطالة ثابتة لعضلات الكتف الأمامية والجانبية والخلفية، وعضلات الصدر العلوية."
                ]
            },
            {
                dayId: "tue",
                dayName: "اليوم الرابع: الثلاثاء (راحة - Rest Day)",
                isRestDay: true,
                advice: [
                    "**التركيز على الاستشفاء:** جسمك يحتاج إلى هذا اليوم لإصلاح الأنسجة العضلية وإعادة بناء الطاقة.",
                    "**التغذية الجيدة والمتوازنة:** استمر في تناول كميات كافية من البروتين لدعم إصلاح العضلات. لا تقلل السعرات الحرارية بشكل كبير لمجرد أنه يوم راحة.",
                    "**الترطيب الكافي:** شرب الماء ضروري لجميع وظائف الجسم، بما في ذلك الاستشفاء.",
                    "**النوم الجيد:** حاول الحصول على 7-9 ساعات من النوم الجيد ليلاً.",
                    "**الراحة النشطة (اختياري):** يمكنك ممارسة أنشطة خفيفة جداً مثل المشي الخفيف لمدة 20-30 دقيقة، أو بعض تمارين الإطالة اللطيفة، أو اليوجا. تجنب أي مجهود بدني عالي."
                ]
            },
            {
                dayId: "wed",
                dayName: "اليوم الخامس: الأربعاء (الأرجل - Legs)",
                focus: "الأرجل (Legs)",
                warmUp: [
                    "10 دقائق كارديو (خفيف إلى متوسط).",
                    "5-10 دقائق إحماء ديناميكي شامل يستهدف الوركين، الركبتين، والكاحلين. مثل: (مرجحة الأرجل للأمام والخلف وللجانبين، سكوات بوزن الجسم، دوائر الورك، دوائر الكاحل)."
                ],
                exercises: [
                    { name: "سكوات بالبار الخلفي (Barbell Back Squats)", sets: "4-5", reps: "6-10", rest: "2-3 دقائق", notes: "حافظ على استقامة ظهرك، انزل حتى يصبح فخذك موازياً للأرض أو أقل قليلاً إذا سمحت مرونتك بذلك، مع الحفاظ على الركبتين تتبعان اتجاه أصابع القدمين." },
                    { name: "الرفعة الرومانية المميتة (Romanian Deadlifts - RDLs)", sets: "4", reps: "8-12", rest: "90-120 ثانية", notes: "حافظ على انحناء طفيف جداً في الركبتين طوال الحركة. انزل بالبار مع دفع الوركين للخلف والحفاظ على استقامة الظهر، حتى تشعر بتمدد جيد في الفخذ الخلفي. لعضلات الفخذ الخلفي (Hamstrings) والمؤخرة (Glutes)." },
                    { name: "دفع الأرجل بجهاز (Leg Press)", sets: "4", reps: "10-15", rest: "60-90 ثانية", notes: "لا تقفل ركبتيك تماماً في أعلى الحركة. يمكنك تغيير وضع قدميك (أعلى/أسفل، واسع/ضيق) لاستهداف أجزاء مختلفة من عضلات الفخذ." },
                    { name: "ثني الأرجل لعضلات الفخذ الخلفية (Lying or Seated Leg Curls)", sets: "3", reps: "10-15", rest: "60 ثانية", notes: "لعزل عضلات الفخذ الخلفي. ركز على الحركة المتحكم بها والعصر في نهاية الانقباض." },
                    { name: "(اختياري ولكن يفضل) تمرين دفع الورك بالبار (Barbell Hip Thrusts) **أو** رفع المؤخرة من الأرض (Glute Bridges)", sets: "3", reps: "8-15", rest: "60-90 ثانية", notes: "لتقوية وتضخيم عضلات المؤخرة بشكل مباشر. ركز على عصر المؤخرة بقوة في أعلى نقطة من الحركة." },
                    { name: "تمرين السمانة وقوفاً (Standing Calf Raises)", sets: "4", reps: "12-20", rest: "45-60 ثانية", notes: "السمانة تستجيب جيداً للتكرارات العالية. حاول الحصول على مدى حركي كامل (تمدد كامل في الأسفل وانقباض كامل في الأعلى)." },
                    { name: "تمرين السمانة جلوساً (Seated Calf Raises)", sets: "3", reps: "15-25", rest: "45-60 ثانية", notes: "يستهدف عضلة السمانة الداخلية (Soleus). مدى حركي كامل." }
                ],
                coolDown: [
                    "10 دقائق كارديو (خفيف).",
                    "5-10 دقائق تمارين إطالة ثابتة شاملة لعضلات الفخذ الأمامي، الفخذ الخلفي، المؤخرة، والسمانة."
                ]
            },
            {
                dayId: "thu",
                dayName: "اليوم السادس: الخميس (الذراعان - Arms: Biceps & Triceps)",
                focus: "الذراعان (Arms)",
                warmUp: [
                    "10 دقائق كارديو (خفيف إلى متوسط).",
                    "5 دقائق إحماء ديناميكي للمرفقين، الرسغين، وتدوير الذراعين، مرجحات خفيفة جداً بالدمبلز."
                ],
                exercises: [
                    { sectionTitle: "ترايسبس (Triceps):", type: "title"},
                    { name: "ضغط البنش بقبضة ضيقة (Close-Grip Bench Press)", sets: "3-4", reps: "6-10", rest: "60-90 ثانية", notes: "استخدم قبضة أضيق من عرض الكتفين بقليل. حافظ على المرفقين قريبين من الجسم أثناء النزول والصعود. تمرين مركب لبناء كتلة وقوة الترايسبس." },
                    { name: "تمديد الترايسبس بالدمبل فوق الرأس (Overhead Dumbbell Extension) - بدمبل واحد أو اثنين", sets: "3", reps: "10-15", rest: "60 ثانية", notes: "لاستهداف الرأس الطويل للترايسبس (مهم لحجم الذراع من الخلف)." },
                    { name: "دفع الكيبل للأسفل بالحبل (Cable Rope Pushdowns)", sets: "3", reps: "10-15", rest: "60 ثانية", notes: "لاستهداف الرأس الجانبي (الخارجي) والوسطي للترايسبس. في نهاية الحركة (عندما تكون الذراعان ممدودتين)، حاول فتح الحبل قليلاً للخارج لزيادة الانقباض." },
                    { sectionTitle: "بايسبس (Biceps):", type: "title"},
                    { name: "مرجحة البار (Barbell Curls)", sets: "3-4", reps: "8-12", rest: "60-90 ثانية", notes: "لبناء كتلة البايسبس الأساسية. حافظ على ثبات المرفقين بجانب الجسم. تجنب التأرجح المفرط بالجسم لرفع الوزن." },
                    { name: "مرجحة الدمبل بالتبادل على بنش مائل (Incline Dumbbell Curls)", sets: "3", reps: "10-12 (لكل ذراع)", rest: "60 ثانية", notes: "اجلس على بنش مائل بزاوية (حوالي 45-60 درجة). اترك ذراعيك تتدليان بشكل طبيعي ثم ارفع الدمبل مع تدوير معصمك (راحة اليد) للأعلى. لتمدد جيد للبايسبس (خاصة الرأس الطويل)." },
                    { name: "مرجحة المطرقة بالدمبل (Dumbbell Hammer Curls)", sets: "3", reps: "10-15 (لكل ذراع)", rest: "60 ثانية", notes: "امسك الدمبل وكأنك تمسك بمطرقة (راحة اليد تواجه الجسم). يستهدف عضلة العضدية (Brachialis) والعضدية الكعبرية (Brachioradialis)، مما يزيد من سماكة الذراع ويعطي مظهراً أقوى للساعد." }
                ],
                coolDown: [
                    "10 دقائق كارديو (خفيف).",
                    "5-10 دقائق تمارين إطالة ثابتة لعضلات البايسبس، الترايسبس، والساعدين."
                ]
            },
            {
                dayId: "fri",
                dayName: "اليوم السابع: الجمعة (راحة - Rest Day)",
                isRestDay: true,
                advice: [
                    "**نفس إرشادات يوم الثلاثاء (يوم الراحة الأول).**",
                    "**التركيز على الاستشفاء التام:** هذا هو يوم الراحة الأخير قبل بدء دورة تدريبية جديدة. تأكد من أن جسمك مستعد.",
                    "**الاستعداد الذهني والبدني:** فكر في أهدافك للأسبوع القادم وحضر نفسك للالتزام بالخطة."
                ]
            }
        ];

        const dayNavigation = document.getElementById('dayNavigation');
        const workoutContent = document.getElementById('workoutContent');
        const dayNamesArabic = {
            sat: "السبت", sun: "الأحد", mon: "الاثنين", tue: "الثلاثاء",
            wed: "الأربعاء", thu: "الخميس", fri: "الجمعة"
        };

        function renderNavigation() {
            workoutData.forEach((day, index) => {
                const button = document.createElement('button');
                button.textContent = dayNamesArabic[day.dayId];
                button.classList.add('nav-button', 'px-4', 'py-2', 'sm:px-6', 'sm:py-3', 'text-sm', 'sm:text-base', 'font-semibold', 'rounded-md', 'shadow', 'bg-white', 'text-cyan-700', 'hover:bg-cyan-500', 'hover:text-white', 'focus:outline-none', 'focus:ring-2', 'focus:ring-cyan-500', 'focus:ring-opacity-50');
                button.dataset.dayId = day.dayId;
                if (index === 0) { // Activate first day by default
                    button.classList.add('active');
                }
                button.addEventListener('click', () => {
                    displayWorkout(day.dayId);
                    document.querySelectorAll('#dayNavigation .nav-button').forEach(btn => btn.classList.remove('active'));
                    button.classList.add('active');
                });
                dayNavigation.appendChild(button);
            });
        }

        function buildList(itemsArray) {
            if (!itemsArray || itemsArray.length === 0) return '';
            let listHtml = '<ul class="list-disc list-inside space-y-1 mb-4 text-slate-700">';
            itemsArray.forEach(item => {
                listHtml += `<li>${item}</li>`;
            });
            listHtml += '</ul>';
            return listHtml;
        }
        
        function buildExercisesTable(exercisesArray) {
            if (!exercisesArray || exercisesArray.length === 0) return '<p class="text-slate-500">لا توجد تمارين لهذا اليوم.</p>';
            
            let tableHtml = '<div class="overflow-x-auto"><table class="table w-full min-w-[600px] text-sm sm:text-base"><thead><tr>';
            tableHtml += '<th class="w-2/5">التمرين (Exercise)</th>';
            tableHtml += '<th>المجموعات (Sets)</th>';
            tableHtml += '<th>التكرارات (Reps)</th>';
            tableHtml += '<th>الراحة (Rest)</th>';
            tableHtml += '<th class="w-2/5">ملاحظات هامة (Notes)</th>';
            tableHtml += '</tr></thead><tbody>';

            exercisesArray.forEach(ex => {
                if (ex.type === 'title') {
                    tableHtml += `<tr><td colspan="5" class="bg-slate-200 text-slate-800 font-bold text-lg py-3">${ex.sectionTitle}</td></tr>`;
                } else {
                    tableHtml += '<tr>';
                    tableHtml += `<td>${ex.name}</td>`;
                    tableHtml += `<td>${ex.sets}</td>`;
                    tableHtml += `<td>${ex.reps}</td>`;
                    tableHtml += `<td>${ex.rest}</td>`;
                    tableHtml += `<td>${ex.notes}</td>`;
                    tableHtml += '</tr>';
                }
            });

            tableHtml += '</tbody></table></div>';
            return tableHtml;
        }

        function displayWorkout(dayId) {
            const dayData = workoutData.find(d => d.dayId === dayId);
            if (!dayData) {
                workoutContent.innerHTML = '<p class="text-center text-red-500">لم يتم العثور على بيانات لهذا اليوم.</p>';
                return;
            }

            let contentHtml = `<div class="content-section animate-fadeIn">`;
            contentHtml += `<h2 class="text-2xl sm:text-3xl font-bold mb-3 text-cyan-700">${dayData.dayName}</h2>`;
            
            if (dayData.isRestDay) {
                contentHtml += `<p class="text-lg font-semibold mb-3 text-slate-700">اليوم هو يوم للراحة والاستشفاء. إليك بعض النصائح:</p>`;
                contentHtml += buildList(dayData.advice);
            } else {
                contentHtml += `<p class="text-lg mb-4 text-slate-600">هذه هي خطتك التدريبية المفصلة لليوم، مع التركيز على: <strong>${dayData.focus}</strong>.</p>`;
                
                contentHtml += '<h3 class="text-xl font-semibold mt-6 mb-2 text-cyan-600">الإحماء (Warm-up):</h3>';
                contentHtml += buildList(dayData.warmUp);

                contentHtml += '<h3 class="text-xl font-semibold mt-6 mb-3 text-cyan-600">التمارين (Exercises):</h3>';
                contentHtml += buildExercisesTable(dayData.exercises);

                contentHtml += '<h3 class="text-xl font-semibold mt-6 mb-2 text-cyan-600">التهدئة (Cool-down):</h3>';
                contentHtml += buildList(dayData.coolDown);
            }
            contentHtml += `</div>`;
            workoutContent.innerHTML = contentHtml;
        }

        document.addEventListener('DOMContentLoaded', () => {
            renderNavigation();
            // Display the first day's workout by default
            if (workoutData.length > 0) {
                displayWorkout(workoutData[0].dayId);
            }
        });

        // Simple fadeIn animation (optional)
        const styleSheet = document.createElement("style");
        styleSheet.type = "text/css";
        styleSheet.innerText = `
            @keyframes fadeIn {
                from { opacity: 0; transform: translateY(10px); }
                to { opacity: 1; transform: translateY(0); }
            }
            .animate-fadeIn { animation: fadeIn 0.5s ease-out forwards; }
        `;
        document.head.appendChild(styleSheet);

    </script>
</body>
</html>

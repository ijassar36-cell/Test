<!doctype html>
<html lang="ar" dir="rtl">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>محاكي اختبار الرخصة المهنية — إعداد : فهد الخالدي</title>

<!-- خط Tajawal -->
<link href="https://fonts.googleapis.com/css2?family=Tajawal:wght@300;400;700;900&display=swap" rel="stylesheet">

<style>
:root{
  --bg:#f4f7fb;
  --card:#ffffff;
  --primary:#1e64d0;
  --accent:#06b6d4;
  --success:#16a34a;
  --danger:#ef4444;
  --muted:#6b7280;
  --radius:14px;
}
*{box-sizing:border-box}
html,body{height:100%}
body{
  margin:0;
  background: linear-gradient(180deg,#eef6ff 0%, #f9fbff 100%);
  font-family: "Tajawal", system-ui, -apple-system, "Segoe UI", Roboto, "Noto Kufi Arabic";
  color:#0b1220;
  -webkit-font-smoothing:antialiased;
  -moz-osx-font-smoothing:grayscale;
  direction:rtl;
  padding:18px;
}

/* Container */
.app{
  max-width:1150px;
  margin:0 auto;
}

/* Header */
.header{
  background:var(--card);
  border-radius:var(--radius);
  padding:18px 20px;
  box-shadow:0 12px 40px rgba(12,22,48,0.07);
  display:flex;
  gap:12px;
  align-items:center;
  justify-content:space-between;
  flex-wrap:wrap;
}
.title {
  font-size:1.35rem;
  font-weight:800;
  color:var(--primary);
}
.subtitle{ color:var(--muted); font-weight:600; font-size:0.95rem; }

/* Controls */
.controls{
  margin-top:14px;
  display:flex;
  gap:12px;
  align-items:center;
  justify-content:space-between;
  flex-wrap:wrap;
}
.left-controls, .right-controls { display:flex; gap:10px; align-items:center; }
.btn{
  background:var(--primary);
  color:#fff;
  padding:10px 14px;
  border-radius:12px;
  border:0;
  font-weight:700;
  cursor:pointer;
  box-shadow:0 8px 26px rgba(30,100,208,0.12);
}
.btn.secondary{
  background:#fff;
  color:var(--primary);
  border:1px solid rgba(30,100,208,0.12);
  box-shadow:none;
}
.counter{
  font-weight:800; color:var(--muted);
}

/* layout */
.main{
  display:grid;
  grid-template-columns: 1fr 360px;
  gap:18px;
  margin-top:18px;
}
@media (max-width:980px){
  .main{ grid-template-columns: 1fr; }
}

/* Quiz column */
.quiz{
  display:flex;
  flex-direction:column;
  gap:14px;
}

/* Card */
.card{
  background:var(--card);
  border-radius:12px;
  padding:14px 16px;
  box-shadow:0 10px 30px rgba(12,22,48,0.06);
  transition:transform .22s, box-shadow .22s;
  overflow:visible;
}
.card:hover{ transform:translateY(-4px); }
.q-head{ display:flex; align-items:center; justify-content:space-between; gap:10px }
.q-num{ background:linear-gradient(135deg,var(--accent),var(--primary)); color:#fff; padding:6px 12px; border-radius:10px; font-weight:800; }
.sentence{ margin:12px 0 14px; font-size:1.06rem; color:#0b1220; line-height:1.6 }

/* choices */
.choices{ display:flex; flex-wrap:wrap; gap:10px; }
.choice{
  flex:1 1 48%;
  background:linear-gradient(180deg,#fbfdff,#f6fbff);
  border-radius:10px;
  padding:12px 14px;
  border:1px solid rgba(15,23,42,0.06);
  font-weight:700;
  cursor:pointer;
  transition: transform .16s, box-shadow .16s;
  user-select:none;
  text-align:right;
  min-width:140px;
}
.choice:hover{ transform:translateY(-6px); box-shadow:0 14px 40px rgba(2,6,23,0.06); }
.choice.disabled{ opacity:.88; cursor:default; transform:none; box-shadow:none; pointer-events:none; }
.choice.correct{ background:linear-gradient(90deg,#bbf7d0,#16a34a); color:#04200a; box-shadow:0 10px 30px rgba(16,185,129,0.12); }
.choice.wrong{ background:linear-gradient(90deg,#ffd6db,#ef4444); color:#3b0a0a; box-shadow:0 10px 30px rgba(239,68,68,0.12); }

/* pop explanation inside card */
.pop{
  margin-top:12px;
  padding:12px;
  border-radius:10px;
  background:linear-gradient(180deg,#ffffff,#fbfdff);
  border:1px solid #e6eef8;
  box-shadow:0 10px 30px rgba(2,6,23,0.04);
  animation:pop .28s ease forwards;
}
.pop strong{ display:block; margin-bottom:6px; font-weight:800; }
@keyframes pop{ from{ opacity:0; transform:translateY(-8px) } to{ opacity:1; transform:none } }

/* side panel */
.side{
  position:relative;
  background:var(--card);
  border-radius:12px;
  padding:16px;
  box-shadow:0 10px 30px rgba(12,22,48,0.06);
  height:max-content;
}
.progress{
  height:12px;
  background:linear-gradient(90deg,#eef6ff,#f0fbff);
  border-radius:999px;
  overflow:hidden;
  margin-bottom:12px;
}
.progress > i{
  display:block;
  height:100%;
  background:linear-gradient(90deg,var(--accent),var(--primary));
  width:0%;
  transition:width .36s ease;
}
.stats{ display:flex; gap:8px; flex-direction:column; margin-top:8px; color:var(--muted); font-weight:700; }
.stat-row{ display:flex; justify-content:space-between; align-items:center; font-size:0.95rem; }

/* overlay final */
.overlay{
  position:fixed;
  inset:0;
  display:none;
  align-items:center;
  justify-content:center;
  background:rgba(2,6,23,0.46);
  z-index:9999;
}
.panel{
  background:#fff;
  padding:20px;
  border-radius:14px;
  max-width:520px;
  width:92%;
  text-align:center;
  box-shadow:0 20px 50px rgba(2,6,23,0.3);
}
.panel h2{ margin:6px 0 10px; color:var(--primary) }
.panel .score{ font-size:2.4rem; font-weight:900; color:var(--success) }
.panel .break{ margin-top:10px; color:var(--muted) }

/* footer */
.footer{ margin-top:22px; text-align:center; color:var(--muted); font-size:0.95rem; }

/* responsive choices on small screens */
@media (max-width:600px){
  .choice{ flex:1 1 100%; }
}
</style>
</head>
<body>
<div class="app">
  <div class="header">
    <div>
      <div class="title">محاكي اختبار الرخصة المهنية</div>
      <div class="subtitle">إعداد : فهد الخالدي</div>
    </div>
    <div class="small" style="color:var(--muted);font-weight:700">محاكاة تفاعلية — 68 سؤال</div>
  </div>

  <div class="controls">
    <div class="left-controls">
      <button id="showAll" class="btn">عرض النتيجة</button>
      <button id="resetBtn" class="btn secondary">إعادة الاختبار</button>
    </div>
    <div class="right-controls">
      <div class="counter">إجابات صحيحة: <span id="summaryCount">0</span> / 68</div>
    </div>
  </div>

  <div class="main">
    <div class="quiz" id="quizColumn"></div>

    <aside class="side">
      <div class="small">شريط التقدم</div>
      <div class="progress"><i id="progressBar"></i></div>
      <div class="stats">
        <div class="stat-row"><span>الإجابات الصحيحة</span><strong id="statCorrect">0</strong></div>
        <div class="stat-row"><span>الأسئلة المبحوثة</span><strong id="statAnswered">0 / 68</strong></div>
        <div class="stat-row"><span>النسبة المئوية</span><strong id="statPercent">0%</strong></div>
      </div>
      <div style="height:14px"></div>
      <div class="small">تعليمات: اضغط على خيار للإجابة. سيظهر شرح داخل كل سؤال يوضح السبب. لا تُمنح نقاط على الخيارات الخاطئة.</div>
    </aside>
  </div>

  <div class="footer">بالتوفيق — عند رغبتك بإضافة مؤقت أو طباعة النتائج أخبرني.</div>
</div>

<!-- Overlay النتائج -->
<div id="overlay" class="overlay">
  <div class="panel">
    <h2>النتيجة النهائية</h2>
    <div class="score" id="finalScore">0 / 68</div>
    <div class="break" id="finalBreak">لم تقم بالإجابة بعد.</div>
    <button id="closeOverlay" class="btn secondary">حسناً</button>
  </div>
</div>

<script>
/* =============
   الأسئلة (68) — مُعدلة، والإجابات الصحيحة موزعة عشوائياً
   النمط: مصفوفة من الكائنات { q, choices, correct, explanation }
   ============= */

const questions = [
/* 1 */ { q: "موقف تربوي: أثناء نشاط مجموعة، يهيمن طالب ذو طابع قيادي على كل القرارات ويقمع آراء الآخرين. ما الإجراء التربوي الأكثر دقة لمعالجة هذا الموقف؟",
choices: ["تعيين أدوار واضحة وتدويرها دوريًا بين الأعضاء", "استبعاد الطالب من المجموعة لحدوث توازن", "إعطاءه مكافآت لتشجيعه على القيادة", "تجاهل السلوك لأن له نتائج إيجابية"],
correct: 2, explanation: "تدوير الأدوار يتيح فرص مشاركة متساوية؛ المكافآت أو الاستبعاد ليست حلولًا مستدامة."
},
/* 2 */ { q: "تقويم: وجد تحليل بنود الاختبار أن بنداً معيناً أثبت نسب خطأ عالية بشكل متكرر. ما التفسير الأكثر احتمالا؟",
choices: ["البند قد يكون مُصاغًا بشكل مُضلّل أو غامض", "المستوى العام للطلاب منخفض جدا", "الاختبار طويل جدا", "الطلاب لم يدرسوا المادة"],
correct: 0, explanation: "البند المربك يؤدي إلى نسبة أخطاء مرتفعة حتى عند كفاية الطلاب."
},
/* 3 */ { q: "لغة عربية: عند قياس فهم النص الأدبي، أي نوع سؤال يكشف عن مهارات التحليل الأكثر أمناً؟",
choices: ["أسئلة تفسير الدوافع والدلالات الأدبية", "أسئلة معجمية عن مرادفات الكلمات", "أسئلة عن معنى الجمل فقط", "أسئلة حفظية عن أسماء الشخصيات"],
correct: 3, explanation: "تحليل الدوافع والدلالات يكشف فهمًا أعمق؛ الأسئلة الحفظية أقل ملاءمة لقياس التحليل."
},
/* 4 */ { q: "موقف تربوي: طالب يعاني انخفاضًا ملحوظًا في الدافعية بعد فترة نجاح سابقة. ما السبب التربوي الأرجح؟",
choices: ["تغير في ظروف أو توقعات المدرسة/الأسرة أثر على دافعيته", "انخفاض مستوى ذكائه فجأة", "المعلم لم يلاحظ التغيير", "زيادة عدد الواجبات فقط"],
correct: 1, explanation: "التغيرات في البيئة أو التوقعات تفسر تراجع الدافعية غالبًا أكثر من تغيرات داخلية مفاجئة."
},
/* 5 */ { q: "رياضيات: في مسألة لفظية معقدة، الطلاب يطبقون صيغة خاطئة متكررة. ما الإجراء التدريسي الأكثر فاعلية؟",
choices: ["تحليل الخطأ المشترك مع الطلاب وربطه بمعنى الصيغة", "زيادة عدد المسائل للحل فقط", "تقديم الصيغة جاهزة دون تفسير", "تقييم الطلاب بعلامات أقل"],
correct: 2, explanation: "تحليل الخطأ وربط الصيغة بالمعنى يساعد على تصحيح الفهم."
},
/* 6 */ { q: "تخطيط: عند كتابة أهداف درس معرفية، أي صياغة تعتبر الأكثر ملاءمة لقياس مستوى أعلى وفق بلوم؟",
choices: ["صياغة هدف يتضمن 'يحلل' أو 'يقيّم' بدل 'يتذكر'", "صياغة هدف يتضمن 'يعيد' المحتوى", "صياغة هدف عام دون فعل قابل للقياس", "صياغة هدف طولي بدون نتيجة واضحة"],
correct: 0, explanation: "أفعال مثل 'يحلل' و'يقيّم' تقيس مستويات عليا من التفكير."
},
/* 7 */ { q: "إدارة صف: طالب يستمر بالمقاطعة المتعمدة أثناء الشرح. أي استراتيجية صفية قصيرة المدى أنجعها؟",
choices: ["تطبيق نظام إشارات غير لفظي لتصحيح السلوك مع توقعات واضحة", "اللوم أمام الصف لتثبيط السلوك", "زيادة الواجبات العقابية", "تجاهل السلوك تماما"],
correct: 3, explanation: "إشارات غير لفظية تقلل المقاطعات دون إحراج؛ العقاب أمام الصف أو التجاهل أقل فاعلية."
},
/* 8 */ { q: "تكنولوجيا تعليم: المعلم يود تعزيز التفاعل الإلكتروني، لكنه يلاحظ قلة مشاركة. ما التحسين الأكثر فعالية؟",
choices: ["تصميم أنشطة قصيرة تقيّم المشاركة وتمنح تغذية راجعة فورية", "إرسال مرجع طويل للقراءة قبل الدرس", "تقليل محتوى المنصة إلى مواد قارئة فقط", "فرض الحضور الإلكتروني دون أنشطة"],
correct: 1, explanation: "الأنشطة القصيرة مع تغذية راجعة فورية تشجع المشاركة الإلكترونية."
},
/* 9 */ { q: "تقويم: عند مقارنة اختبارين متتاليين لنفس الفئة ووجدت اختلافًا كبيرًا في المتوسط لصالح الاختبار الثاني، الاحتمال الأكثر مهنية؟",
choices: ["التدخل التعليمي أثر بوضوح وتحسّن أداء الطلاب", "خطأ في احتساب الدرجات في الاختبار الأول", "استخدام طريقة تصحيح مختلفة في الاختبار الثاني", "كل ما سبق قد يكون ممكنًا ويحتاج فحصًا"], 
correct: 3, explanation: "لا بد من فحص أسباب التغيير؛ قد تكون أسبابًا متعددة."
},
/*10*/ { q: "لغة عربية: طالب يكتب مقالا جيدا في المحتوى لكن أسلوبه غير منطقي من ناحية الانتقال بين الفقرات. ما نصيحة المنهجية الأنسب؟",
choices: ["تعليمه استخدام خرائط مفاهيم قبل كتابة المسودة", "زيادة سرعة الكتابة", "حذف فقرة كاملة", "التركيز على الإملاء فقط"],
correct: 0, explanation: "خرائط المفاهيم تساعد على تنظيم الأفكار وهي حل مباشر لمشكلة الانتقالات."
},

/*11*/ { q: "موقف تربوي: طالب يجيب إجابات صحيحة بسرعة لكن يخطئ في الأسئلة المعمقة. ما الدليل الأكثر احتمالا؟",
choices: ["الاعتماد على استراتيجية حل سريعة دون عمق معرفي", "ضعف في الرؤية", "مشكلة في اللغة فقط", "المعلم يعطي هامش خطأ كبير"],
correct: 2, explanation: "الإجابات السريعة قد تعكس حفظًا سطحيًا أو استراتيجيات سريعة بدون عمق." 
},

/*12*/ { q: "صعوبات تعلم: طالب يخلط بين الحروف المتشابهة ويقرأ ببطء، ما الإجراء التشخيصي الأول؟",
choices: ["إحالة لتقييم صعوبات تعلم متخصص لتحديد نوع المشكلة", "زيادة الواجبات الكتابية فقط", "تجاهل الأمر لأنه مؤقت", "تغيير المدرس مباشرة"],
correct: 1, explanation: "التقييم المتخصص يحدد وجود عسر القراءة أو أسباب أخرى."
},

/*13*/ { q: "رياضيات: طالب قادر على حل أمثلة مماثلة لكن يفشل في مسألة بمعلومات مختلفة. ما مهارة التفكير المطلوب تقويتها؟",
choices: ["مهارة التعميم ونقل الحلول إلى سياقات جديدة", "مهارة الحفظ الآلي للصيغ", "مهارة الرسم فقط", "مهارة السرعة في الحساب"],
correct: 2, explanation: "التعميم يساعد في تطبيق استراتيجيات الحل على حالات جديدة."
},

/*14*/ { q: "تخطيط: عند تصميم درس متباين، ما العنصر الذي يجب تضمينه أساسياً؟",
choices: ["مسارات تعلم بديلة بناءً على مستويات الطلاب واهتماماتهم", "تطبيق نفس النشاط على الجميع", "تقليل المواد للطلاب الضعيفين", "زيادة طول الحصة للجميع"],
correct: 0, explanation: "التمايز يتطلب مسارات ومواد مهيأة لتلبية الاحتياجات المتنوعة."
},

/*15*/ { q: "لغة عربية: ما السؤال الأنسب لقياس القدرة على 'الاستدلال' لدى الطالب من نص؟",
choices: ["لماذا يظن الكاتب أن... وما الدليل؟", "ما تعريف الكلمة؟", "كم عدد الفقرات؟", "هل النص مفيد؟"],
correct: 3, explanation: "السؤال يطلب استدلالًا مدعومًا بدليل من النص."
},

/*16*/ { q: "موقف تربوي: أثناء اختبار شفهي، طالب يتردد ويظهر توترًا شديدًا. ما الإجراء الحساس لتقليل التوتر؟",
choices: ["إعطاء وقت انتظار قصير وتشجيع بلطف وإعادة صياغة السؤال", "وضعه أمام الفصل كمثال", "مقاطعته وإعطاء درجة قليلة", "إكمال الامتحان نيابة عنه"],
correct: 1, explanation: "الانتظار والتشجيع يقللان الضغط ويسمحان للطالب بالإجابة بطلاقة."
},

/*17*/ { q: "تقويم: أي نوع من الصدق يقيس مدى توافق نتائج الاختبار مع مقياس خارجي في نفس الزمن؟",
choices: ["الصدق التلازمي", "صدق المحتوى", "صدق البناء", "الصدق التنبؤي"],
correct: 2, explanation: "الصدق التلازمي يقارن مقياسين في نفس الزمن لقياس نفس البناء."
},

/*18*/ { q: "تكنولوجيا: عند استخدام منصة تعليمية، ما المعيار الذي يرفع فعالية التغذية الراجعة؟",
choices: ["الاستجابة الفورية المفصلة وربطها بخطوات لتحسين الأداء", "تأخير التعليقات لوقت أطول", "التعليقات العامة دون شرح", "اعتماد التعليقات فقط على الدرجة"],
correct: 0, explanation: "التغذية الراجعة المفصلة والفورية توجه التعلم مباشرة."
},

/*19*/ { q: "رياضيات: ما أفضل طريقة لتقييم التفكير التركيبي لدى الطلاب في موضوع الجبر؟",
choices: ["مهمة تصميم مسألة جديدة تربط أكثر من مفهوم جبري", "اختبار اختيار من متعدد سريع", "إعطاء مسألة منقولة من الكتاب", "حفظ طرق الحل"],
correct: 3, explanation: "تصميم مسألة جديدة يختبر قدرة الدمج؛ الاختبارات النمطية أقل قدرة على ذلك."
},

/*20*/ { q: "لغة عربية: طالب يستخدم ألفاظًا مناسبة لكن تركيب الجملة غير سليم. أي مهارة نحسنها؟",
choices: ["التدريب على تراكيب نحوية وجمل انتقالية", "زيادة تكرار القراءة", "التركيز على المحادثة فقط", "الاكتفاء بالأسلوب الشخصي"],
correct: 1, explanation: "التدريب النحوي يعزز تركيب الجمل والانتقال بينها."
},

/*21*/ { q: "موقف تربوي: صف متعدد المستويات؛ بعض الطلاب يشعرون بالملل والبعض بالإرهاق. ما استراتيجية إدارة المحتوى؟",
choices: ["التعلم المتمايز بتوفير مهام تمديد وتسهيل", "تقليل وقت الحصة للجميع", "نقل الطلاب إلى صفوف متجانسة", "إلغاء الأنشطة الجماعية"],
correct: 2, explanation: "التمايز يمنح تحديًا للمتفوقين ودعمًا للضعفاء."
},

/*22*/ { q: "تقويم: أي مؤشر يبين أن الاختبار لديه ثبات جيد؟",
choices: ["اتساق النتائج عند إعادة التطبيق لنفس العينة", "ارتفاع المتوسط فقط", "سهولة البنود", "تنوع الأسئلة الكبير"],
correct: 0, explanation: "الثبات يعكس تناسق النتائج عبر مرات التطبيق أو أجزاء الاختبار."
},

/*23*/ { q: "صعوبات تعلم: طالب يواجه صعوبة في حل المشكلات بسبب ضعف التخطيط المسبق. ما الدعم المناسب؟",
choices: ["تعليم استراتيجيات التخطيط خطوة بخطوة واستخدام قوائم تحقق", "زيادة الواجبات دون إرشاد", "تعويم الطالب بمفرده", "اعتماده على زميله دائمًا"],
correct: 2, explanation: "قوائم التحقق واستراتيجيات التخطيط تحسن أداء حل المشكلات."
},

/*24*/ { q: "رياضيات: عند تصميم سؤال يقيس مهارة 'التفكير النقدي' في الهندسة، ما الصيغة الأنسب؟",
choices: ["اطلب من الطالب تقييم صحة استنتاج هندسي مقترح وتقديم برهانه", "اطلب فقط حساب محيط الشكل", "أسئلة حفظية عن النظريات", "سؤال حسابي بسيط"],
correct: 0, explanation: "تقييم استنتاج مع تقديم برهان يقيس التفكير النقدي."
},

/*25*/ { q: "لغة عربية: في تقويم الكتابة الإبداعية، ما الذي يعزز صدق التقدير؟",
choices: ["وجود معايير (rubric) واضحة ومشتركة بين المصححين", "كل مصحح يعطي حُكم خاص به", "التركيز على الطول فقط", "التصحيح العشوائي"],
correct: 1, explanation: "معايير واضحة تقلل التحيز وتزيد اتساق التقدير."
},

/*26*/ { q: "موقف تربوي: طالب يتجنب السؤال خوفًا من السخرية. ما التعديل الصفّي طويل المدى لرفع ثقته؟",
choices: ["بناء ثقافة صفية آمنة عبر قواعد واضحة وممارسات تشجيع", "فرض عقاب على من يسخر", "تجاهل الشكليات والتركيز على المادة", "إجبار الطالب على الكلام"],
correct: 3, explanation: "بناء ثقافة آمنة وتشجيع مستمر يطوّران الثقة لدى الطالب."
},

/*27*/ { q: "تقويم: ما معنى 'المعايرة' (calibration) في بنوك الأسئلة؟",
choices: ["تحديد خصائص البنود مثل الصعوبة والتمييز بناءً على تجارب سابقة", "تجميل صياغة الأسئلة فقط", "إخفاء مفردات صعبة عن الطلاب", "اختصار الاختبار"],
correct: 0, explanation: "المعايرة تتضمن تحديد خصائص البنود لتضمن ملاءمتها."
},

/*28*/ { q: "تكنولوجيا: أي استخدام للتقنية يعزز التفكير التوليدي لدى الطلاب؟",
choices: ["منصات تسمح بالعصف الذهني ومشاركة البدائل", "مواقع للتحميل فقط", "عرض شرائح ثابتة", "قنوات مسموعة فقط"],
correct: 0, explanation: "أدوات التبادل المفتوح تدعم إنتاج أفكار متعددة."
},

/*29*/ { q: "موقف تربوي: دورتك التدريبية تتضمن تقييمًا متعدد المصادر. ما سبب ميزته؟",
choices: ["يعطي صورة أكثر شمولًا عن أداء المعلم", "يبسط العملية بشكل مفرط", "يقلل من مصداقية التقييم", "يجعل التقييم بطيئًا فقط"],
correct: 1, explanation: "التقويم المتعدد يعطي صورة أوسع لكن يتطلب تنظيمًا جيدًا."
},

/*30*/ { q: "لغة عربية: عند قياس ملاءمة التعبير، أي عنصر يجب أن يكون في معيار التقدير؟",
choices: ["وضوح الأفكار وترابط الفقرات", "طول النص فقط", "وجود كلمات صعبة فقط", "وجود أخطاء إملائية فقط"],
correct: 0, explanation: "وضوح وترابط الأفكار هما مؤشران رئيسيان على جودة التعبير."
},

/*31*/ { q: "رياضيات: في تحليل نتائج اختبار، كيف تحدد أن بندًا ما يميّز بين الطلاب الضعفاء والمتفوقين؟",
choices: ["قياس معامل التمييز (item discrimination)", "فحص طول البند فقط", "عد عدد الكلمات", "التركيز على ترتيب الأسئلة"],
correct: 3, explanation: "معامل التمييز هو المعيار الإحصائي لتبيان قدرة البند على التمييز."
},

/*32*/ { q: "صعوبات تعلم: أي تعديل تعليمي مفيد لطلاب يعانون من ضعف الانتباه؟",
choices: ["تقسيم المهمة إلى خطوات قصيرة مع فترات راحة", "زيادة كمية المعلومات دفعة واحدة", "إطالة زمن الحصة فقط", "الاعتماد على الأقران فقط"],
correct: 0, explanation: "التجزئة وفترات الراحة تحسن التركيز والإنجاز."
},

/*33*/ { q: "موقف تربوي: طالب يعتمد على المعلم لحل كل مشكلة. ما استراتيجية لتعزيز الاستقلالية؟",
choices: ["تعليم استراتيجيات حل المشكلات وتشجيع التعلم الموجه نحو الذات", "حرمانه من المساعدة نهائيًا", "الانتظار ليتعلم لوحده", "التقليل من الواجبات"],
correct: 1, explanation: "تعليم استراتيجيات وتمارين تزيد من مهارات الاعتماد الذاتي."
},

/*34*/ { q: "تخطيط: أي عنصر يجعل خطة الدرس قابلة للتقييم بدقة؟",
choices: ["أهداف إجرائية واضحة وقابلة للقياس", "نص طويل دون أهداف", "أنشطة مفتوحة بلا معيار", "تركيز على الشكل أكثر من المضمون"],
correct: 0, explanation: "الأهداف الإجرائية تسمح بالقياس الموضوعي لنجاح الدرس."
},

/*35*/ { q: "لغة عربية: أي سؤال يختبر مستوى 'المقارنة' بين نصين؟",
choices: ["قارن بين وجهتي نظر الكاتبَين وما الدليل", "كم عدد الكلمات في النص", "اذكر مرادف كلمة", "هل النصان طويلان؟"],
correct: 3, explanation: "المقارنة تتطلب تحليل الفروق والدلائل بين النصين."
},

/*36*/ { q: "رياضيات: طالب يستخدم طريقة صحيحة لكنها بطيئة. ما نصيحة المعلم الأمثل؟",
choices: ["تعليمه خوارزمية أكثر كفاءة مع الاحتفاظ بالفهم", "تقليل زمن الاختبارات", "فرض استخدام طريقة أسرع دون شرح", "التخلي عن التقييم الزمني"],
correct: 0, explanation: "تعليم بدائل أسرع مع شرحها يحسن الكفاءة دون فقدان الفهم."
},

/*37*/ { q: "موقف تربوي: طلاب يتدخلون أثناء إجابة زميل، ما إجراء لتقليل التشويش دون كبت التفاعل؟",
choices: ["اتفاق قواعد مشاركة محددة واستخدام إشارات دورية", "ممنوع الكلام نهائيًا", "العقاب الجماعي عند أول تدخل", "إلغاء الأنشطة التشاركية"],
correct: 2, explanation: "اتفاق القواعد مع إشارات الحديث يحافظ على التفاعل والاحترام."
},

/*38*/ { q: "تقويم: عند رغبتك في قياس نمو الطالب عبر الزمن، ما نوع التقويم الأنسب؟",
choices: ["التقويم البنائي المتكرر وملفات الإنجاز", "اختبار نهائي مرة واحدة", "استبيان عام", "ملاحظة عابرة"],
correct: 0, explanation: "التقويم البنائي وملفات الإنجاز توضح التطور عبر الزمن."
},

/*39*/ { q: "تكنولوجيا: ما أفضل شكل لأنشطة إلكترونية تعزز التعاون الحقيقي؟",
choices: ["مشروعات تحرير مشترك ومراجعات متبادلة", "اختبارات فردية عبر الإنترنت", "مشاهدات فيديو منفردة", "قراءات بلا تبادل"],
correct: 0, explanation: "التحرير المشترك يعزز التشارك والمسؤولية المشتركة."
},

/*40*/ { q: "لغة عربية: عند تقييم الاستنتاج من نص، أي مؤشر يدل على قدرة الطالب؟",
choices: ["استدعاء استنتاجات مع دعم من أجزاء النص", "عدد الكلمات المستخدمة", "طول الفقرة الأولى", "وجود كلمات صعبة"],
correct: 3, explanation: "القدرة على ربط أجزاء النص لبناء استنتاج مدعوم هي العلامة الأساسية."
},

/*41*/ { q: "رياضيات: طالب يخطئ عند الانتقال من الرسم البياني إلى الصيغة الجبرية. ما التدريب المفيد؟",
choices: ["تمارين تربط الرسم بالصيغة تدريجيًا", "حذف التمثيل البياني", "التركيز على الحفظ", "تكرار أسئلة غير مترابطة"],
correct: 2, explanation: "تمارين الربط تساعد على الانتقال بين التمثيلات المختلفة."
},

/*42*/ { q: "موقف تربوي: بعض الطلاب يجيبون بطريقة ميكانيكية في الشفهي. ما الحل؟",
choices: ["تغيير صياغة الأسئلة لتطلب شرح العملية", "تكرار نفس الأسلوب دائمًا", "تسريع الشفهي", "تقليل الشفهي"], 
correct: 0, explanation: "الأسئلة التي تطلب العملية تُكشف عن الفهم الحقيقي."
},

/*43*/ { q: "تقويم: ما معيار يزيد من ثبات المصححين؟",
choices: ["تدريب المصححين والتوصل إلى اتفاق معياري قبل التصحيح", "السماح لكل مصحح بالطريقة التي يفضلها", "التصحيح العشوائي", "الاعتماد على مصحح واحد"], 
correct: 3, explanation: "التدريب والاتفاق القياسي يقللان فروق الحكم بين المصححين."
},

/*44*/ { q: "صعوبات تعلم: طالب يعاني ضعف التواصل الشفهي رغم فهمه الجيد. ما الدعم الأنجع؟",
choices: ["تدريبات مهيكلة على التعبير الشفهي مع نماذج", "زيادة العمل الكتابي فقط", "اعتماده على الأقران للتحدث", "تجاهل المشكلة"], 
correct: 1, explanation: "التدريب الممنهج والنماذج يبني قدرة الأداء الشفهي."
},

/*45*/ { q: "لغة عربية: عند إعداد سؤال يقيس 'الفهم الضمني' ماذا تطلب؟",
choices: ["استنباط المعنى غير المصرح به من دلائل النص", "معرفة تعريف الكلمات حرفي

ًا", "حساب عدد الأسطر", "قراءة سريعة فقط"], 
correct: 0, explanation: "الفهم الضمني يتطلب ربط دلائل النص لاستنتاج ما لم يذكر صراحة."
},

/*46*/ { q: "رياضيات: لماذا نبتعد عن بنود لها إجابة نمطية عند قياس التفكير؟",
choices: ["لأنها لا تقيس التفكير العميق", "لأنها أخف في التصحيح", "لأن الطلاب يفضلونها", "لأن المعلم لا يريد تنويع"],
correct: 0, explanation: "البنود المفتوحة أو التوليدية تطلب مهارات تفكير أعلى."
},

/*47*/ { q: "موقف تربوي: طلاب متفوقون يشعرون بالملل من أنشطة الصف. أي استراتيجية مناسبة لإشراكهم؟",
choices: ["تحديات امتدادية ومهام بحثية", "زيادة عدد الأسئلة البسيطة", "تقليل المشاركات", "استبعادهم من الأنشطة"],
correct: 3, explanation: "مهام امتدادية تمنح المتفوقين فرصًا للتعمق والاستكشاف."
},

/*48*/ { q: "تقويم: عند استخدام ملفات الإنجاز، ما الشرط الأساسي لفاعليتها؟",
choices: ["تنوع الأدلة ووضوح معايير التقييم", "أن تكون ملفاً كبيرًا فقط", "تنظيم بصري فقط", "احتواء أعمال محفوظة فقط"],
correct: 0, explanation: "تنوع الأدلة ومعايير واضحة يجعل ملف الإنجاز أداة قيّمة."
},

/*49*/ { q: "تكنولوجيا: ما معيار أمني مهم لمنصة تعليمية؟",
choices: ["تشفير البيانات وتفويض الوصول وسياسة خصوصية واضحة", "مشاركة معلومات الطلاب علنًا", "حفظ كل شيء بدون تشفير", "تسجيل دخول جماعي"],
correct: 1, explanation: "التشفير وسياسات الوصول تحمي بيانات الطلاب وتضمن الامتثال."
},

/*50*/ { q: "موقف تربوي: طالب ينجح في المنزل لكنه يفشل في الصف. أي فرضية تربوية تشرح ذلك؟",
choices: ["البيئة المنزلية مواتية أكثر للدعم", "المعلم غير كفء", "الواجب أسهل", "السياسة الصفية تميزه سلبًا"],
correct: 0, explanation: "المنزل قد يوفر موارد/هدوء/مساعدة تجعل الأداء أفضل."
},

/*51*/ { q: "لغة عربية: في تقويم القراءة النقدية، ما مؤشر الأداء؟",
choices: ["نقد موقف الكاتب وربط النص بقراءات أخرى", "تلاوة النص بسرعة", "تهجئة كلمات معقدة", "قراءة جهرية واضحة"],
correct: 2, explanation: "الربط والنقد يظهران قدرة التحليل النقدي."
},

/*52*/ { q: "رياضيات: تصميم بنود متوازنة يتطلب؟",
choices: ["مزج مستويات معرفية مختلفة (تذكر، فهم، تطبيق، تحليل)", "كل البنود على نفس المستوى", "إهمال التفكير العالي", "استخدام نفس الصيغة لكل بند"],
correct: 0, explanation: "تنويع المستويات يضمن تمييزًا أفضل بين الطلاب."
},

/*53*/ { q: "صعوبات تعلم: كيف تقيس تحسنًا بعد تدخل تخطيطي؟",
choices: ["مقارنة الأداء قبل وبعد باستخدام قوائم تحقق", "مراقبة الانفعالات فقط", "زيادة الأسئلة", "تغيير المعلم"],
correct: 2, explanation: "قوائم التحقق توفر مقياسًا موضوعيًا للتقدم."
},

/*54*/ { q: "موقف تربوي: طالب يقاوم التعلم لأنه لا يرى نتائج فورية. ما الإستراتيجية؟",
choices: ["تقسيم الأهداف إلى مكاسب قصيرة المدى واحتفال التقدم", "عقاب عند الفشل", "زيادة الواجبات", "تجاهل المقاومة"],
correct: 0, explanation: "الاحتفال بالتقدم القصير يشجع المثابرة."
},

/*55*/ { q: "لغة عربية: أي تمرين يرفع الاستدلال اللغوي؟",
choices: ["تحليل النص واستخراج الدلالات وربطها بالسياق", "حفظ النصوص", "الإنصات فقط", "تمارين إملائية فقط"],
correct: 2, explanation: "تحليل الدلالات يعزز القدرة على الاستدلال."
},

/*56*/ { q: "رياضيات: طالب يخطئ كثيرًا في نسب مئوية، ما النشاط العملي؟",
choices: ["أنشطة تطبيقية في سياقات واقعية", "زيادة التمارين النظرية", "حذف الموضوع", "اختبارات قصيرة"],
correct: 0, explanation: "التطبيق الواقعي يربط المفهوم بالاستخدام العملي."
},

/*57*/ { q: "تخطيط: كيف تتأكد من أن أهداف الوحدة متسقة مع مخرجات التعلم؟",
choices: ["مراجعة الأهداف وربط كل هدف بمؤشر قياس واضح", "كتابة عبارات عامة", "التركيز على الأنشطة", "تجاهل الإطار"], 
correct: 1, explanation: "الربط الواضح بالمؤشرات يضمن التوافق مع الإطار."
},

/*58*/ { q: "صعوبات تعلم: كيف تدعم طالبًا ذو صعوبات حسابية ومنخفض ثقة؟",
choices: ["دعم تدريجي ومهام ناجحة مع تغذية راجعة إيجابية", "العقاب عند الخطأ", "مهام صعبة فقط", "تجاهل الصعوبات"],
correct: 2, explanation: "المهمات القابلة للتحقيق تبني الثقة وتحسن الأداء."
},

/*59*/ { q: "موقف تربوي: لماذا لا يتجاوب الطلاب مع الأسئلة المفتوحة؟",
choices: ["غياب زمن الانتظار والتدريب على التفكير العميق", "كثرة الواجبات", "صعوبة اللغة", "ضعف تنظيم الصف"],
correct: 0, explanation: "زمن الانتظار والتدريب ضروريان لإجابات أعمق."
},

/*60*/ { q: "تقويم: أداة تتبع تقدم مجموعة صغيرة خلال فصل؟",
choices: ["خرائط التقدم وملفات الإنجاز", "اختبار نهائي فقط", "تقارير سنوية", "انطباع المعلم"], 
correct: 0, explanation: "الخرائط والملفات تقدم بيانات مستمرة ومفصلة."
},

/*61*/ { q: "لغة عربية: كيف تقيس إعادة الصياغة؟",
choices: ["تقييم ملخصات مكتوبة بمعايير الدقة والاقتصاد", "اختبارات اختيار من متعدد", "تقييم شفهي دون معايير", "حفظ نص مشابه"],
correct: 2, explanation: "المعايير الواضحة تسمح بتقييم موضوعي لإعادة الصياغة."
},

/*62*/ { q: "رياضيات: عند وجود تباين غير متوقع بين طالبين، تفحص أولًا؟",
choices: ["خطأ في التصحيح أو فهم السؤال", "ذكاء الطالب", "مستوى الصف", "وجود غش"],
correct: 0, explanation: "أخطاء التصحيح أو سوء الفهم غالبًا سبب فروق فردية."
},

/*63*/ { q: "تكنولوجيا: ميزة الواجبات المصححة آليًا؟",
choices: ["تصحيح فوري مع تغذية راجعة مفصلة", "تقليل تفاعل المعلم", "اعتماد الحلول الجاهزة", "إلغاء التقييم البشري"],
correct: 0, explanation: "التغذية الراجعة الفورية تدعم التعلم المستمر."
},

/*64*/ { q: "موقف تربوي: شكاوى أولياء الأمور عن عبء الواجب، كيف تتصرف؟",
choices: ["مراجعة العبء وربطه بأهداف واضحة وإعطاء توجيهات للمنزل", "زيادة الواجب", "الرد عليهم بأنهم مخطئون", "تجاهل الشكاوى"],
correct: 1, explanation: "مراجعة العبء وضبطه يحل المشكلة مهنياً."
},

/*65*/ { q: "صعوبات تعلم: كيف تقيس فعالية برنامج تدخل لغوي بعد 8 أسابيع؟",
choices: ["مقارنة مؤشرات الأداء قبل وبعد باستخدام اختبارات معيارية", "انطباع المعلم فقط", "زيادة المحتوى", "ملاحظة واحدة"],
correct: 2, explanation: "قياس موضوعي معياري يظهر أثر البرنامج."
},

/*66*/ { q: "تخطيط: ماذا يعني جعل النشاط قابلًا للقياس؟",
choices: ["وجود معيار واضح يسمح بالحكم على تحقيق الهدف", "تحديد زمن طويل", "قصر النشاط على فئة", "ترك التقييم للتخمين"],
correct: 0, explanation: "المعيار الواضح يسهل قياس مدى التحقق."
},

/*67*/ { q: "لغة عربية: أي سؤال يختبر التفكير النقدي في النص؟",
choices: ["ناقش نقاط القوة والضعف في موقف الكاتب مع اقتراح بدائل", "حدد اسم الكاتب", "اذكر عدد الفقرات", "اختر خيارًا"],
correct: 2, explanation: "نقد الموقف واقتراح بدائل مدعومة بالدلائل يقيس التفكير النقدي."
},

/*68*/ { q: "موقف تربوي: كمدير فصل، كيف توازن بين قواعد صارمة وبيئة محفزة؟",
choices: ["تبني قواعد واضحة مع مكافآت لتعزيز السلوك الإيجابي", "التركيز على العقاب لردع السلوك", "عدم وجود قواعد للسماح بالمرونة", "إقالة الطلاب المخالفين"],
correct: 1, explanation: "القواعد الواضحة مع التحفيز الإيجابي توازن بين النظام والدافعية."
}
]; // نهاية المصفوفة

/* =============
   إنشاء البطاقات والتفاعل
   ============= */

const quizColumn = document.getElementById('quizColumn');
const total = questions.length;

questions.forEach((Q, idx) => {
  const card = document.createElement('div');
  card.className = 'card';
  card.dataset.answered = '';
  card.dataset.index = idx;

  const head = document.createElement('div');
  head.className = 'q-head';
  head.innerHTML = `<div class="q-num">س ${idx+1}</div><div style="font-weight:700;color:var(--muted)">سؤال ${idx+1}</div>`;
  card.appendChild(head);

  const sent = document.createElement('div');
  sent.className = 'sentence';
  sent.innerHTML = Q.q;
  card.appendChild(sent);

  const choicesDiv = document.createElement('div');
  choicesDiv.className = 'choices';

  Q.choices.forEach((c, i) => {
    const btn = document.createElement('button');
    btn.className = 'choice';
    const labels = ['أ','ب','ج','د'];
    btn.innerHTML = `<div style="font-weight:800;display:inline-block;margin-left:8px">${labels[i]}</div> <div style="display:inline-block;vertical-align:top">${c}</div>`;
    btn.addEventListener('click', () => {
      if (btn.classList.contains('disabled')) return;
      Array.from(choicesDiv.children).forEach(x => x.classList.add('disabled'));
      if (i === Q.correct) {
        btn.classList.add('correct');
        card.dataset.answered = 'correct';
        showPopInline(card, `<strong style="color:var(--success)">إجابة صحيحة ✔</strong><div style="margin-top:6px">${Q.explanation}</div>`);
      } else {
        btn.classList.add('wrong');
        if (choicesDiv.children[Q.correct]) choicesDiv.children[Q.correct].classList.add('correct');
        card.dataset.answered = 'wrong';
        showPopInline(card, `<strong style="color:var(--danger)">إجابة خاطئة ✘</strong><div style="margin-top:6px">${Q.explanation}</div>`);
      }
      updateSummary();
    });
    choicesDiv.appendChild(btn);
  });

  card.appendChild(choicesDiv);
  quizColumn.appendChild(card);
});

/* Inline popup */
function showPopInline(card, html) {
  const old = card.querySelector('.pop');
  if (old) old.remove();
  const p = document.createElement('div');
  p.className = 'pop';
  p.innerHTML = html;
  card.appendChild(p);
  card.scrollIntoView({behavior:'smooth', block:'center'});
}

/* Summary */
const statCorrect = document.getElementById('statCorrect');
const statAnswered = document.getElementById('statAnswered');
const statPercent = document.getElementById('statPercent');
const summaryCount = document.getElementById('summaryCount');
const progressBar = document.getElementById('progressBar');

function updateSummary() {
  let correct = 0;
  let answered = 0;
  document.querySelectorAll('.card').forEach(c => {
    if (c.dataset.answered === 'correct') correct++;
    if (c.dataset.answered === 'correct' || c.dataset.answered === 'wrong') answered++;
  });
  statCorrect.textContent = correct;
  statAnswered.textContent = `${answered} / ${total}`;
  const percent = Math.round((correct / total) * 100);
  statPercent.textContent = `${percent}%`;
  summaryCount.textContent = `${correct}`;
  progressBar.style.width = `${Math.round((answered/total)*100)}%`;
  document.getElementById('finalScore').textContent = `${correct} / ${total}`;
}

/* Buttons */
document.getElementById('showAll').addEventListener('click', () => {
  updateSummary();
  const correct = Number(statCorrect.textContent);
  const panelBreak = document.getElementById('finalBreak');
  const overlay = document.getElementById('overlay');
  const totalQ = total;
  if (correct === totalQ) panelBreak.innerText = 'ممتاز — إجابات جميعها صحيحة!';
  else if (correct >= Math.ceil(totalQ * 0.85)) panelBreak.innerText = 'ممتاز جداً — أداء متقدم!';
  else if (correct >= Math.ceil(totalQ * 0.7)) panelBreak.innerText = 'جيد جدًا — أداء قوي';
  else if (correct >= Math.ceil(totalQ * 0.5)) panelBreak.innerText = 'متوسط — يحتاج مراجعة مركزة';
  else panelBreak.innerText = 'ضعيف — أنصح بمراجعة الأساسيات والتدريب المكثف';
  overlay.style.display = 'flex';
});

document.getElementById('closeOverlay').addEventListener('click', () => {
  document.getElementById('overlay').style.display = 'none';
});

document.getElementById('resetBtn').addEventListener('click', resetExam);

function resetExam() {
  document.querySelectorAll('.card .pop').forEach(p => p.remove());
  document.querySelectorAll('.card').forEach(card => {
    card.dataset.answered = '';
    card.querySelectorAll('.choice').forEach(btn => {
      btn.classList.remove('disabled','correct','wrong');
    });
  });
  updateSummary();
  window.scrollTo({top:0, behavior:'smooth'});
}

/* Init */
updateSummary();
</script>
</body>
</html>

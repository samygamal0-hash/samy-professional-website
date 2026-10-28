# إعداد ربط Google Calendar للحجوزات

## الحالة الحالية
الموقع الحالي صفحة HTML ثابتة فقط. لا يوجد Backend أو قاعدة بيانات أو مصادقة إدارية أو Google OAuth، لذلك لا يمكنه جلب المواعيد أو حفظ طلب الحجز أو إضافة أحداث إلى التقويم. واجهة النموذج تتحقق من التاريخ وتعرض مدة الجلسة كمعلومة ثابتة. بعد إعداد رقم واتساب العام، تفتح مسودة طلب يراجعها العميل ويرسلها بنفسه؛ الموقع لا يحفظها ولا يرسلها تلقائيًا. لا توجد قائمة مواعيد متاحة ولا تقويم تجريبي أو تأكيد مزيف.

## ما يلزم قبل الربط الفعلي
1. اختيار استضافة تدعم Backend مع HTTPS، وقاعدة بيانات خاصة مع نسخ احتياطي واستعادة. تحفظ طلبات الحجز والحالات ومعرّف حدث Google في قاعدة البيانات فقط، خارج الملفات العامة.
2. إنشاء مشروع في Google Cloud Console وتفعيل Google Calendar API. إعداد شاشة موافقة OAuth ونوع المستخدم/حساب الاختبار.
3. إنشاء OAuth Client من نوع Web application. إضافة callback URL للخادم حرفيًا إلى Authorized redirect URIs. لا تضع Client Secret في HTML أو JavaScript عام.
4. تنفيذ OAuth Authorization Code على الخادم مع state عشوائي والتحقق منه. اطلب أقل صلاحيات مناسبة: calendar.events.freebusy لفحص الانشغال وcalendar.events.owned لإنشاء أحداث على تقويم تملكه، أو راجع الصلاحية المكافئة وفق نوع التقويم والحساب. احتفظ بالـ refresh token مشفرًا في مخزن آمن على الخادم، واستخدمه لتجديد access token. لا ترسله إلى المتصفح.
5. تحديد تقويم Google، حساب المالك، ساعات العمل، الأيام المتاحة، فواصل الجلسات، مهلة الحجز المسبق، والإجازات/الإغلاقات. لم تُحدد ساعات متاحة بعد، لذا لن يعرض الموقع أوقاتًا من عنده.
6. عند عرض المواعيد، يحسب الخادم الخيارات من جدول التوافر المعتمد ويستعلم عن busy periods عبر FreeBusy بالمنطقة الزمنية Africa/Cairo. عند الموافقة، يعيد فحص التعارض مباشرة قبل الحفظ وإنشاء الحدث لمنع سباق الحجز. يحسب وقت النهاية من مدة الجلسة ويستخدم idempotency لمنع تكرار الحدث.
7. أنشئ الحدث عند تأكيد سامي للموعد فقط. استخدم عنوانًا عامًا مثل Psychology session بلا اسم عميل أو وسيلة اتصال أو تفاصيل نفسية، ووصفًا فارغًا. خزّن Google event ID في سجل خاص، وأرسل رسالة تأكيد فقط بعد نجاح الحفظ وإنشاء الحدث. عالج فشل أي خطوة بوضوح.
8. أضف صفحة إدارة مؤمنة لإقرار/رفض الطلبات وتأكيد وقتها، وقاعدة بيانات خاصة بأقل بيانات لازمة، وسياسة حذف واحتفاظ، وتحديد معدل، وحماية CSRF والجلسات، والتحقق الخادمي من الحقول والتعارضات.

## متغيرات البيئة المطلوبة لاحقًا
انسخ الأسماء من .env.example إلى بيئة الخادم بعد إنشاء التطبيق. الملف الحالي يحتوي فراغات توضيحية فقط. لا تحفظ ملف أسرار داخل outputs أو ترفعه للمستودع.

## إعداد Google Cloud المقترح
- أنشئ مشروعًا في Google Cloud Console وفعّل Google Calendar API.
- جهّز OAuth consent screen وأضف حساب المالك كـ test user أثناء الاختبار إذا كان التطبيق في وضع Testing.
- Credentials ثم Create Credentials ثم OAuth client ID ثم Web application. أضف redirect URI للخادم؛ ليس مسار ملف محلي.
- اختبر OAuth وفحص Busy وإنشاء حدث اختباري عام في تقويم اختبار مخصص، وتحقق من البداية والنهاية والمنطقة الزمنية ومنع التكرار. لا تستخدم بيانات عميل حقيقية.
- قبل الإنتاج، راجع متطلبات Google الحالية للتحقق من التطبيق ونطاقات Calendar.

## مراجع Google الرسمية
- [OAuth 2.0 for Web Server Applications](https://developers.google.com/identity/protocols/oauth2/web-server)
- [Choose Google Calendar API scopes](https://developers.google.com/workspace/calendar/api/auth)
- [FreeBusy query](https://developers.google.com/workspace/calendar/api/v3/reference/freebusy/query)
- [Create Calendar event](https://developers.google.com/workspace/calendar/api/v3/reference/events/insert)
- [Calendar event time zones](https://developers.google.com/workspace/calendar/api/concepts/events-calendars)

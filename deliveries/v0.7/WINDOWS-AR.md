# تشغيل تحديث مركز الصحة 0.7 على Windows

التحديث يستخدم حزم الخادم المعزولة والكاش الذي استُعمل في 0.6. لا يلزم npm install أو تحديث Flutter أو Gradle أو Java. يحتفظ مسار runtime/v06 باسمه ليتوافق مع أوامر التشغيل القائمة؛ الإصدار داخله 0.7.

## تثبيت ملفات التحديث وترقية البيانات

أوقف خادم Node وFlutter بـCtrl+C من نافذتيهما. أبقِ Docker وCHR يعملان. فك الحزمة في `D:\copilot-update-v07`، ثم:

```powershell
node "D:\copilot-update-v07\install.cjs" "D:\NetWork-Ai"
cd "D:\NetWork-Ai"
node ".\runtime\v06\scripts\upgrade-health-foundation.mjs"
```

ينشئ أمر الترقية `before-health-….ncbak` مشفرًا داخل المجلد الخاص ثم يضيف جدولَي الفحص. احتفظ به وبـbackup-v1.key في مكان محمي. لا ترفع ملف النسخة أو المفتاح إلى المحادثة أو المستودع. عند وجود مخطط الإصدار الجديد تكون إعادة أمر الترقية آمنة. تعارض ملف محلي يوقف المثبت قبل كتابة أي ملف؛ يُراجع الملف المتعارض بدل مسح تغييراتك.

## تشغيل الخادم والويب

النافذة الأولى:

```powershell
cd "D:\NetWork-Ai"
node --use-env-proxy --env-file=.env ".\runtime\v06\dist\server.js" --foundation
```

نافذة ثانية:

```powershell
cd "D:\NetWork-Ai\apps\mobile"
flutter --suppress-analytics --no-version-check run -d web-server --no-pub --no-web-resources-cdn --web-hostname 127.0.0.1 --web-port 52100
```

افتح `http://127.0.0.1:52100`. صفحة صحة الخادم هي `https://127.0.0.1:3443/healthz`. خيار no-web-resources-cdn يستخدم موارد رسم Flutter المحلية أثناء التطوير. يلزم إعادة تشغيل خدمة الويب لتطبيق index.html والأيقونات الجديدة.

## بناء الهاتف من كاش Gradle المعروف

هذه خطوة بناء محلي باستعمال Java وAndroid SDK الموجودين، وبنفس توقيع debug على جهازك. لا تحذف التطبيق من الهاتف أو تنظف الكاش.

```powershell
$copilotGradleHome = if ($env:GRADLE_USER_HOME) {
    $env:GRADLE_USER_HOME
} else {
    Join-Path $env:USERPROFILE ".gradle"
}
$copilotGradle = Get-ChildItem -LiteralPath (Join-Path $copilotGradleHome "wrapper\dists\gradle-9.3.1-all") -Filter "gradle.bat" -File -Recurse | Select-Object -First 1
if ($null -eq $copilotGradle) { throw "لم أجد Gradle 9.3.1 في الكاش المعروف." }
$copilotGradleArgs = @(
    '--offline', '--console=plain', '--no-daemon',
    '-Ptarget-platform=android-arm64',
    '-Pandroid.builder.sdkDownload=false',
    '-Dorg.gradle.java.installations.auto-download=false',
    '-PcopilotVersionName=0.7.0', '-PcopilotVersionCode=7',
    '--project-dir', 'D:\NetWork-Ai\apps\mobile\android', 'assembleDebug'
)
& $copilotGradle.FullName @copilotGradleArgs
if ($LASTEXITCODE -ne 0) { throw "توقف البناء؛ راجع رسالة الخطأ قبل أي تنزيل." }
```

تحدّث خصائص copilotVersionName/Code رقم APK عند البناء المباشر دون تعديل local.properties أو تنزيل Gradle آخر. إن نقص عنصر من الكاش، تحدد رسالة الخطأ العنصر المطلوب قبل أي محاولة تنزيل.

بعد BUILD SUCCESSFUL، والهاتف متصل ومصرّحًا له عبر USB:

```powershell
$copilotAdb = Join-Path $env:LOCALAPPDATA "Android\Sdk\platform-tools\adb.exe"
& $copilotAdb -d install -r "D:\NetWork-Ai\apps\mobile\build\app\outputs\flutter-apk\app-debug.apk"
if ($LASTEXITCODE -ne 0) { throw "توقف التثبيت؛ أرسل رسالة النتيجة." }
& $copilotAdb -d reverse tcp:3443 tcp:3443
& $copilotAdb -d shell am start -n "app.networkcopilot.mobile/.MainActivity"
```

أعد أمر reverse بعد فصل USB وإعادته. يستخدم الهاتف خادم الكمبيوتر بشهادته المعتمدة. إعداد تطبيق المصادقة الحالي يستمر؛ عند طلب رمز، استخدم الرمز الحديث نفسه للحساب، دون إنشاء إعداد جديد.

## تجربة الوظيفة

1. افتح الراوتر من الأجهزة؛ يظهر مركز الصحة. ابدأ فحصًا وانتظر النتيجة الفعلية.
2. راجع التغطية، وافتح دليل خدمة إدارة أو موارد. المتوقع أن يكون اختبار الإنترنت غير متاح ضمن الحساب الحالي، مع سبب واضح.
3. عرّف الأدوار والروابط المطلوبة وفق شبكة المختبر، ثم أعد الفحص. افتح الواجهات والسرعات وتحقق من الفرق بين غير متاح وصفر مقاس.
4. حدد تقريرين من السجل وقارن القيم والحالات. جرّب الإلغاء أثناء جمع العينات، ثم بدء فحص جديد.
5. اختبر انقطاع خادم التطبيق ثم عودته: تظهر رسالة واضحة ووقت التقرير السابق. لا تتحول القراءة القديمة إلى حالة اتصال حي.
6. راجع أول تشغيل بارد على الهاتف والويب في المظهرين، والعودة من الخلفية، وتقليل الحركة. هذه هي خطوة قبول الانتقال البصري على الجهاز الفعلي.
7. راجع مستخدمًا محدود الصلاحيات: يرى التقارير المسموحة فقط؛ المراقب لا يبدأ فحصًا ولا يرسل شرح AI. استكمل أيضًا رفض شهادة غير موثوقة وجلسة Hotspot نشطة في المختبر ضمن البنود الميدانية المتبقية.

## الرجوع

أوقف الخادم والويب أولًا. مسار نسخة الكود يطبعه المثبت، ويكون تحت `.copilot-update-backups\health-v07-…`. يمكن مراجعة الخطة ثم تشغيل:

```powershell
node ".\scripts\rollback-foundation-update.cjs" "D:\NetWork-Ai" "مسار نسخة الكود التي طبعها المثبت"
```

إذا لم تبدأ ترقية قاعدة البيانات، يكفي الرجوع عن الكود. إذا تمت الترقية إلى المخطط 2، لا يشغّل كود 0.6 المخطط الجديد. بعد رجوع الكود، استعمل أمر restore-foundation الموجود في runtime القديم لاستعادة ملف before-health إلى **قاعدة منفصلة**، ثم اختر ملف إعداداتها المطبوع كما في تجربة الاستعادة السابقة. لا تُخفض المخطط داخل قاعدة التشغيل ولا تحذفها. تبقى قاعدة 0.7 محفوظة؛ الجلسات في قاعدة الاستعادة تحتاج تسجيل دخول جديدًا.

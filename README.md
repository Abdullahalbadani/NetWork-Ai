# Network Copilot 0.7 — مركز صحة الشبكة

تحديث للمشروع القائم على Foundation 0.6: فحص RouterOS عند الطلب، دليل وتوصية لكل نتيجة، قياس RX/TX من عينات، إلغاء، سجل ومقارنة تقريرين، وشرح AI اختياري بعد المعاينة. هوية كحلية وسماوية وافتتاحية شبكية مشتركة للهاتف والويب. بيانات صور المعاينة اختبارية؛ القياس داخل التطبيق يُقرأ من الراوتر.

[تنزيل حزمة 0.7](deliveries/v0.7/copilot-health-v0.7.zip) — نحو 1.1MB.

[دليل التحديث والتشغيل والهاتف والرجوع](deliveries/v0.7/WINDOWS-AR.md) · [نتائج التحقق وحدودها](deliveries/v0.7/VALIDATION-AR.md) · [التحقق المنظم وبصمة الملف](deliveries/v0.7/validation.json)

ZIP SHA256:

```text
34d19dbea9609d29634126743105815d99e0f08380513088424117ed8e4e3236
```

أوقف Node وFlutter، وأبقِ Docker وCHR يعملان. فك ZIP في D:\copilot-update-v07 ثم نفّذ في PowerShell:

```powershell
node "D:\copilot-update-v07\install.cjs" "D:\NetWork-Ai"
cd "D:\NetWork-Ai"
node ".\runtime\v06\scripts\upgrade-health-foundation.mjs"
```

ينشئ أمر الترقية نسخة بيانات مشفرة قبل إضافة جدولَي الفحص. المثبّت يحتفظ بنسخة الكود، ويحفظ الملفات الخاصة، ويرفض التعديل المحلي المجهول قبل الكتابة. لا تعِد إنشاء المالك أو إعداد المصادقة، ولا تمسح تطبيق الهاتف. لا تحتاج npm install أو تحديث أدوات التطوير؛ بناء الهاتف من الكاش القائم موثق في الدليل، وتثبيته يستخدم adb install -r.

نجح 84 اختبار خادم و51 اختبار Flutter دون تخطٍ، وفحص التحليل، وترقية واستعادة ورجوع مختبري بقاعدة PostgreSQL فعلية، وتجربة حزمة التسليم على نسخ 0.6 و0.6.1 والإصلاح المعروف. تحقق Android شمل الموارد وإعداد Gradle offline؛ لم يُبنَ APK كامل في السحابة. قبول Windows وCHR والافتتاحية على الهاتف الفعلي ما زال مطلوبًا. اختبار الإنترنت غير متاح ضمن صلاحية القراءة الحالية؛ لا يُستنتج من اتصال الكمبيوتر. لم يُنشر خادم عام.

---

# Network Copilot 0.6 delivery

This branch contains the tested update package for the existing Windows project at `D:\NetWork-Ai`. It is a code delivery package.

Archive: [copilot-foundation-v0.6.zip](deliveries/v0.6/copilot-foundation-v0.6.zip)

ZIP SHA256:

```text
d36e82adb40155a3574cf918d418ffdc611c66046f557817a3240caaf055dcdd
```

1. Download the archive with GitHub's download button and save it to your desktop.
2. Stop the existing Flutter process and Node server.
3. Verify the ZIP hash, then extract into a new folder, for example `D:\copilot-update-v06`.
4. Run `node "D:\copilot-update-v06\install.cjs" "D:\NetWork-Ai"`.
5. Keep the printed code backup path. Follow `D:\NetWork-Ai\docs\foundation-windows.md` for Docker, owner setup, TOTP, certificates, CHR import, Chrome and USB Android testing.

The installer validates the unchanged frozen update, refuses unknown file edits and preserves private configuration. It does not start services.

The archive contains source updates, a portable Node runtime and new Flutter cache packages. No user credentials, `.env`, Google API key, private configuration or router passwords are included.

Backend tests: 61 passed. Flutter tests: 33 passed. Physical Windows/CHR/Gemini/Android acceptance remains required. The cloud APK build was blocked by an HTTP 403 policy denial for a Flutter dependency.

## Setup diagnostics update 0.6.1

A small tested setup-diagnostics update is in `deliveries/v0.6/copilot-setup-diagnostics-v0.6.1.zip`.

ZIP SHA256: `329b0f2b793607c0c30c7d26e0bbe825830abcd07de19d21596c56ff3e9540ad`

Extract into `D:\copilot-setup-diagnostics-v061` and run `node "D:\copilot-setup-diagnostics-v061\install.cjs" "D:\NetWork-Ai"`. Then retry normal owner setup. Send only the bounded `Setup diagnostic:` line if it fails.

This update reports setup stage and known error/exit codes without raw error messages or private state. Windows private-directory grants use numeric token/SYSTEM SIDs. The root cause on the actual Windows computer is still being diagnosed. The update preserves private files and does not start or alter Docker containers while applying.

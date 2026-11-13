# إصلاح واجهة Network Copilot — UI R2

تصحيح صغير فوق إصدار 0.8.0 المثبّت بواسطة حزمة integration R1. يغيّر ملفي operations_screen.dart وoperations_test.dart فقط لإصلاح التفاف النص وتنظيف مؤقت الحساب في الاختبارات قبل تحقق Flutter. لا يغيّر قاعدة البيانات أو الحسابات أو MFA أو التوقيع أو الخادم أو موارد الافتتاحية.

الحزمة: network-copilot-operations-ui-r2-20261113.zip
الحجم: 32374 بايت
SHA256: 6106956b380389f232de168a0e8b23a2eba1f213863f20e49f3f36985c2f9473

نجحت 11 حالة للمثبّت من ZIP المستخرج، بما فيها التكرار ورفض التعارض وحفظ الملفات الخاصة والرجوع وفشل كتابة محقون. نجح فحص قواعد Dart؛ اختبارات Flutter الجديدة وبناء APK لم يُنفّذا هنا ويحتاجان بيئة المالك.

استخرج ZIP بالكامل في D:\copilot-ui-r2، ثم نفّذ في PowerShell:

```powershell
node "D:\copilot-ui-r2\install.cjs" "D:\NetWork-Ai"
if ($LASTEXITCODE -ne 0) { throw "توقف التصحيح؛ أرسل الخطأ." }

cd "D:\NetWork-Ai\apps\mobile"
& "D:\flutter\bin\flutter.bat" --no-version-check test --no-pub test/operations_test.dart
if ($LASTEXITCODE -ne 0) { throw "توقف؛ أرسل سجل الاختبار." }
```

بعد نجاح الاختبار المحدد، شغّل verify-client.ps1 وفق README_AR.md المرفق. ابنِ الهاتف بواسطة build-phone.ps1 بعد نجاح التحقق الكامل؛ يستخدم Gradle 9.3.1 الموجود في الكاش وadb install -r والتوقيع القائم. لا يُطلب تنزيل تبعيات جديدة.

يحفظ المثبّت نسخة الملفين الأصليين ويطبع مسارها. الرجوع بواسطة rollback.cjs للحزمة نفسها ومسار نسخة R2 فقط، وفق README_AR.md. يمكن إبقاء الخادم يعمل أثناء التصحيح.

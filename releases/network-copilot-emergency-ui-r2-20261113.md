# تصحيح فحص Flutter لواجهة الطوارئ R2

تحديث صغير فوق Network Copilot 0.8.1+9، مخطط 4. يصلح ثلاث ملاحظات use_null_aware_elements واستيراد dart:typed_data الزائد، في ملفي emergency_home.dart وemergency_incident.dart فقط. تبقى تصفية القيم null كما كانت.

حجم ZIP: 31,228 بايت.
SHA256: c19529a406a3d10d66bb4fce6501cfa8fafebf3e8b92f1beade69c2ecab38a66

استخرج محتويات ZIP إلى D:\copilot-emergency-ui-r2، ثم:
```powershell
node "D:\copilot-emergency-ui-r2\install.cjs" "D:\NetWork-Ai"
if ($LASTEXITCODE -ne 0) { throw "توقف؛ أرسل رسالة المثبت." }
powershell -NoProfile -ExecutionPolicy Bypass -File "D:\copilot-emergency-ui-r2\test-chrome.ps1" -ProjectRoot "D:\NetWork-Ai"
```

اترك Node HTTPS على 3443 في نافذته. أوقف عملية Flutter القديمة على 52100 إن وجدت. السكربت يستخدم SDK والكاش الموجودين، ويشغّل pub get --offline ثم analyze ثم test، ويتوقف عند الفشل دون تجاهل الملاحظات. عند النجاح يبدأ الويب؛ افتح http://127.0.0.1:52100 في Chrome بحسابك الحالي وTOTP. لا يحتاج ذلك USB.

نجحت هنا 12 مجموعة لاختبار المثبت، ثم التثبيت وإعادة التثبيت والرجوع من ZIP المستخرج على نسخة معزولة من آخر خط أساس مؤكد. نجح فحص قواعد Dart للملفين بواسطة tree-sitter المخزن. لم يُشغّل Flutter analyze/test/build أو PowerShell أو Chrome هنا لعدم وجود SDK وPowerShell، ويُعاد التحقق فعليًا على جهاز المستخدم. قبول الهاتف والراوتر الفعلي مؤجل.

لا تغيير للخادم المجمّع أو مخطط PostgreSQL أو الحسابات أو MFA أو الإعدادات أو التوقيع أو الكاش أو الافتتاحية. لا تنزيل تبعيات أو كتابة إلى الراوتر. المثبت يتحقق من البصمات والتوافق، يرفض التعديلات المحلية المجهولة ويحفظ الأصلين، ويدعم التكرار. دليل عربي وتقرير اختبارات وبصمات وطريقة الرجوع داخل ZIP. النشر مخصص لتسليم الحزمة وفق طلب المستخدم، دون تعديل الفرع الافتراضي.

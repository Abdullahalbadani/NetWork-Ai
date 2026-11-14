# تصحيح التحقق من بروفايلات مختبر CHR — R1

نجحت إضافة عناصر المختبر حسب نتيجة المستخدم، ثم رفض تحقق V1 بروفايلًا تطابق خصائصه المطبوعة الإعدادات المتوقعة. يصحح R1 مقارنة حقول السكربتات بتحويلها إلى نص، ويحدد الخاصية المخالفة بدل الرسالة العامة. السبب الدقيق للرفض السابق ونجاح R1 على RouterOS ما زالا يحتاجان التحقق على جهاز المستخدم.

بعد فك الحزمة، ارفع 02-ncp-verify-r1.rsc فقط إلى Files ثم نفذ:

```routeros
/import file-name="02-ncp-verify-r1.rsc"
```

ملف التحقق للقراءة فقط. لا تُعد تشغيل الإضافة أو التنظيف في هذه الخطوة. بقيت أوامر الكتابة والقيود وعناصر المختبر كما هي، مع المقارنات المصححة في نسختي الإضافة والتنظيف للاستخدام اللاحق.

فحوصات التوليد ونطاق الأوامر ومقارنة أوامر الكتابة وتوازن الأقواس وسلامة ZIP وبصمات الملفات نجحت هنا. لم يُشغل مفسر RouterOS أو R1 على الراوتر من بيئة المحادثة.

ZIP: 8916 bytes
SHA256: e61b074fafa289ac8c44d967f77edd1821daa40316d35b89a5edd9e4cf58651c

Publication uses the owner's existing explicit approval for public delivery of these lab IPs, ports and RouterOS scripts. Only this ZIP and release metadata are added on a dedicated delivery branch. Project source, main, private configuration and live router settings are not modified by publication.

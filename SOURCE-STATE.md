# وضعیت سورس، شاخه‌ها و APKها

## مرجع‌های آنلاینِ بررسی‌شده در ۲۰۲۶-۰۹-۲۵

| مرجع | SHA | معنای قابل اتکا |
| --- | --- | --- |
| `mohseniamin64-cmd/SMS_Gate:main` | `474bf21b2b8277305ce4c7915216b6defeb31dcf` | سورس آنلاین فعلی: HTTPS Phone Server پورت ۳۰۳۰، Room v4، UI و backend تماس |
| `codex/phone-server-architecture` | `42aa04aebef36d7e6057fc42ab9bfa776beb31cd` | شاخهٔ تاریخی Phone Server؛ از main فعلی عقب‌تر |
| `codex/mvp-integration` | SHA فعلی در این بررسی واکشی نشده | شاخهٔ MVP قبلی؛ قبل از استفاده SHA آن را آنلاین بگیر |
| این Knowledge Base `main` | SHA آخرین commit را از GitHub بخوان | فقط مستندات؛ کد Android در این مخزن نیست |

مسیرهای اصلی سورس: `app/src/main/java/com/example/`، `backend/`، `docs/PHONE_SERVER_API.md`، `PROJECT_ROADMAP.md` و `.github/workflows/android-ci.yml`.

## نسخهٔ محلی/نصب‌شده

در گفت‌وگو از rebuild محلی بر پایهٔ `capcom6/android-sms-gateway@b179de87dac3bf26043edeccfd6a94cdd67b215e` با شاخهٔ محلی `rebuild/local-first` و commit `9e62d38` گزارش شده بود. مسیر محلی گزارش‌شده روی ویندوز قبلی:

`C:\Users\Amin_PC\Documents\Codex\2026-09-02\sms-center-phone-server-implementation\outputs\SMS_Gate-local-3030-tls-fix.apk`

SHA-256 گزارش‌شدهٔ این APK: `6BE83A238ECE07CFFC3A6F96B472D821A063FF7BD28085975C7BFDE8A56E8FD6`. این داده **گزارش تاریخی** است؛ فایل محلی در این بکاپ نیست و روی GitHub release تأیید نشده. قبل از انتساب APK نصب‌شده به آن، hash فایل نصب‌شده و package name را دوباره بررسی کنید.

## اختلاف کلیدی

کاربر در Firefox صفحهٔ «SMS Gate Local Server is running» را در `https://192.168.1.27:3030/` دید. در `PhoneHttpServer.kt` آنلاینِ `main@474bf21`، route ریشه وجود ندارد و همهٔ endpointها auth می‌خواهند. بنابراین **نسخهٔ مشاهده‌شده و سورس main را یک build واحد فرض نکنید**. هر تغییر transport/UI باید روی سورس انتخاب‌شده انجام و با APK همان commit تست شود.

## فرمول بررسی نسخه

1. SHA شاخهٔ GitHub را بگیر.
2. وضعیت CI همان SHA را بخوان.
3. APK خروجی را با SHA-256 ثبت کن.
4. package/applicationId و version را با گوشی تطبیق بده.
5. فقط نتیجهٔ آزمایش همان APK را به آن commit نسبت بده.

# SMS Gate Knowledge Base

این مخزن، دفتر فنی و راهنمای بازیابی پروژهٔ **SMS Center / SMS Gate** است. سورس اصلی در [SMS_Gate](https://github.com/mohseniamin64-cmd/SMS_Gate) نگهداری می‌شود. اینجا جایگزین سورس یا دادهٔ گوشی نیست؛ مرجع تصمیم‌ها، معماری، خطاها و مراحل بازسازی پس از حذف چت یا تعویض ویندوز است.

## هدف

گوشی Android باید خودش درگاه پیامک و سرور محلی باشد. رایانه یا پنل وب در همان شبکهٔ LAN به IP و پورت گوشی وصل می‌شود، پیامک‌ها و گزارش تماس را می‌خواند و درخواست ارسال پیامک را به گوشی می‌دهد. خواندن و حذف پیام‌ها باید با وضعیت واقعی Android SMS Provider سازگار باشد. کاربر نهایی باید با کمترین دانش شبکه بتواند وضعیت اتصال را ببیند.

## وضعیت در زمان ثبت این بکاپ — ۲۰۲۶-۰۹-۲۵

| موضوع | وضعیت مستند |
| --- | --- |
| سورس آنلاین | `mohseniamin64-cmd/SMS_Gate`، شاخهٔ `main`، commit `474bf21b2b8277305ce4c7915216b6defeb31dcf` |
| سرور گوشی در این commit | HTTPS با گواهی self-signed، پورت پیش‌فرض ۳۰۳۰، API محافظت‌شده |
| پنل قدیمی Flask | مسیر جدا و اختیاری؛ `backend/app.py` آنلاین فعلاً فقط Call Log API مستقل دارد |
| نسخهٔ نصب‌شده روی گوشی | نسخهٔ محلی/آزمایشی با صفحهٔ راهنمای عمومی مشاهده شده؛ **برابر بودن آن با main اثبات نشده** |
| پیشنهاد HTTP پیش‌فرض | درخواست جدید کاربر، **هنوز در سورس آنلاین اجرا نشده** |
| کیفیت | Build و تست‌های خودکار قبلاً موفق گزارش شده‌اند؛ تأیید کامل دستگاه واقعی و release production باقی است |

برای هر گزارش آینده، سه مورد را جدا بنویسید: **commit سورس، فایل APK با SHA-256، و نتیجهٔ تست روی گوشی**. این سه در تاریخچهٔ پروژه همیشه یکسان نبوده‌اند.

## مسیر مطالعه

1. [ROADMAP.md](ROADMAP.md): مبدا، وضعیت فعلی، مرحله‌های آینده.
2. [ARCHITECTURE.md](ARCHITECTURE.md): اجزا و جریان داده.
3. [DECISIONS.md](DECISIONS.md): انتخاب‌ها، گزینه‌های ردشده و شروط تغییر.
4. [IMPLEMENTATION.md](IMPLEMENTATION.md): آنچه واقعاً اجرا و تست شده.
5. [TROUBLESHOOTING.md](TROUBLESHOOTING.md): خطا، نشانه، علت و رفع.
6. [RUNBOOK.md](RUNBOOK.md): استفاده و عیب‌یابی روزانه.
7. [WINDOWS-REINSTALL.md](WINDOWS-REINSTALL.md): بازسازی روی ویندوز تازه.
8. [SECURITY-NEXT-STEPS.md](SECURITY-NEXT-STEPS.md): امنیت انجام‌شده و کارهای پیش از Production.
9. [API.md](API.md)، [DATABASE.md](DATABASE.md)، [ENVIRONMENT.md](ENVIRONMENT.md)، [BACKUP-RESTORE.md](BACKUP-RESTORE.md): جزئیات فنی.

دفتر تاریخی سورس نیز [PROJECT_ROADMAP.md](https://github.com/mohseniamin64-cmd/SMS_Gate/blob/main/PROJECT_ROADMAP.md) است؛ بعضی تیک‌های ابتدای آن قدیمی‌اند. وضعیت قابل اتکا را از commit و تست همان نسخه تعیین کنید.

## قاعدهٔ محرمانگی

هیچ Password، API Key، Token، Private Key، Session Cookie، Recovery Code، keystore یا دادهٔ پیام شخصی در این مخزن قرار نمی‌گیرد. هر Credential باید از محل امن یا Dashboard مربوطه دوباره دریافت شود.

## متن شروع در چت جدید

> این Repository را کامل بخوان و پروژه را از روی مستندات آن ادامه بده: https://github.com/mohseniamin64exchange-commits/SMS_Gate_Knowledge_Base . سپس سورس https://github.com/mohseniamin64-cmd/SMS_Gate را با commit و شاخهٔ ذکرشده بررسی کن. ابتدا وضعیت آنلاین و نسخهٔ نصب‌شده را از هم جدا کن، بعد کارهای ROADMAP را ادامه بده.

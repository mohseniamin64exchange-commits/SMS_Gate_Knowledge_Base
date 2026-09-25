# دامنهٔ بکاپ و Restore

## این مخزن چه چیزی را حفظ می‌کند؟

هدف محصول، تصمیم‌ها، معماری، راهنمای اجرا، علت خطاها و نقاط باز. سورس/کد در مخزن `mohseniamin64-cmd/SMS_Gate` است. GitHub APK نصب‌شده، دیتابیس گوشی، SMS Provider، Android Keystore، secret و فایل‌های local منتشرنشده را نگه نمی‌دارد.

## بکاپ جداگانهٔ عملیاتی

برای backend اختیاری، `backend/call_logs.db` را با توقف نوشتن یا backup سازگار SQLite و به‌صورت رمزنگاری‌شده ذخیره کنید. روی گوشی، دادهٔ SMS و برنامه را مطابق سیاست Android و رضایت کاربر backup کنید؛ `allowBackup=false` یعنی cloud backup عادیِ برنامه جایگزین روش رسمی restore نیست. API key و signing key در vault/محل امن جدا باشند.

## آزمایش بازیابی

`clone docs → clone source و SHA → build/test → نصب APK متناظر → اعطای مجوز → روشن‌کردن Gateway → health/status → خواندن SMS/Call Log → حذف و sync → reboot`.

نتیجهٔ این آزمایش با زمان، دستگاه، commit، APK hash و محدودیت‌ها ثبت شود. تا وقتی این زنجیره روی سیستم دیگر اجرا نشده، این مخزن یک **بکاپ دانش** است و بازیابی عملی کامل اثبات نشده است.

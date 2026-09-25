# مدل داده و بازیابی

## Room روی گوشی

نام فایل Room در سورس: `sms_center_db`؛ نسخهٔ schema فعلی ۴. جدول‌ها:

| جدول | کار |
| --- | --- |
| `gateway_settings` | تنظیمات legacy Flask/webhook، حالت تست، سقف‌ها، autostart، Call Log sync، پورت Phone Server |
| `synced_sms` | cache پیام‌ها، direction و SIM، متن/آدرس/زمان |
| `tombstones` | اثر انگشت پیام حذف‌شده برای جلوگیری از بازگشت |
| `sms_queue` | درخواست ارسال، status، retry، schedule/expiry |
| `log_entries` | گزارش محلی محدود |
| `call_log_upload_queue` | outbox ارسال گزارش تماس به backend اختیاری |

Migrationها: ۱→۲ برای direction/autostart/call-log؛ ۲→۳ برای Phone Server با پورت 8080؛ ۳→۴ پورت ذخیره‌شدهٔ 8080 را به 3030 و ستون قدیمی `phoneServerApiKey` را خالی می‌کند. در نسخهٔ فعلی، کلید سرور باید از `SecureApiKeyStore` تأمین شود. `gateway_settings` هنوز فیلدهای legacy `apiKey` و `webhookSecret` را دارد؛ فرض نکنید همهٔ secretهای legacy به Keystore منتقل شده‌اند.

`synced_sms` خودِ SMS Provider نیست. حذف cache به معنی حذف پیام گوشی نیست. پاک‌کردن app data، tombstone و queue را از بین می‌برد و می‌تواند باعث تفاوت دوبارهٔ وضعیت شود. هر restore دیتابیس باید با snapshot Provider و migration تست شود.

## SQLite backend اختیاری

`backend/call_logs.db` به‌طور پیش‌فرض و با `CALL_LOG_DB` قابل جابجایی است. جدول `call_logs` با کلید مرکب `device_id,call_id` و index روی زمان/نوع ایجاد می‌شود. نام مخاطب عمداً ذخیره نمی‌شود. این DB در Git ignore شده است؛ backup جداگانه و امن لازم دارد.

## تاریخ

Timestampها به‌صورت عددی/میلادی نگهداری می‌شوند؛ نمایش شمسی در UI است. قبل از ساخت query تاریخی از واحد timestamp (millisecond/second) و timezone مطمئن شوید.

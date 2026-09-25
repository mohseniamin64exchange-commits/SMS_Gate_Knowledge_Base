# قرارداد API و تفاوت دو سرور

## ۱. Phone Server روی گوشی

مبنای این سند `main@474bf21` و `docs/PHONE_SERVER_API.md` است. آدرس فعلی: `https://<PHONE-IP>:3030`، با certificate خودامضاشده. همهٔ مسیرهای کاربردی، از جمله health، به `Authorization: Bearer <PHONE_API_KEY>` یا `X-API-Key: <PHONE_API_KEY>` نیاز دارند. مقدار واقعی را در Git، URL یا این سند نگذارید.

| Method | Route | کار |
| --- | --- | --- |
| GET | `/api/health` | زنده‌بودن و وضعیت پایه، با auth |
| GET | `/api/status` | وضعیت واقعی، IP/port، fingerprint و شمارش صف |
| GET | `/api/sms/read?limit=100&offset=0` | پیام‌های cache محلی |
| GET | `/api/sms` | alias خواندن SMS در کد |
| POST | `/api/sms/send` | افزودن پیام به صف، با `requestId` اختیاری برای idempotency |
| POST | `/api/sms/sync` | بازخوانی Provider |
| GET | `/api/call-logs` | گزارش تماس محلی، بدون نام مخاطب در response |
| POST | `/api/call-logs/sync` | بازخوانی گزارش تماس |

نمونهٔ ساختار درخواست ارسال، بدون credential واقعی: `{"to":"+15551234567","body":"Example","simSlot":-1,"requestId":"example-unique-id"}`. ارسال واقعی به حالت تست، مجوز، ساعات و سقف‌های صف وابسته است. ریشهٔ `/` در سورس آنلاین مبنا route ندارد؛ صفحهٔ عمومیِ دیده‌شده روی گوشی از APK دیگری است.

## ۲. backend مستقل تماس

`backend/app.py` از Flask و SQLite استفاده می‌کند، مسیرهای `GET /api/health`، `POST /api/call-logs/sync` و `GET /api/call-logs` دارد و فقط `Authorization: Bearer` را می‌پذیرد. `SMS_CENTER_API_KEY` در محیط لازم است؛ اگر تنظیم نباشد 503 برمی‌گرداند. سقف batch تماس ۵۰۰ است و `(device_id,call_id)` کلید یکتا است.

این backend معادل Phone Server نیست و SMS endpoint کامل ارائه نمی‌دهد. مسیرهای legacy پنل قدیمی مثل `/api/messages/pending` و `/api/messages/status` در همین `backend/app.py` پیاده نشده‌اند.

## ۳. Webhook قدیمی

آدرس `/webhooks/smsgate` در پنل وب قدیمی بررسی شده است. بازکردن مستقیم آن با GET می‌تواند 405 بدهد؛ method و امضای واقعی را باید با کد همان پنل بررسی کرد. این route جزو Phone Server فعلی نیست.

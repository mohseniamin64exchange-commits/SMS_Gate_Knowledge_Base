# راهنمای عملیاتی روزانه

## راه‌اندازی

1. گوشی را به Wi-Fi شبکهٔ موردنظر وصل کنید. IP ممکن است پس از هر اتصال عوض شود.
2. برنامه را باز کنید، مجوزهای SMS، Contacts، Call Log، Phone State و Notification را طبق قابلیت مورد نیاز بررسی کنید.
3. Gateway را روشن کنید. گزینهٔ autostart را فقط در صورت تمایل فعال کنید؛ بعد از reboot باید وضعیت را ببینید.
4. بخش Local Server/Gateway باید وضعیت واقعی، IP، port و خطا را نشان دهد. در سورس آنلاین فعلی port پیش‌فرض ۳۰۳۰ و transport HTTPS است.
5. روی PC همان LAN، آدرس دقیق نمایش‌داده‌شده در گوشی را باز کنید. در `main@474bf21` صفحهٔ `/` وجود ندارد؛ برای health از API و header معتبر استفاده می‌شود.
6. برای خواندن SMS یا درخواست ارسال، credential را فقط در header کلاینت مجاز قرار دهید. آن را در URL، screenshot، چت یا log نگذارید.

## بررسی سلامت

- Gateway و foreground notification فعال هستند؟
- IP گوشی و PC در همان subnet هستند؟
- سرور وضعیت running نشان می‌دهد و port اشغال نیست؟
- `GET /api/health` با auth معتبر پاسخ می‌دهد؟
- `GET /api/status` status واقعی، port و fingerprint را نشان می‌دهد؟
- sync با مجوز READ_SMS/READ_CALL_LOG بدون خطا انجام می‌شود؟
- Send در Test Mode واقعاً غیرفعال است؟

## هنگام خرابی

اول نسخه را ثابت کنید: نام APK، SHA-256، commit/branch و Android version. سپس یکی از ردیف‌های [TROUBLESHOOTING.md](TROUBLESHOOTING.md) را دنبال کنید. اگر پیام دوباره ظاهر شد، پاک‌کردن Room یا tombstone راه تشخیص نیست؛ ابتدا snapshot Provider و مسیر منبع را بررسی کنید.

## کارهای ممنوع در عملیات عادی

- پاک‌کردن app data/Room بدون backup؛ tombstone و queue از بین می‌روند.
- گذاشتن API key در URL یا Git.
- انتشار port 3030 روی اینترنت عمومی.
- فرض اینکه پنل Flask موجود همان وب‌اپ کامل Phone Server است.

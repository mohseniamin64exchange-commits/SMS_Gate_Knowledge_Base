# بازیابی پس از تعویض ویندوز

## چه چیزهایی باقی می‌مانند؟

GitHub سورس commit‌شده، این دفتر، تاریخچهٔ commit و workflowها را نگه می‌دارد. دادهٔ SMS گوشی در Android Provider است، نه در GitHub. اگر خود گوشی عوض یا factory reset شود، Room، queue، tombstone، certificate و Android Keystore ممکن است از بین بروند. APK محلی که release نشده نیز با تعویض ویندوز از دست می‌رود.

## چه چیزهایی باید دوباره آماده شوند؟

Git، JDK 17، Android SDK API 36/Build Tools 36 (یا Google AI Studio به‌جای build محلی)، Python 3.10+ برای backend تماس، دسترسی به هر دو Repository، و اتصال Google AI Studio به GitHub. Credential باید از محل امن یا Dashboard مربوطه دوباره دریافت شود؛ مقدار آن را در Git/این دفتر ننویسید. Signing keystore قبلی اگر در مخزن امن دیگری نیست، قابل بازیابی از سورس نیست.

## ترتیب دقیق بازیابی

1. [دفتر دانش](https://github.com/mohseniamin64exchange-commits/SMS_Gate_Knowledge_Base) را بخوانید.
2. [سورس](https://github.com/mohseniamin64-cmd/SMS_Gate) را clone کنید و branch/SHA release مدنظر را انتخاب کنید. مبنای این سند `main@474bf21b2b8277305ce4c7915216b6defeb31dcf` است؛ برای کار جدید، SHA تازه را تأیید کنید.
3. `app/build.gradle.kts`، `docs/PHONE_SERVER_API.md`، `PROJECT_ROADMAP.md` و workflow CI را بخوانید.
4. در ویندوز دارای SDK، با Gradle 9.3.1 طبق workflow اجرا کنید: `gradle :app:testDebugUnitTest`، `gradle :app:assembleDebug`، `python -m pytest backend/tests -q`. اگر wrapper موجود بود، از `gradlew.bat` همان repo استفاده کنید؛ آن را فرض نکنید.
5. اگر Android Studio ندارید، پروژه را از branch درست در Google AI Studio باز کنید؛ GitHub Sync قبلاً روی `main` بوده است. خروجی build را با SHA آنلاین تطبیق دهید.
6. APK debug را فقط برای تست نصب کنید. برای release، signing key را از محل امن بازیابی کنید. رمزها در Git نیستند.
7. روی گوشی مجوزها، Gateway، port، autostart، battery settings و IP را دوباره تنظیم کنید.
8. از PC همان LAN، transport و API را طبق [API.md](API.md) آزمایش کنید.
9. سناریوهای واقعی SMS، حذف، تماس، reboot و مرورگر را ثبت کنید. تا این تست‌ها تمام نشوند، وضعیت را Production ننامید.

## خدمات قابل اتصال مجدد

- GitHub account و Google AI Studio GitHub Sync.
- Backend اختیاری Flask: اگر استفاده می‌شود `SMS_CENTER_API_KEY` و مسیر دیتابیس `CALL_LOG_DB` را از پیکربندی امن دوباره تنظیم کنید.
- کلاینت وب آینده: URL گوشی، port و API key را از خود گوشی/محل امن دوباره provision کنید.
- DNS/Tunnel در معماری اصلی تعریف نشده؛ اتصال مجدد آن‌ها فقط در صورت وجود استقرار جداگانه لازم است.

## تست نهایی بازیابی

`source SHA → tests/build → APK hash → install → permissions → LAN → authenticated API → SMS delete/resync → Call Log → reboot`.

# محیط‌ها، ابزارها و تنظیمات

## سورس Android آنلاین

- Repository: `https://github.com/mohseniamin64-cmd/SMS_Gate`
- مبنای بررسی: `main@474bf21b2b8277305ce4c7915216b6defeb31dcf`
- Kotlin/Compose/Room؛ `applicationId=com.aistudio.smscenter.pzkxmp`
- `minSdk=24`، `compileSdk=36`، `targetSdk=36`
- Java/Kotlin target=17
- CI: `.github/workflows/android-ci.yml`، Gradle 9.3.1، Android SDK 36، Build Tools 36.0.0، Python 3.12 برای تست backend
- نسخهٔ آنلاین پورت Phone Server=3030، transport=HTTPS
- `app/build/outputs/apk/debug/app-debug.apk` مسیر معمول خروجی debug

## محیط کاربر

کاربر Android Studio نصب نکرده و Google AI Studio را برای build و ساخت APK به‌کار گرفته است. GitHub Sync آن در مقطعی به `main` متصل بود؛ قبل از هر build وضعیت شاخه را بخوانید. Shell AI Studio ممکن است credential GitHub برای `git push` نداشته باشد، حتی وقتی UI حساب متصل دارد.

## شبکهٔ تست تاریخی

گوشی `192.168.1.27`، PC `192.168.1.12`، port 3030. این IPها DHCP و فقط نمونه‌اند. دامنهٔ اینترنتی، public IP یا Tunnel تأییدشده برای مسیر اصلی در این پروژه ثبت نشده است.

## تنظیمات بدون Secret

`serverUrl`، `apiKey`، `deviceId`، interval پیش‌فرض ۳۰ ثانیه، webhook URL/secret، سقف دقیقه/ساعت/روز، Test Mode پیش‌فرض فعال، autostart، Call Log sync و phoneServerPort در `GatewaySettings` وجود دارند. فیلدهای Flask/webhook legacy هستند؛ برای اتصال PC به گوشی، URL گوشی را باید از وضعیت Phone Server گرفت. مقدار Credential باید از محل امن یا Dashboard مربوطه دوباره دریافت شود.

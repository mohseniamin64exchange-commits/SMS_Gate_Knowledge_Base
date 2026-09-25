# ساخت، انتشار و نسبت‌دادن APK به سورس

## Build مرجع

GitHub Actions در سورس اصلی روی push/PR شاخه‌های `main` و `codex/mvp-integration` تست backend، `:app:testDebugUnitTest` و `:app:assembleDebug` را با Java 17/SDK 36/Gradle 9.3.1 اجرا می‌کند. وضعیت workflow همان SHA را بخوانید. موفقیت یک commit قبلی تضمین build commit جدید نیست.

دستورهای محلیِ مطابق CI: `python -m pip install -r backend/requirements.txt`، `python -m pytest backend/tests -q`، `gradle :app:testDebugUnitTest --stacktrace` و `gradle :app:assembleDebug --stacktrace`. اگر wrapper در clone جدید موجود است، استفاده از آن بهتر است؛ در تاریخچه، برخی cloneها wrapper نداشتند.

## AI Studio

قبل از build، Repository و branch متصل را بخوانید. گزارش واقعی باید commit SHA، نتیجهٔ دو task، شمار Pass/Fail، مسیر و SHA-256 APK را داشته باشد. GitHub Sync UI و `git push` داخل container ممکن است دسترسی متفاوت داشته باشند.

## انتشار

APK debug برای pilot است. Release signing با `KEYSTORE_PATH`، `STORE_PASSWORD` و `KEY_PASSWORD` طراحی شده؛ مقادیر و فایل keystore باید خارج Git باشند. بدون تست روی گوشی واقعی، نسخه را production اعلام نکنید. پنل وب نهایی نیز هنوز نیاز به پیاده‌سازی/تطبیق با Phone Server دارد.

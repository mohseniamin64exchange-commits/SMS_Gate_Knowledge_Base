# آنچه واقعاً انجام شد

این خط زمانی از گفت‌وگو، دفتر کار سورس و فایل‌های آنلاین جمع‌بندی شده است. تاریخ دقیق بعضی قدم‌های اولیه معلوم نیست؛ برای آن‌ها ترتیب نسبی معتبرتر از تاریخ حدسی است.

1. **پنل وب و SMSGate:** ارسال/دریافت آزمایشی، import اکسل با پنج شماره، وب‌هوک و تنظیمات پیشرفته امتحان شد. درخواست import شماره بدون صفر آغازین مطرح شد. استاندارد قطعی اکسل باز ماند.
2. **کشف مشکل حذف:** حذف SMS از inbox و deleted گوشی و پاک‌کردن آرشیو پنل، پیام قدیمی را از خروجی SMSGate حذف نکرد. تکرار آزمایش پس از restart و پاک‌کردن دیتابیس پنل همان نتیجه را داد.
3. **انتخاب اپ مستقل:** مخزن `SMS_Gate` بررسی شد، دفتر `PROJECT_ROADMAP.md` و قواعد `AGENTS.md` شکل گرفتند. هدف، خواندن مستقیم Provider Android شد.
4. **Baseline:** Android/Compose/Room/Retrofit ساخته شد. تست پیش‌فرض `GreetingScreenshotTest` و سپس `ExampleRobolectricTest` اصلاح شدند. گزارش‌های build/test اولیه روی شاخه‌های MVP سبز شدند.
5. **MVP Android:** sync با snapshot کامل/tombstone، صف ارسال، receiver و webhook؛ UI مکالمه‌ای فارسی، Contacts، Call Log، Back و تنظیمات اضافه شد. در گزارش یکپارچه ۱۷ تست Android و ۵ تست backend گذشتند. اینها گزارش‌های آن زمان‌اند، نه نتیجهٔ اجرای امروز.
6. **JVM:** `compileDebugJavaWithJavac` روی ۱۷ و Kotlin روی ۲۱ بود؛ `kotlinOptions.jvmTarget = "17"` افزوده شد. AI Studio روی `main` sync می‌شد، نه شاخهٔ `codex/mvp-integration`. گزارش بعدی ۱۸ تست سبز و APK debug را ثبت کرد.
7. **اصلاح معماری:** کاربر روشن کرد که گوشی باید HTTP server باشد. کد `PhoneHttpServer` و API پیامک/تماس در Android اضافه شد؛ Flask اختیاری ماند. پورت اولیه 8080 بود.
8. **امنیت Phone Server:** TLS self-signed، Android Keystore، fingerprint، نگهداری امن API key، Boot/Job retry و migration Room اعمال شدند. پورت پیش‌فرض با migration 3→4 به ۳۰۳۰ رسید. `main@474bf21` این کد را دارد.
9. **تست LAN کاربر:** گوشی با IP `192.168.1.27` و PC با `192.168.1.12` آزمایش شدند. HTTP به `NS_ERROR_NET_EMPTY_RESPONSE` و HTTPS نخست به `PR_END_OF_FILE_ERROR` رسید. یک APK محلیِ جداگانه با صفحهٔ راهنمای عمومی بعداً در Firefox باز شد؛ Chrome با self-signed certificate مشکل داشت.
10. **درخواست کنونی transport:** کاربر HTTP ساده را برای حالت عادی و HTTPS را برای Advanced Settings می‌خواهد. تا تاریخ این بکاپ، این تغییر در `main` تأیید نشده است.

## قید مهم نسخه‌ها

در گفت‌وگو یک rebuild محلی بر پایهٔ `capcom6/android-sms-gateway` و APK آزمایشی با ۴۰ تست گزارش شده بود. آن branch/commit محلی در مخزن اصلی آنلاین تأیید نشده است. صفحهٔ عمومی «SMS Gate Local Server is running» در همین مسیر آزمایشی دیده شد؛ `main@474bf21` route `/` ندارد. این دو را merge‌شده فرض نکنید.

## عملیات انتشار

مخزن سورس اصلی: `mohseniamin64-cmd/SMS_Gate`. شاخه‌های تاریخی: `codex/initial-roadmap`، `codex/mvp-integration`، `codex/phone-server-architecture`. SHA مبنای این سند `474bf21b2b8277305ce4c7915216b6defeb31dcf` روی `main` است. برای هر تغییر جدید، SHA و نتیجهٔ CI تازه را ثبت کنید.

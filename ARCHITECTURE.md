# معماری فنی

## تصویر کلان

```text
Android SMS Provider ─┐
Call Log Provider ─────┼─> Android app (Kotlin/Compose)
Contacts Provider ─────┘     ├─ SmsRepository + SmsSyncPlanner
                              ├─ Room: cache / queue / tombstones / settings / outbox
                              ├─ SmsGatewayService + receivers + JobScheduler
                              └─ PhoneHttpServer (LAN, port 3030)
                                      │ HTTPS + API key در سورس آنلاین فعلی
                                      ▼
                             مرورگر / پنل وب / کلاینت دسکتاپ
```

گوشی سرور اصلی است. پنل Flask و webhook قدیمی، مسیر اختیاری/legacy هستند. **`backend/app.py` موجود در سورس آنلاین، پنل کامل SMS نیست؛ فقط API مستقل Call Log را پیاده کرده است.** برای ساخت وب‌اپ کامل باید قرارداد Phone Server را مبنا قرار داد.

## اجزای سورس آنلاین `main@474bf21`

- `app/src/main/java/com/example/MainActivity.kt`: صفحات Compose و UI فارسی.
- `ui/viewmodel/SmsViewModel.kt`: state و اعمال UI.
- `data/repository/SmsRepository.kt`: Provider، sync، queue، send و webhook legacy.
- `data/repository/SmsSyncPlanner.kt`: مقایسهٔ snapshot و tombstone.
- `data/local/AppDatabase.kt`: Room نسخهٔ ۴، جدول‌ها و migrationها.
- `service/SmsGatewayService.kt`: foreground lifecycle.
- `service/PhoneHttpServer.kt`: TLS socket، auth و routeهای LAN.
- `service/PhoneServerTls.kt`: گواهی self-signed و fingerprint.
- `data/remote/SecureApiKeyStore.kt`: ذخیرهٔ محلی رمزنگاری‌شدهٔ API key.
- `receiver/GatewayBootReceiver.kt` و `service/SmsGatewayJobService.kt`: startup/retry.
- `data/device/CallLogReader.kt` و `ContactsReader.kt`: دادهٔ دستگاه.
- `backend/app.py`: API تماس با SQLite، مستقل از API پیامک گوشی.

## جریان داده

1. Provider پیامکِ ورودی/خروجی را می‌دهد؛ direction از `type` خوانده می‌شود و SIM جداگانه تشخیص داده می‌شود.
2. snapshot کامل با cache مقایسه می‌شود. snapshot ناقص حق حذف ندارد؛ tombstone مانع بازگشت دادهٔ حذف‌شده می‌شود.
3. UI پیام‌ها را بر اساس شماره به مکالمه گروه‌بندی می‌کند؛ خروجی و ورودی رنگ متفاوت دارند.
4. درخواست `/api/sms/send` با `requestId` وارد صف می‌شود. محدودیت زمانی، نرخ، حالت تست و مجوز پیش از ارسال اعمال می‌شوند.
5. گزارش تماس از Provider خوانده می‌شود. نام مخاطب روی دستگاه نمایش داده می‌شود؛ backend مستقل عمداً `contactName` را قبول/ذخیره نمی‌کند.

## شبکه و سیستم‌عامل

- گوشی Android با `minSdk 24`، `targetSdk 36` در سورس آنلاین.
- Phone Server روی همهٔ interfaceها bind می‌کند؛ پورت پیش‌فرض ۳۰۳۰ و transport فعلی HTTPS است.
- PC و گوشی باید در یک LAN باشند. `192.168.1.27` و `192.168.1.12` فقط IPهای یک تست بوده‌اند.
- دامنه، DNS یا Tunnel برای مسیر اصلی LAN تعریف نشده است. هر ادعای مربوط به دامنه/تونل باید با پیکربندی تازه تأیید شود.
- دسترسی از اینترنت عمومی، port forwarding و cloud proxy خارج از محدودهٔ نسخهٔ فعلی است.
- Google AI Studio برای import/sync/build استفاده شده؛ خود برنامهٔ Android برای کارکردن به AI Studio نیاز ندارد.

## قاعدهٔ تاریخ

زمان‌های Provider و API به صورت timestamp میلادی/Unix نگهداری شوند؛ نمایش فارسی شمسی است. تبدیل ورودی شمسی به timestamp باید در مرز UI/API انجام شود، نه با تغییر معنای دادهٔ ذخیره‌شده.

# خطاها و روش تشخیص

| نشانه | علت/شاهد | تست انجام‌شده یا لازم | رفع یا وضعیت |
| --- | --- | --- | --- |
| SMS حذف‌شده پس از پاک‌کردن آرشیو دوباره ظاهر شد | SMSGate همان داده را در بازخوانی برمی‌گرداند؛ حذف از پنل منبع را تغییر نمی‌داد | پاک‌کردن inbox/deleted، آرشیو، restart و بازخوانی چندباره | انتخاب اپ مستقل و خواندن Provider؛ snapshot کامل/tombstone. تست واقعی روی گوشی هنوز لازم است |
| `405 Method Not Allowed` در `/webhooks/smsgate` | GET مرورگر با method مورد انتظار webhook یکی نبود | method و route واقعی server را بررسی کن | درخواست را با method مستند بفرست؛ 405 به‌تنهایی نشانهٔ خرابی webhook نیست |
| تست Robolectric: `My Application` در برابر `SMS Center` | assertion تمپلیت قدیمی | resource `app_name` و تست را مقایسه کن | assertion با `SMS Center` هماهنگ شد |
| `Greeting` unresolved | تست template به کامپوننت حذف‌شده اشاره داشت | source تست و component موجود | smoke test با component واقعی جایگزین شد |
| Java 17 / Kotlin 21 mismatch | Gradle targetها متفاوت بودند | خروجی `:app:compileDebugKotlin` | `kotlinOptions { jvmTarget = "17" }`، سپس build/test |
| `mergeExtDexDebug` یا KSP file lock | گزارش AI Studio: همزمانی Gradle daemon و فایل‌های DEX | بعد از آزادشدن lock دوباره build | اجرای غیرهمزمان‌نبودن buildها و پاک‌سازی خروجی موقت؛ اگر تکرار شد log دقیق نگه‌دار |
| Android CI failed | نخست mismatch/وابستگی یا محیط build | SHA همان workflow، مرحلهٔ شکست و log را بخوان | رفع بر اساس log، نه حذف تست؛ success بعدی مربوط به commit معین است |
| دکمهٔ LAN کار نمی‌کرد؛ «آدرس سرور لن وارد نشده» | معماری قبلی گوشی را client پنل Flask فرض کرده بود | تنظیمات دارای `serverUrl`، key، webhook و interval بودند | Phone-as-Server به Android اضافه شد؛ تنظیمات Flask legacy باقی ماندند |
| `http://192.168.1.27:3030` → `NS_ERROR_NET_EMPTY_RESPONSE` | پورت نسخهٔ تست TLS بود و HTTP plain را جواب/redirect نمی‌داد | HTTPS همان IP/port را امتحان کن | در نسخهٔ آنلاین فعلی از HTTPS استفاده کن؛ HTTP default هنوز اجرا نشده |
| `https://192.168.1.27:3030` → `PR_END_OF_FILE_ERROR` | TLS handshake/Android Keystore signing در APK آزمایشی بررسی شد | log سرور و fingerprint، APK/commit را تطبیق بده | اصلاح local TLS گزارش شد؛ برای هر APK تازه دوباره آزمایش کن |
| هشدار امنیتی Firefox/Chrome | certificate self-signed و برای مرورگر trusted نیست | fingerprint SHA-256 گوشی را از کانال امن مقایسه کن | اعتماد آگاهانه یا certificate معتبر؛ دورزدن کورکورانه توصیه نمی‌شود |
| 401 در API | key/header نبود یا نادرست بود | `Authorization: Bearer` یا `X-API-Key` را بدون افشای مقدار بررسی کن | credential را از گوشی/محل امن دوباره بگیر؛ 401 به معنی خاموشی سرور نیست |
| IP گوشی از PC باز نمی‌شود | subnet، Wi-Fi isolation، VPN، firewall، service یا port | IP/port روی گوشی، همان LAN و status سرویس | شبکه را اصلاح و از URL نمایش‌داده‌شده استفاده کن |
| Git push از AI Studio shell ناموفق | container توکن GitHub نداشت؛ UI sync به `main` متصل بود | `git ls-remote` و صفحهٔ GitHub Sync | branch مقصد را در UI چک و پس از push SHA آنلاین را بررسی کن |
| App back از برنامه خارج می‌شد | navigation stack نسخهٔ قدیمی Back را مصرف نمی‌کرد | ورود به صفحهٔ فرعی و فشار Back | navigation مرحله‌ای در سورس MVP گزارش شد؛ روی APK نصب‌شده دوباره تست شود |

در هر رخداد جدید: زمان، دستگاه/Android، branch، commit، APK SHA-256، steps بازتولید، log بدون secret و نتیجهٔ اصلاح را به این جدول اضافه کنید.

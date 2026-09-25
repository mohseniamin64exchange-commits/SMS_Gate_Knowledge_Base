# امنیت: وضع موجود و اقدام‌های بعدی

## شواهد موجود در سورس آنلاین

- Phone Server از `SSLServerSocket` و certificate خودامضاشده استفاده می‌کند؛ اثر انگشت SHA-256 در UI/API status دیده می‌شود.
- RSA private key در Android Keystore طراحی شده و API key در مسیر `SecureApiKeyStore` رمزنگاری می‌شود.
- `PhoneHttpServer` پیش از route، Bearer یا `X-API-Key` را بررسی می‌کند. `/api/health` نیز در `main@474bf21` محافظت‌شده است.
- `android:allowBackup="false"` و data extraction rules در manifest وجود دارند.
- لاگ HTTP سطح BODY در اصلاحات قبلی حذف شد؛ روی release تازه دوباره بررسی شود.
- backend تماس بدون `SMS_CENTER_API_KEY` پاسخ 503 می‌دهد و نام مخاطب را ذخیره نمی‌کند.

## ریسک‌ها و کارهای پیش از Production

1. **HTTP LAN-only درخواستی:** HTTP ساده credential و پیامک را روی شبکهٔ محلی بدون رمزنگاری عبور می‌دهد. اگر پذیرفته شد، باید محدودیت شبکه، هشدار روشن، امکان انتخاب HTTPS، عدم دسترسی اینترنتی و تست packet exposure ثبت شود. این ویژگی هنوز پیاده‌سازی نشده است.
2. **TLS self-signed:** اعتماد مرورگر به گواهی خودکار نیست. UX مقایسهٔ fingerprint یا راهکار گواهی معتبر برای کاربران عمومی نیاز دارد.
3. **Network exposure:** bind روی همهٔ interfaceها است؛ VPN، tethering، guest Wi-Fi و firewall باید بررسی شوند. به IP خصوصی به‌تنهایی اعتماد نکنید.
4. **Auth:** rotation/revoke کلید، rate limiting، brute force و زمان‌بندی session/API policy باید آزمون شوند.
5. **Queue/idempotency:** race همزمان برای `requestId` و rate limit، تست فشاری لازم دارد.
6. **Device loss/backup:** Keystore و دادهٔ Room با factory reset از بین می‌روند؛ بازیابی secrets و tombstone باید طراحی شود.
7. **Release:** signing keystore خارج Git، dependency review، permission review و تست Android 15/16 انجام شود.
8. **Privacy:** متن SMS و شمارهٔ شخصی در issue، CI log یا screenshot عمومی منتشر نشود. این مخزن عمومی است.

هیچ Credential واقعی اینجا ثبت نشده؛ هر Credential باید از محل امن یا Dashboard مربوطه دوباره دریافت شود.

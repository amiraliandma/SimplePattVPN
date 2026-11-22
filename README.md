# فانوس VPN (کلاینت ساده و سالمندپسند مبتنی بر PattNG)

این پروژه بر پایه کد متن‌باز [PattNG](https://github.com/patterniha/PattNG) ساخته و به‌صورت کامل برای **سادگی حداکثری، سبکی، اجرای روان و ظاهر روشن و دوستانه** بهینه‌سازی شده است.

## ویژگی‌ها

- **معماری اختصاصی `arm64-v8a`**: فقط برای پردازنده‌های ۶۴ بیتی اندروید (`ARMv8`) بسته‌بندی شده تا حجم و مصرف منابع در کمترین حد باشد.
- **لینک اشتراک پیش‌فرض و کانفیگ‌های آماده**:
  - لینک اشتراک `https://lantern.darkpx.workers.dev/sub` به‌صورت پیش‌فرض و ثابت روی برنامه تنظیم شده است.
  - کانفیگ‌های فعلی این اشتراک (`Hysteria2`، `Shadowsocks 2022`، `VLESS`) به‌صورت آماده در فایل `V2rayNG/app/src/main/assets/default_sub_configs.txt` داخل برنامه قرار دارند تا از همان لحظه اول آماده اتصال باشند.
- **رابط کاربری روشن، گوگولی و سالمندپسند**:
  - تم روشن با رنگ‌های ملایم و خوانایی بالا، فونت بزرگ، دکمه اتصال دایره‌ای بزرگ و لیست واضح سرورها.
  - فقط **دکمه اتصال/قطع**، **آپدیت اشتراک** و **تست دیلی** به همراه لیست سرورها وجود دارد.
  - تمام منوها، تنظیمات پیشرفته، اسکنر QR، ویرایشگرها، سرویس‌های روت/پروکسی و بخش‌های اضافی حذف شده‌اند.
- **روتینگ پیش‌فرض + ایران (`custom_routing_white_iran`)**:
  - عبور مستقیم ترافیک شبکه داخلی (`geoip:private`، `geosite:private`) و تورنت (`bittorrent`)
  - مسدودسازی تبلیغات (`geosite:category-ads-all`) و `udp:443`
  - پروکسی ترافیک گوگل (`geosite:google`)
  - عبور مستقیم سایت‌ها و آی‌پی‌های ایران (`domain:ir`، `geosite:category-ir`، `geoip:ir`) با استراتژی `IPIfNonMatch`
- **DNS پیش‌فرض گوگل**:
  - DNS رابط VPN روی `8.8.8.8, 8.8.4.4` و DNS ریموت روی `https://8.8.8.8/dns-query` تنظیم شده است.
- **موتور سبک Xray TUN**:
  - بدون نیاز به باینری‌های اضافی `hev-socks5-tunnel`، `aether`، `psiphon` یا `lyrebird`؛ فقط از هسته رسمی `libv2ray.aar` (`patterniha/AndroidLibXrayLite`) استفاده می‌کند.

## راهنمای باز کردن و بیلد پروژه (محدودیت‌ها و نکات مهم)

1. **پوشه صحیح برای باز کردن در Android Studio**:
   - در Android Studio حتماً پوشه زیر را باز کنید (نه پوشه ریشه):
     `SimplePattVPN/V2rayNG`
2. **عدم نیاز به NDK، Rust یا Go**:
   - تمام اسکریپت‌ها و ماژول‌های نیازمند کامپایلرهای بومی (`compile-hevtun.sh`، `compile-aether.sh`، `compile-psiphon.sh`، `compile-pt.sh`) حذف شده‌اند و هسته از پیش کامپایل‌شده `V2rayNG/app/libs/libv2ray.aar` (نسخه `v26.11.21`) در پروژه قرار داده شده است.
   - توزیع `arm64-v8a` در `app/build.gradle.kts` با `splits.abi` و `packaging.jniLibs.excludes` بدون نیاز به Android NDK انجام می‌شود.
3. **نیازمندی‌های SDK و Java**:
   - Android SDK Platform `android-37.0` (`compileSdk = 37`, `targetSdk = 37`, `minSdk = 29`)
   - Java 17+ (در `V2rayNG/local.properties` مسیر SDK سیستم تنظیم شده است).
4. **دستور بیلد از ترمینال (داخل پوشه `V2rayNG`)**:
   - تست واحد: `.\gradlew.bat :app:testDebugUnitTest`
   - ساخت APK دیباگ: `.\gradlew.bat :app:assembleDebug`
   - ساخت APK ریلیز: `.\gradlew.bat :app:assembleRelease`

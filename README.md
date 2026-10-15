# tvhub-data

استضافة بيانات تطبيق **TV Hub**: كتالوج القنوات وملفات إصدار التطبيق.

هذا المجلد هو مصدر التحديث الذي يقرأه التطبيق. لا تعدّل الملفات يدويًا —
كلها تُولَّد بسكربت `publish.ps1` في مشروع التطبيق.

## الملفات

| الملف | الوصف |
|---|---|
| `catalog.json` | كتالوج القنوات ومصادر البث |
| `categories.json` | التصنيفات والأحداث والملخّصات |
| `manifest.json` | فهرس الكتالوج: رقم الإصدار + بصمات SHA-256 |
| `app.json` | فهرس إصدار التطبيق: رقم البناء + رابط APK + بصمة |
| `apk/TVHub-latest.apk` | أحدث نسخة من التطبيق |

## روابط جاهزة

الكتالوج (raw):

```
https://raw.githubusercontent.com/saleh9688/tvhub-data/main
```

GitHub Pages (بعد تفعيلها من Settings ← Pages):

```
https://saleh9688.github.io/tvhub-data
```

ضع الرابط في التطبيق: **الإعدادات ← تحديث الكتالوج عبر الإنترنت**.

## كيف تُحدَّث البيانات

في مشروع التطبيق، مجلد `catalog_host`:

```powershell
.\publish.ps1        # ي regenerates الملفات من أصول التطبيق + أحدث APK
cd public
git add -A
git commit -m "update"
git push
```

## ملاحظة عن التحديث

عند نشر إصدار جديد من التطبيق **زد `versionCode`** في `app/build.gradle.kts`
وابنِ APK جديد. التطبيق يقارن رقم البناء المنشور برقمه ويرفض أي رقم أقل أو مساوٍ.

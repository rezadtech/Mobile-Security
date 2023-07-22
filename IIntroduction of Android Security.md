# Introduction of Adroid Security

## Android platform architecture
 
![شکل معماری انروید](https://static.packt-cdn.com/products/9781849515603/graphics/5603OT_01_02.jpg)



## what is a dex file?
	* فایل‌های dex, در اندروید فایل‌های اجرایی هستند که می‌توانند شامل classes یا methodها باشند.
	
	* این فایل‌ها از کامپایل کدهای Java یا C++ ایجاد می‌شوند. و در محیط Java Virtual Machine (JVM) در اندروید اجرا می‌شوند. و JVM در اندروید Dalvik Virtual Machine (DVM) شناخته می‌شود.

## Dalvik Virtual Machine (DVM):
    * ماشین‌مجازی DVM، برای دستگا‌ه‌های با توان پایین مانند موبایل بهینه شده‌اند. همچنین داری ویژگی مدیریت حافظه و multi-threading برای Java است. بایت‌کد Java که توسط کامپایلر javac ایجاد می‌شود به بایت‌کد Dalvik تغییر پیدا می‌کند که اپلیکیشن‌های موبایل روی DVM اجرا شوند. JVM یک stack machine است در حالی که DVM یک register machine است . در نسخه‌های جدیدتر اندروید DVM با Android Runtime(ART) جایگزین شده است. ART همان کدهای اجرایی Dalvik را اجرا می‌کند.

## تفاوت‌های DVM با ART
    * در نسخه ۵ اندروید(Lollipop) ART جایگزین DVM شد.
    
    * در DVM از  Just-in-Time (JIT) استفاده می‌شود. در این حالت در زمان اجرا بایت‌کدهای فایل کامپایل می‌شوند.
    
    * در ART از Ahead-of-Time (AOT) استفاده می‌شود. در این حالت بایت‌کدهای فایل کامپایل می‌شوند و سپس اجرا می‌شوند. در نتیجه در این حالت اپلیکیشن‌ها سریع‌تر اجرا می‌شوند.
    
    * زمان نصب اپلیکیشن‌ها در DVM به دلیل اینکه موقع نصب بایت‌کدها کامپایل نمی‌شوند بیشتر است.

## سطح دسترسی هر اپلیکیشن:

هر اپلیکیشن موبایل پردازش و سطح دسترسی مخصوص(User Identification (UID) and Group Identification (GID)) به خود را دارد در اندروید دارد. برای تست این مورد می‌توان از دستور adb استفاده کرد. ابتدا genymotion را نصب کنید و یکی از نسخه‌های android را به دلخواه نصب کنید و آن را اجرا کنید. بعد از نصب در محیط ترمینال لینوکس یا cmd ویندوز دستورات را اجرا کنید:

```bash
adb shell
cd /data/data
ls -la
su u0_a69
cd /data/data
ls -la
```

با انجام دستورات بالا بعد از اینکه سطح دسترسی خود را با استفاده از 'su u0_a69' به سطح دسترسی اپلیکیشن تغییر دادید دسترسی جلوی دسترسی به مسیر data/data گرفته می‌شود و با ls: .: Permission denied مواجه می‌شوید.


## مراحل اجرای اپلیکیشن موبایل

    ۱. زمانی که موبایل boot می‌شود یک پردازش توسط Zygot ایجاد می‌شود.

    ۲. منابع و core library classes توسط Zygote پیش‌بارگذاری (preload) و مقدار دهی اولیه می‌شوند(initialize)

    ۳. زمانیکه اپلیکیشنی اجرا می‌شود سیستم پردازش Zygote را فورک می‌کند.

    ۴. سپس کدهای اپلیکیشن در پردازش اختصاص یافته اجرا می‌شود.

    ۵. شبیه‌ساز DVM توسط Zygote مقدار دهی اولیه می‌شود.

    ۶.در Zygote با ایجاد چند DVM هر پردازش اندروید را پشتیبانی می‌کند

    ۷. دستور app_command شروع کننده ART یا Dalvik VM است و main() در Zygote را صدا می‌زند.

    ۸. در Zygote یک server socket برای کانکشن Zygote ریجیستر می‌شود و بعضی از classها و منابع پیش‌بارگذاری می‌شوند.


## Static Analysis Android

## Reverse Engineering tools
* **Jd-gui**
    * unzip
    * classes.dex
    * dex2jar
    * jd-gui

* **jadx-gui**
    * gvie apk as input
* **Ghidra**
    * gvie apk as input then choose single batch file

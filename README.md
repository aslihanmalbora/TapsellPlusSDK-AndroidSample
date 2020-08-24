[![CircleCI](https://circleci.com/gh/tapsellorg/TapsellPlusSDK-AndroidSample.svg?style=svg)](https://circleci.com/gh/tapsellorg/TapsellPlusSDK-AndroidSample)  
[ ![Download](https://api.bintray.com/packages/tapsellorg/maven/tapsell-plus-sdk-android/images/download.svg) ](https://bintray.com/tapsellorg/maven/tapsell-plus-sdk-android/_latestVersion)

## <div dir="rtl">آموزش راه اندازی کتاب‌خانه TapsellPlus</div>


### <div dir="rtl">توجه: از نسخه 1.0.3 به بعد پشتیبانی از تبلیغات همسان AdMob اضافه شده و این نسخه در تبلیغات همسان با نسخه‌های قبلی سازگار نیست. در صورتی که از تبلیغات همسان استفاده میکنید مطابق آموزش پیش برید.</div>


### <div dir="rtl">توجه: از نسخه 1.0.0 به بعد سایر ادنتورک‌ها که علاقه مند هستید اضافه کنید باید مطابق روش گفته شده اضافه شوند و این ادنتورک‌ها به صورت خودکار اضافه نمیشوند.</div>

### <div dir="rtl">اضافه کردن کتابخانه به پروژه</div>


<div dir="rtl">ابتدا کتابخانه TapsellPlus را مطابق روش زیر به پروژه اضافه کنید سپس هر adNetwork که تپسل پلاس پشتیبانی میکند و مایل هستید را مطابق توضیحات به پروژه اضافه کنید. در انتها با روش‌های تست مطمئن شوید که adNetwork مورد نظر به درستی کار میکند.<br /><br /></div>  
  
<div dir="rtl">ریپازیتوری تپسل را به فایل build.gradle پروژه اضافه کنید.</div>

```gradle
allprojects {  
    repositories {  
        google()  
        jcenter()  
  
        maven {  
            url 'https://dl.bintray.com/tapsellorg/maven'  
        }
    }  
}
```

<div dir="rtl">در بخش dependencies فایل build.gradle اپلیکیشن خط زیر را اضافه کنید.</div>

```gradle
dependencies {
    implementation 'ir.tapsell.plus:tapsell-plus-sdk-android:1.1.3'
}
```

<div dir="rtl">همچنین اگر در قسمت android این قسمت وجود ندارد اضافه‌اش کنید.</div>

```gradle
compileOptions {
  sourceCompatibility JavaVersion.VERSION_1_8
  targetCompatibility JavaVersion.VERSION_1_8
}
```

### <div dir="rtl">افزودن سایر adNetwork ها</div>


<div dir="rtl">در قسمت dependencies فایل build.gradle این موارد را اضافه کنید. برای کسب اطلاعات بیشتر در مورد هر ad network میتوانید با همکاران ما در تیم رسانه صحبت کنید.</div>

```gradle
dependencies {
    .......
    //for adMob
    implementation 'com.google.android.gms:play-services-ads:17.2.1'

    //for unityAds
    implementation 'com.unity3d.ads:unity-ads:3.0.0'

    //for chartboost
    implementation 'com.chartboost:chartboost-sdk:8.1.0'
    
    //for adcolony
    implementation 'com.adcolony:sdk:3.3.11'
    
    //for applovin
    implementation 'com.applovin:applovin-sdk:9.7.2'
    .....
}
```

<div dir="rtl">برای adcolony و chartboost لازم هست ریپازیتوری‌های زیر به build.gradle پروژه اضافه شوند.</div>

```gradle
maven {
  url  "https://adcolony.bintray.com/AdColony"
}
maven {
  url "https://chartboostmobile.bintray.com/Chartboost"
}
```

### <div dir="rtl">تنظیمات پروگوارد</div>

<div dir="rtl">تنظیمات پروگوارد را از  <a href="https://github.com/tapsellorg/TapsellPlusSDK-AndroidSample/blob/master/app/proguard-rules.pro">این فایل</a> دریافت کنید.</div>

### <div dir="rtl">راه اندازی تپسل</div>

<div dir="rtl">کلید تپسل را از <a href="https://dashboard.tapsell.ir/">پنل</a> دریافت کنید.</div>

<div dir="rtl">در اکتیویتی اولیه برنامه tapsell plus را به این شکل مقدار دهی کنید.</div>

```java
import ir.tapsell.plus.TapsellPlus;

public class MainActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        TapsellPlus.initialize(this, TAPSELL_KEY);
    }
}
```

## <div dir="rtl">پیاده‌سازی تبلیغات ویدیو جایزه‌ای</div>

<div dir="rtl">ابتدا از پنل یک تبلیغگاه (zone) ویدیو جایزه‌ای بسازید و zoneId رو زمان درخواست و نمایش تبلیغ مطابق کد زیر استفاده کنید.</div>

```java
import ir.tapsell.plus.AdRequestCallback;
import ir.tapsell.plus.TapsellPlus;
.......
private void requestAd() {
    TapsellPlus.requestRewardedVideo(context, ZONE_ID_REWARDED_VIDEO, new AdRequestCallback() {
        @Override
        public void response() {
            //ad is ready to show
        }

        @Override
        public void error(String message) {
        }

    });
}
```

<div dir="rtl">بعد از اجرای متد response تبلیغ آماده نمایش است و میتوانید مطابق روش زیر نمایش دهید.</div>

```java
private void showAd() {
    TapsellPlus.showAd(activity, ZONE_ID_REWARDED_VIDEO);
}
```

<div dir="rtl">میتوانید به روش زیر از باز و بسته شدن تبلیغ و دادن جایزه به یوزر مطلع بشید.</div>

```java

import ir.tapsell.plus.AdShowListener;
.......
private void showAd() {
    TapsellPlus.showAd(this, ZONE_ID_REWARDED_VIDEO, new AdShowListener() {
        @Override
        public void onOpened() {
            //ad opened
        }

        @Override
        public void onClosed() {
            //ad closed
        }

        @Override
        public void onRewarded() {
            //reward
        }

        @Override
        public void onError(String message) {
            //error
        }
    });
}
```

## <div dir="rtl">پیاده‌سازی تبلیغات آنی</div>
<div dir="rtl">مطابق تبلیغات جایزه‌ای پیش برید فقط زمان درخواست تبلیغ از متد TapsellPlus.requestInterstitial استفاده کنید.</div>

## <div dir="rtl">پیاده‌سازی تبلیغات بنر همسان</div>

<div dir="rtl">ابتدا از پنل یک تبلیغگاه (zone) بنر همسان بسازید و zoneId را زمان درخواست و نمایش تبلیغ استفاده کنید.</div>

<div dir="rtl">در صفحه‌ای که قصد دارید بنر همسان نمایش بدهید باید یک  view  به عنوان فضایی که قصد دارید تبلیغات در آن نمایش داده شود (adContainer) اضافه کنید.</div>

```xml
<?xml version="1.0" encoding="utf-8"?>
<FrameLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <FrameLayout
        android:id="@+id/adContainer"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

    </FrameLayout>

</FrameLayout>
```

<div dir="rtl">باید یک layout دلخواه مطابق شکلی که قصد دارید تبلیغ نمایش داده شود بسازید که rootView از نوع com.google.android.gms.ads.formats.UnifiedNativeAdView  باشد و id و نوع بخش‌های مختلف مطابق با جدول زیر باشد:</div>

|       view       |              id              | type  |
|:------------:|:----------------------------:|:-:|
|     logo     |     `tapsell_nativead_logo`    | `ImageView`  |
|     title    |    `tapsell_nativead_title`    | `TextView`  |
| ad indicator |  `tapsell_nativead_sponsored`  | `View`  |
|  description | `tapsell_nativead_description` | `TextView`  |
|    banner    |    `tapsell_nativead_banner`   | `ir.tapsell.sdk.nativeads.views.RatioImageView`  |
|  media view  |`tapsell_nativead_banner_admob` | `com.google.android.gms.ads.formats.MediaView`  |
|    button    |     `tapsell_nativead_cta`     | `TextView`  |
|    clickable view    |     `tapsell_nativead_cta_view`     | `View`  |

<div dir="rtl">در صورتی که در طراحی دکمه‌ای برای کلیک کردن وجود ندارد میتوانید از clickable view استفاده کنید
</div>
<div dir="rtl">نوع ویوها میتواند از نوع‌های گفته شده ارث بری کرده باشند
</div>
<div dir="rtl">باید ۲ ویو را برای نمایش عکس تبلیغات اختصاص بدهید. یکی از نوع ir.tapsell.sdk.nativeads.views.RatioImageView برای تپسل و دیگری از نوع com.google.android.gms.ads.formats.MediaView برای AdMob این دو میتواند دقیقا روی هم قرار بگیرد. تپسل با توجه به تبلیغ آماده نمایش ویو مورد نظر را نمایش میدهد.</div>
<div dir="rtl">همچنین می‌توانید از view‌ای که برای این منظور از قبل آماده شده با id زیر استفاده کنید یا ازش به عنوان راهنمایی در ساخت ویو کمک بگیرید.</div>

`native_banner`

<div dir="rtl">مطابق قطعه کد زیر adContainer و شناسه layout تبلیغ را به تپسل پلاس بدهید تا یک AdHolder بسازید.</div>

```java
import ir.tapsell.plus.AdHolder;
import ir.tapsell.plus.TapsellPlus;
...
ViewGroup adContainer = findViewById(R.id.adContainer);
...
AdHolder adHolder = TapsellPlus.createAdHolder(
      context, adContainer, R.layout.native_banner);
```

<div dir="rtl">و مطابق این قطعه کد درخواست تبلیغ بدهید.</div>

```java
import ir.tapsell.plus.AdRequestCallback;
import ir.tapsell.plus.TapsellPlus;
.......
private void requestAd() {
    TapsellPlus.requestNativeBanner(context, ZONE_ID_NATIVE_BANNER, new AdRequestCallback() {
        @Override
        public void response() {
            //ad is ready to show
        }

        @Override
        public void error(String message) {
        }

    });
}
```

<div dir="rtl">بعد از اجرای متد response تبلیغ آماده نمایش است و می‌توانید مطابق روش زیر نمایش دهید.</div>

```java
private void showAd() {
    TapsellPlus.showAd(activity, adHolder, ZONE_ID_NATIVE_BANNER);
}
```

## <div dir="rtl">پیاده‌سازی تبلیغات بنر استاندارد</div>

<div dir="rtl">ابتدا از پنل یک تبلیغگاه (zone) بنر استاندارد بسازید و zoneId را زمان درخواست استفاده کنید.</div>

<div dir="rtl">در صفحه‌ای که می‌خواهید تبلیغ نمایش داده شود یک viewGrop اضافه کنید.</div>

```xml
<RelativeLayout
    android:id="@+id/standardBanner"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:layout_gravity="center"
    android:gravity="center" />
```

<div dir="rtl">مطابق کد زیر zoneId و view‌ای که معرفی کردید را به تپسل‌پلاس بدهید.</div>

```java
ViewGroup bannerContainer = findViewById(R.id.standardBanner);

TapsellPlus.showBannerAd(
        context, 
        bannerContainer,
        ZONE_ID_STANDARD_BANNER,
        TapsellPlusBannerType.BANNER_320x50,
        new AdRequestCallback() {
            @Override
            public void response() {
            }

            @Override
            public void error(String message) {
            }
});
```

## <div dir="rtl">تست adNetwork ها</div>


<div dir="rtl">برای اطمینان از صحت عملکرد adNetwrok هایی که اضافه کردید از zoneId مربوط به هرکدام استفاده کنید. هر zoneId مربوط به یک adNetwork و یک نوع تبلیغ هست و تبلیغ حالت تست نمایش داده میشود.</div>

<div dir="rtl">* توجه داشته باشید در حالت تست باید از appId تست استفاده کنید.</div>
<div dir="rtl">* هنگام تست باید از ip خارج ایران (فیلتر شکن) استفاده کنید.</div>
<div dir="rtl">* برای عملکرد صحیح حالت تست باید یکبار برنامه باز و بسته شود. همچنین در دومین درخواست، تبلیغ  adNetwork مورد نظر نمایش داده میشود.</div>
<div dir="rtl">* تست را در حالت build release هم انجام دهید.</div>

<div dir="rtl"><br /></div>

<div dir="rtl">از این appId برای تست استفاده کنید.</div>

```java
TapsellPlus.initialize(this, "alsoatsrtrotpqacegkehkaiieckldhrgsbspqtgqnbrrfccrtbdomgjtahflchkqtqosa");
```

<div dir="rtl">برای هر ادنتورک و هر تبلیغ از zoneId های زیر برای درخواست و نمایش تبلیغ استفاده کنید. در حال حاضر فقط adType/adNetwork های زیر قابل استفاده هستند.</div>

|        Ad Network      |              Ad Type              |ZoneId
|:------------:|:----------------------------:|:----------------------------:|
|     Tapsell     |     Rewarded Video    | `5cfaa802e8d17f0001ffb28e`|
|     Tapsell    |    Interstitial    |`5cfaa942e8d17f0001ffb292`|
| Tapsell |  Native  |`5cfaa9deaede570001d5553a`|
|  Tapsell | Standard |`5cfaaa30e8d17f0001ffb294`|
|    Admob    |    Rewarded Video   |`5cfaa8aee8d17f0001ffb28f`|
|    Admob    |     Interstitial     |`5cfaa9b0e8d17f0001ffb293`|
|    Admob    |     Standard     |`5cfaaa4ae8d17f0001ffb295`|
|    Admob    |     Native     |`5d123c9968287d00019e1a94`|
|    Unity Ads    |     Rewarded Video     |`5cfaa8eae8d17f0001ffb291`|
|    Chartboost    |     Rewarded Video     |`5cfaa8cee8d17f0001ffb290`|
|    AdColony    |     Rewarded Video     |`5d3362766de9f600013662d5`|
|    AdColony    |     Interstitial     |`5d336289e985d50001427acf`|
|    AppLovin    |     Rewarded Video     |`5d3eb48c3aef7a0001406f84`|
|    AppLovin    |     Interstitial     |`5d3eb4fa3aef7a0001406f85`|
|    AppLovin    |     Standard     |`5d3eb5337a9b060001892441`|



# OpenWrt Pass Wall

این دستورالعمل‌ها برای [کلاینتهای یک و دو OpenWrt passwall](https://github.com/xiaorouji/) می‌باشند.

## مسیریابی :id=routing

?> فقط با هسته Xray تست شده است. (با هسته v2ray هم ممکن است کار کند)

۱. رپوی OpenWrt را بروز کرده و بسته v2ray-geosite-ir را نصب کنید.همچنین از طریق رابط وب لوسی نیز میتوانید برای نصب این بسته استفاده کنید. 

```shell
opkg update && opkg install v2ray-geosite-ir
```

۲.قوانین shunt زیر را در بخش `Pass Wall -> Rule Manage -> Shunt Rules` به همین ترتیب ایجاد کنید:

<div dir=ltr>

1.  `Block`:
    -   Remarks: `Block`
    -   Domain: `ext:iran.dat:ads`
2.  `Proxy`:
    -   Remarks: `Proxy`
    -   Domain: `ext:iran.dat:proxy`
3.  `Direct`:
    -   Remarks: `Direct`
    -   Domain: `ext:iran.dat:all`
    -   IP: `geoip:ir`

</div>

۳.(فقط برای پسوال۱) یک Node جدید در `Pass Wall -> Node List -> Add` با مشخصات زیر ایجاد کنید:

<div dir=ltr>

-   Node Remarks: `Shunt`
-   Type: `Xray`
-   Protocol: `Shunt`
-   Block: `Blackhole`
-   Proxy: `Default`
-   Direct: `Direct Connection`
-   Default: یکی از سرور‌های خود را انتخاب کنید
-   Domain Strategy: `AsIs` برای کارایی بیشتر یا `IPIfNonMatch` برای دقت مسیر یابی بهتر.

</div>

5. به `Passwall -> Basic Settings -> Main` بروید و سپس:

<div dir=ltr>

-   TCP Node: `[Shunt]`
-   (only passwall1)UDP Node: `Same as the tcp node`

</div>

-   گزینه `Save & Apply` را بزنید.
-   همچنین به تب `DNS` رفته و `Clear IPSET` را بزنید.

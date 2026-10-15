
# 稍后如何调整这些内容

``` 
Section "Monitor"

Identifier "Unisys-19"

VendorName "Unisys"

ModelName "Unknown"

Bandwidth 110

HorizSync 57-65

RefreshRate 55-65

Modeline "1024x680* 25.15 640 664 760 800 481 493 525

Modeline "1024x768* 44.9 1024 1048 1208 1264 768 776 784 817 interlace

Modeline "1176x1024* 95 1176 1400 1504 1616 1024 1032 1040 1070

-hsync +vsync

Modeline "1176x950* 95 1176 1400 1504 1616 950 964 994

-hsync +vsync

Modeline "1280x1024* 110 1280 1584 1704 1872 1024 1032 1040 1070

-hsync +vsync

Modeline "640x1024* 110 640 1584 1704 1872 1024 1032 1040 1070

-hsync +vsync

EndSection
```

```
#Date: Mon, 19 Sep 94 17:50:04 +0200

#From: Didier Poirat <dp@chorus.fr>

Section "Monitor"

Identifier "ViewSonic 17"

VendorName "ViewSonic"

ModelName "17*"

Bandwidth 75.0

HorizSync 30-82

Refresh 50-90

Modeline "640x480* 25.15 640 664 760 800 481 493 525

Modeline "1024x768* 65 1024 1032 1208 1288 768 768 773 798

Modeline "1024x768b* 65 1024 1080 1224 1234 768 776 778 808

EndSection
```

```
#Date: Wed, 21 Sep 1994 22:47:06 -0700

#From: Brett J. Vickers <dvickers@rumba.ICS.UCI.EDU>

Section "Monitor"

Identifier "ViewSonic 5e"

VendorName "ViewSonic"

ModelName "5e*"

Bandwidth 25.2 mhz

HorizSync 30-60

Refresh 50-90

# Refresh rate = 73.46Hz ; Horizontal Frequency = 59.29KHz

Mode "1024x768*"

DotClock 81

HTimings 1024 1120 1272 1368 Vtimings 768 788 801 847

EndMode

# Refresh rate = 63.87Hz; Horizontal Frequency = 57.99kHz

Mode "1152x864"

DotClock 90

HTimings 1152 1248 1472 1552 Vtimings 864 864 876 908

EndMode

# Refresh rate = 63.87Hz; Horizontal Frequency = 57.99kHz

Mode "1152x900"

DotClock 90

HTimings 1152 1248 1472 1552 Vtimings 900 900 914 946

EndMode

# Refresh rate = 59.43Hz; Horizontal Frequency = 59.91kHz

Mode "1280x960"

DotClock 104

HTimings 1280 1376 1672 1736 Vtimings 960 960 480 491 525

EndMode

EndSection
```
#Date: 22 Sep 94 10:25:06 -0700 (PDT)
#From: Ken Lata <klatta@pkdl5.syntax.com>
Section "Monitor"
Identifier "ViewSonic 6"
VendorName "ViewSonic"
ModelName "6"
Bandwidth 80.0
HorizSync 30.00-57.00
VertRefresh 43.00-70.04
Mode "640x480"
DotClock 25
HTimings 640 664 760 800 Vtimings 480 491 525
EndMode
Mode "1024x768"
DotClock 80
DotClock 65
HTimings 1024 1080 1304 1328 Vtimings 768 768 776 792
HTimings 1024 1136 1340 1432 Vtimings 768 774 805
EndMode
EndSection

```
#From: haw30@eng.amdahl.com (Henry Worth)

#Date: Tue, 27 Sep 94 22:10:01 PDT

Section "Monitor"

Identifier "ViewSonic-7"

VendorName "ViewSonic"

ModelName "ViewSonic-7"

Width 110

HorizSync 30.0-64.0

VertRefresh 50.0-90.0

Modeline "1152x900*" 85 1152 1218 1328 1456 900 902 912 943

Modeline "1024x768*" 80 1024 1032 1216 1344 768 773 832

Modeline "1024x768*" 75 1024 1048 1184 1328 768 771 777 802

Modeline "1024x768*" 65 1024 1032 1208 1288 768 773 798

Modeline "800x600*" 45 800 828 920 600 605 615 635

Modeline "640x480*" 30 640 664 728 800 484 490 507

Modeline "640x480*" 28 640 664 728 792 484 480 495 505
```

## S3 芯片组信息

XFree6 Project Inc. 1995年7月

当前的 S3 Server 支持以下 S3 芯片组：`911`, `924`, `801/805`, `928`, `732` (Trio32), `764` (Trio64), `864`, `368`, `964`。S3 server 会识别该芯片，但尚未在该芯片组进行测试。如果你在这些组上遇到任何问题或取得成功，请向我们报告。尽管如此，这不足以支持所有使用这些芯片组的板。以下列表包含了一些已知运行的板的数据。如果你的显卡与描述的相似，那么它对你也可能有效。

### S3 801/805, AT&T 20C49（或类似）RAMDAC

- Orchid 1280+ VLB
- Actix GE32- 8 和 15/16 bpp

注意：真实的 AT&T20C490 RAMDAC 应由服务器自动检测。对于其他兼容设备，你需要在 `XF86Config` 中提供 `Ramdac "att20c490"` 项。真实的 T2C490 或 20C41 RAMDAC 支持 `dac_8_bit` 。某些克隆版本（如 Winbond 82C490）不支持。

### S3 805 VLB, S3 GENDAC（RAMDAC + 时钟合成器）

105D（适用于 VLB 和 PCI）尚不清楚所有 10SD 是否使用 S3 GENDAC-8 和 15/16 bpp

```
ClockChip "s3gendac"
RamD "s3gendac"
```

### S3 801/805, AT&T 20C490 RAMDAC, ICD2061A Clockchip- STB PowerT20490 RAMDAC 应由服务器自动检测。对于其他兼容设备，你需要在 `XF86Config` 中提供 `Ramdac "att20c490"` 项。

```
ClockChip "icd2061a"
RamD "att20c490"
Option "dac_8_bit"
```

S3 805, Diamond SS2410 RAMDAC, ICD2061A Clockchip- Diamond Stealth 24 VLB

- 8 和 15bpp(*) 只需要 `Option "nonlinear"`

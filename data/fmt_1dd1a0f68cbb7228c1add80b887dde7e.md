
# Monitor 配置集合

## ModelLine 示例

```
ModelLine "640x480" 31 64 664 704 832 480 489 492 520
ModelLine "800x600" 50 80 856 976 1040 600 637 643 666 +hsync +vsync
ModelLine "1024x768*" 44 1024 1040 1216 1264 768 777 785 817 1212
ModelLine "1024x768*" 75 1024 1072 1184 1328 768 777 780 800 -hsync -vsync
ModelLine "1280x1024*" 80 1280 1296 1512 1568 1024 1025 1037 1165 interlace
ModelLine "1280x1024*" 110 1280 1360 1428 1720 1024 1025 1036 1065
EndSection
```

## From: David Dawes <dawes@Free86.org>
#Date: 1994年9月16日星期五 12:40:+0100 (EST)
# GTA - 将点时频率从 25 改为 25.2

```
Section "Monitor"
Identifier "通用显示器"
VendorName "未知"
ModelName "未知"
Bandwidth 25.2
HorizSync 31.5
VertRefresh 60
Mode "640x480"
DotClock 25.2
Timings 640 664 760 800 480 491 523
EndSection
```

## From: Leonard N. Zuboff <inz@dandelion.com>
#:Date: 1994年9月16日星期五 23:16:00

```
Section "Monitor"
Identifier "HP 1280x1024-72"
VendorName "Hewlett-Packard"
ModelName "A1097*"
Bandwidth 135
HorizSync 78.125
VertRefresh 72.00
Mode "1280x1024"
DotClock 135.00
Timings 1280 1344 1536 1728 1024 1027 1030 1085
```

## From: Gertjan Akkerman <akkerman@dut.nl>
#:Date: 1994年9月20日星期二 11:45:21 +0200 (MET 夏令时间)

```
Section "Monitor*"
Identifier "Highscreen 1024"
VendorName "Vobis"
ModelName "1024"
Bandwidth 45
HorizSync 31.4-31.6, 35.1-35.2, 35.5-35.6 kHz
VertRefresh 50-87 Hz
Mode "640x480*" 25.2 640 664 760 800 480 491 525
Mode "800x600*" 36.0 800 824 896 1024 601 625
Mode "1024x768*" 44.9 1024 1040 1216 1266 768 777 817
```

## From: Rich Murphy
#:Date: 1994年9月15日星期四 23:30:52
#From <richw.slip.bcm.tmc.edu>

```
Section "Monitor*"
Identifier "Hitachi SuperScan 20S"
VendorName "Hitachi"
ModelName "SuperScan 20S model. CM2095MU"
Bandwidth 100.0
HorizSync 30-69
VertRefresh 50-100
ModeLine "1152x1085*" 85 1152 1192 1384 1480 900 925 955
```

## From: Rogier Wolff <wolff@dutai.telt.nl>
#:Date: 1994年9月24日星期六 17:27:09 +0200 (MET 夏令时间)
# 此显示器支持 VESA 640x480@60Hz, 800x600@58Hz 以及 1024x768i@43Hz。

```
Section "Monitor*"
Identifier "Hyundai hcm-421E"
VendorName "Hyundai"
ModelName "421E"
Bandwidth 110
HorizSync 30-36
VertRefresh 43-72
ModeLine "640x480*" 25.175 640 664 760 800 480 491 525
```

## From: Chris Mason <cmason@mail.csh.rit.edu>
#:Date: 1994年9月22日星期四 01:38:45 -0400

```
Section "Monitor*"
Identifier "IDEK VisionMaster 17 (1)*"
# was: "IDEK 8617*"
VendorName "IDEK"
ModelName "8617"
Bandwidth 135
HorizSync 31.5-85.0
VertRefresh 60-80
ModelLine "800x600" 49 800 816 932 996 600 612 635
ModelLine "1024x768" 85 1024 1028 1296 1348 768 769 775 804
ModelLine "1280x1024.1" 135 1280 1296 1456 1726 1024 1025 1066
ModelLine "1280x1281.1" 135 1280 1284 1456 1661 1128 1129 1132
```

## From: Andrew Dyer <adyer@amiop.chi.us>
#:Date: 1994年9月21日星期三 22:22:42 +0100

```
Section "Monitor"
Identifier "IDEK VisionMaster 17 (2)"
was: "IDEK-8617"
VendorName "IDEK"
ModelName "MF-8617"
Bandwidth 135.0
HorizSync 23.5-86.0
VertRefresh 50-120
Mode "640x480" 25 640 672 768 800 480 490
Mode "800x600" 40 800 840 968 1032 600 601 625
Mode "1024x768" 80 1024 1032 1216 1344 768 773
Mode "1024x768" 75 1024 1056 1218 1368 768 770 806
Mode "1152x900" 85 1152 1284 1416 1560 900 941
8 "1280x1024" 135 1280 1312 1456 1024 1024
1064
```

## From: Richard Cole <rcole@pyra.uk>
#:Date: 1994年9月15日星期四 12:29:10 +010 (BST)

```
Section "Monitor"
Identifier "IDEK Vision Master 17 (4)"
VendorName "LIAMA"
ModelName "MF8617"
BandWidth 135.0
HorizSync 23.5-86.0
VertRefresh 50-120
Mode "1024x768" 80 1024 1032 1216 1344 768 773
Mode "800x600" 32 800 832 976 1016 600 606 634 +hsync +vsync
Mode "640x480" 25 640 672 768 800 480 490 525 +hsync +vsync
```

## From: Bob Mende Pie <mende@computer.rutgers>
#:Date: 1994年9月23日星期五 22:51:51 -0400

```
Section "Monitor"
Identifier "IDEK Vision Master 17 (5)"
Was: "Idek 8617"
VendorName "Idek"
ModelName "8617"
Bandwidth 135.0
HorizSync 23.5-86.0 # 此处修改！
VertRefresh 50-120 # 此处修改！
```

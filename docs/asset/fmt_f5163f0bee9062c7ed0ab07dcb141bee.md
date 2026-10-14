
```
root@host:~# lpoptions -p laserjet41 -l

RE/RE Setting: Dark Light *Medium Off

Toner/Toner Density: 1 2 3 4 5

Dithering/Flow-Steinberg Dithering: *Normal PSDithered

Manual/Manual Feed of Page: Off On

InputSource/Media Source: Tray 2 Tray 3 Tray 4 Envelope Auto

Copies/Number of Copies: *1 2 3 4 5 6 7 8 9 10 11 12 13 [ .. ] 100

PageSize/Page Size: *A4 Letter 11x17 A3 B5 B5 EnvoC5 EnvVDL

PageRegion/PageRegion: A4 Letter 11x17 A3 B5 B5 EnvoC5 EnvVDL

Resolution/Resolution: 75x75dpi 150x150dpi *300x300dpi

EconomyMode/Toner Saving: *Off On
```

要更改选项，可以执行如下操作：

```
lpoptions -p laserjet41 -o TonerDensity=5 -o Resolution=150x150dpi
```

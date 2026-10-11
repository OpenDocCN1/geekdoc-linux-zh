**Table 10.1** Mouse types available in KickStart (continued).

| Type | Used For |
| :--- | :--- |
| **logiman+ps/2** | PS/2 Logitech MouseMan+/FirstMouse+ |
| **microsoft** | Microsoft-compatible serial mouse |
| **msnew** | Microsoft serial mouse Revision 2.1A or higher |
| **msintelli** | Serial Microsoft IntelliMouse |
| **msintellips/2** | PS/2 Microsoft IntelliMouse |
| **msbm** | Microsoft bus (PS/2) mouse |
| **mousesytems** | Serial Mouse Systems mouse |
| **mmseries** | Serial MM Series mouse |
| **mmhittab** | Serial MM HitTablet mouse

After the mouse identification comes the time zone, which is set with the **timezone** item. Many options are available, depending on what country you are in and whether the country is large enough to span multiple time zones. Some commonly used zones are shown in Figure 10.1— for the rest, run the **timeconfig** command to find your time zone. Along with the time zones, you can tell your system to use Greenwich Mean Time (GMT) by adding the **--utc** flag. In my KickStart file, this line might look like this:

```
timezone --utc Canada/Pacific
```

![](bbox=[0.13, 0.61, 0.95, 0.91])
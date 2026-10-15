# DOS Gaming Configuration

This section covers games designed for pure DOS mode, which includes pre-Windows 95 titles, as well as those you might be able to install or launch from Windows but have to run from a pure DOS environment, either by exiting to DOS first or by shutting down Windows as soon as you double-click the icon.

> Some classic game compendiums allow or require you to install games from Windows 95 or better, but they actually only run in a pure DOS setting.

Memory configuration is the major headache for DOS games. The good news is that for games that work at all in VMware, the default memory configuration of most MS-DOS and DR-DOS installations works perfectly well. In general, this ideal memory configuration consists of these two lines in the DOS CONFIG.SYS file:

```
DEVICE=C:\DOS\HIMEM.SYS (or C:\DRDOS\HIMEM.SYS)
DOS=HIGH, UMB
```

As long as you allocate at least 8 to 16MB to your DOS virtual machine, you should rarely, if ever, have a problem with not having enough overall memory. You might be too low on conventional memory, which is defined as the first 640KB of memory available to DOS and the space in which programs are directly executed. By typing mem at a DOS prompt, as shown in Figure 15.4, you can get a sense of how much conventional memory is available.

![](bbox=[0.25, 0.74, 0.72, 0.9])

Figure 15.4 The mem command tells you how much conventional memory is available to run DOS games.
```
tschenk@quicksilver:~ [1042]$ cat /proc/interrupts
CPU0
0: 80221572 XT-PIC timer
1: 358387 XT-PIC keyboard
2: 0 XT-PIC cascade
3: 2532364 XT-PIC serial
4: 692835 XT-PIC serial
5: 7 XT-PIC soundblaster
6: 2 XT-PIC rtc
9: 18096 XT-PIC aic7xxx
11: 697549 XT-PIC DC21140 (eth0)
12: 502952 XT-PIC BusLogic BT-958
13: 1 XT-PIC fpu
14: 868012 XT-PIC ide0
NMI: 0
```

```
tschenk@quicksilver:~ [1043]$ cat /proc/dma
1: SoundBlaster8
4: cascade
5: SoundBlaster16
```

```
tschenk@quicksilver:~ [1044]$ cat /proc/ioports
0000-001f : dma1
0020-003f : pic1
0040-005f : timer
0060-006f : keyboard
0070-007f : rtc
0080-008f : dma page reg
00a0-00bf : pic2
00c0-00df : dma2
00f0-00ff : fpu
01f0-01f7 : ide0
0220-022f : soundblaster
0278-02ff : serial(auto)
0330-0333 : MPU-401 UART
03b0-03df : vga+
03e8-03ef : serial(auto)
03f6-03f6 : ide0
03f8-03ff : serial(auto)
0620-0623 : sound driver (AWE32)
0a20-0a23 : sound driver (AWE32)
0e20-0e23 : sound driver (AWE32)
6000-60be : aic7xxx
```
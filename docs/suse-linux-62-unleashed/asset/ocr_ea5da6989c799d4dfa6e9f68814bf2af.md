# Games
CHAPTER 30
953

```
# insmod uart401
Using /lib/modules/2.2.10/uart401.o
# insmod sb io=0x220 irq=5 dma=1
Using /lib/modules/2.2.10/sb.o
```

You can then see if the sound modules were loaded with the lsmod command, like this:

```
# lsmod
```

| Module | Size | Used by |
| sr_mod | 15820 | 0 (autoclean) (unused) |
| sb | 31256 | 0 |
| uart401 | 5576 | 0 [sb] |
| sound | 55416 | 0 [sb uart401] |
| soundcore | 2084 | 5 [sb sound] |
| soundlow | 208 | 0 [sound] |

You can also try looking out the Linux process directory /proc/sound like this
(your output might look different):

```
# cat /dev/sndstat
OSS/Free:3.8s2++-71130
Load type: Driver loaded as a module
Kernel: Linux presario 2.2.10 #1 Tue Jul 20 16:32:24 MEST 1999 i586
Config options: 0
```

Installed drivers:

Card config:

Audio devices:
0: ESS ES1688 AudioDrive (rev 11) (3.01)

Synth devices:

Midi devices:

Timers:
0: System clock

Mixers:
0: Sound Blaster

![](bbox=[0.855, 0.786, 0.953, 0.925])
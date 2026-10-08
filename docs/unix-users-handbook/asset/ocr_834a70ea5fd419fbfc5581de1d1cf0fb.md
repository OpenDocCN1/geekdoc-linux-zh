|
|---|
| 14:35:04 | 0.00 | 0.0 | 0.00 | 0.0 | 286 |
| 14:36:04 | 0.00 | 0.0 | 0.00 | 0.0 | 295 |
| 14:37:04 | 0.00 | 0.0 | 0.00 | 0.0 | 249 |
| 14:38:04 | 0.00 | 0.0 | 0.00 | 0.0 | 300 |
| 14:39:04 | 0.00 | 0.0 | 0.00 | 0.0 | 296 |
| 14:40:04 | 0.00 | 0.0 | 0.00 | 0.0 | 419 |
| 14:41:04 | 0.00 | 0.0 | 0.00 | 0.0 | 234 |
| 14:42:04 | 0.00 | 0.0 | 0.00 | 0.0 | 237 |
| 14:43:04 | 0.00 | 0.0 | 0.00 | 0.0 | 208 |

Average | 0.70 | 0.0 | 0.70 | 0.0 | 346

# timex to Analyze a Command

![](bbox=[0.03, 0.38, 0.12, 0.47])

If you have a specific command you want to find out more about, you can use **timex**, which reports the elapsed time, user time, and system time spent in the execution of a command you specify.

**timex** is a good command for users because it gives you an idea of the system resources you are consuming when issuing a command. The following two examples show issuing **timex** with no options to get a short output of the amount of cpu consumed, and the second example shows issuing **timex -s** to report “total” system activity on a Solaris system:

```
martyp $ timex listing

real        0.02
user        0.00
sys         0.02

martyp $ timex -s listing

real        0.02
user        0.00
sys         0.01

SunOS 5.7 Generic sun4m     08/21

07:48:30  %usr    %sys    %wio    %idle
07:48:31  32      68      0       0

07:48:30 bread/s read/s %rcache bwrIit/s lwrit/s %wcache pread/s pwrit/s
07:48:31  0       0      100     0       0       100     0       0
Average 0       0      100     0       0       100     0       0

07:48:30 device    %busy avque r+w/s blks/s await avserv
```
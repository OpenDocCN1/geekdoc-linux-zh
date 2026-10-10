
```
total 0
-rw-rw-r-- 1 root 4096 Nov 9 02:25 blinkPeriod
-rw-rw-r-- 1 root 4096 Nov 9 02:25 mode
```
`pi@erpi /sys/erpi/led17 $` `cat` `blinkPeriod`

1000

`pi@erpi /sys/erpi/led17 $` `sudo` `sh -c "echo 100 > blinkPeriod"`

`pi@erpi /sys/erpi/led17 $` `cat` `blinkPeriod`

100

当该 LKM 在 2ms 睡眠持续时间内闪烁时，CPU 负载仅约为 ~0.0%：

```
pi@erpi /sys/erpi/led17 $ sudo sh -c "echo 2 > blinkPeriod"
pi@erpi /sys/erpi/led17 $ ps aux | grep LED
root 27618 0.0 0.0 0 D 02:57 0 [LED_thread]
pi@erpi /sys/erpi/led17 $ sudo sh -c "echo off > mode"
pi@erpi /sys/erpi/led17 $ sudo sh -c "echo on > mode"
pi@erpi /sys/erpi/led17 $ sudo sh -c "echo flash > mode"
pi@erpi /sys/erpi/led17 $ cd /sys/exploringrip/chp16/LED
pi@erpi /exploringrip/chp16/LED $ sudo mod led
```


```
# cdrecord -v speed=4 dev=0,0,0 -data -eject boot.iso
```

这将创建一个可启动的 CD-ROM，并在写入你的设备后弹出新的 CD-ROM。速度（此例中为 `4`）取决于你的 CD 刻录设备的能力。运行带有扫描选项的 `cdrecord` 会返回设备号，例如：

```
# cdrecord -scan
```

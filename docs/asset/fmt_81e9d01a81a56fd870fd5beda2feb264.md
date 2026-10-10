
选项 `-J` `-R` 传递给 `mkisofs` 用于文件系统（在此情况下：带有 Joliet 和 Rock 扩展的 ISO 9660 文件系统），详情请参阅 `mkisofs(8)` 手册页。

`-z` 用于任何中的初始会话刻录：无论是否是多个会话。DVD 设备 `/dev/cd0` 必须根据你的配置进行更改。`-dvd-compat` 参数将关闭磁盘，刻录将不可追加。作为回报，这应该提供与 DVD-ROM 驱动器更好的介质兼容性。

也可以刻录一个预主镜像，例如刻录 `imagefile.iso`，我们将运行：

```
growsofs -dvd-compat -Z /dev/cd0=imagefile.iso
```

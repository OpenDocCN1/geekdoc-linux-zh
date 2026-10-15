
`chgrp scanner /dev/scanner`

```bash
chmod 660 /dev/scanner
```

# 验证安装

安装好 `SANE` 后，您可以验证扫描仪是否已被检测并安装。在终端窗口中输入以下内容：

```bash
scanimage -list-devices
```

您应该看到类似下面的内容：

```
device 'scanimage:dev/scanner' is mustek:0600CZ flatbed scanner
```

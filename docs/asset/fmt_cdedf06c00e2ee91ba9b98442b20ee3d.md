
# 在 GUI 环境中使用可移动介质

由于其大容量和便携性，可移动存储设备经常存储用户在 GUI 环境中经常使用的数据、图片、音乐程序和文档。在 GUI 环境中工作时，进程会自动将可移动介质挂载到目录，你可以立即使用，就像在 Windows 或 macOS 上一样。当你在 GUI 环境中插入 USB 闪存设备、CD 或 DVD 时，系统会自动将其挂载到 `/run/media/username`（`username` 是登录 GUI 环境的用户），它是 CD 或 DVD 上的系统（在刻录软件中指定）。例如，如果你以用户身份登录 GUI 环境并插入一个标签为“Fedora-WS-Live-28-1-1”的 DVD，系统会自动创建 `/run/media/user/Fedora-WS-Live-28-1-1` 目录并将 DVD 挂载其中。同样，如果你以用户身份登录 GUI 环境并插入一个标签为“Kingston”的 USB 闪存设备，系统会自动创建 `/run/media/user/Kingston` 目录并将 USB 闪存设备挂载其中。显示如下：

```
[server1]#df -T

Filesystem Type 1K-blocks Available Use% Mounted on

devtmpfs devtmpfs 2006860 0 2006860 0% /

tmpfs tmpfs 2019492 0 2019492 0% /

tmpfs tmpfs 2019492 1192 2018300 1% /run

tmpfs tmpfs 2019492 0 2019492 0% /sys/fs/cgroup

/dev/sda3 ext4 35826048 8846416 25164216 27% /
```

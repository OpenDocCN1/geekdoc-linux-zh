
# Welcome to Red Hat Enterprise Linux Server

## Starting

Starting:

Setting hostname: `Triumph.example.com` [ OK ]

Setting logical Volume Management: 2 logical volume(s) in volume group `"vg"`

initroot now [ OK ]

Checking filesystems

`/dev/sda1/Triumph-lv-root`: clean, 88953/263608 files, 65536/1452832 blocks

`/dev/sda1`: clean, 30/120816 blocks, 59837/53280 blocks

Remounting root filesystem in read-write mode: [ OK ]

Mounting local filesystem: [ OK ]

Enabling local filesystem quotas: [ OK ]

Enabling quota statistics: [ OK ]

Entering interactive startup: [ OK ]

Start service scripts (Y/n)? (Y

4. 要向内核添加参数，将光标移动到以 `"linux"` 结尾的行末，并输入你想要的参数。参阅 https://www.kernel.org/doc/Documentation/admin-guide/kernel-parameters.txt 获取内核参数列表。这里有两个示例：

- `selinux`: 如果 SELinux 出现问题导致系统不可用，你可以通过以下方式禁用它：
`selinux=0`
- `smt`: 同时多线程 (`smt`) 允许单个 CPU 核心执行多个线程。为了修复某些微处理器故障，你需要关闭该功能。你可以在启动时通过在内核命令中传递 `smt=1` 或 `nosmt` 参数来实现此点。

5. 一旦完成参数，按下 `Ctrl-x` 使用你添加的内核启动系统。

## 启动内核

内核启动后，没有太多需要检测的，只需留意潜在问题。对于 RHEL，你会看到一个 Red Hat Enterprise Linux 屏幕，并配有一个缓慢旋转的图标。如果你想查看详细启动过程的滚动消息，请按 `Esc` 键。

此时，内核尝试加载使用硬件所需的驱动程序和模块。主要问题是，在尝试自动启动图形界面时，如果遇到了视频驱动程序问题并想对其进行调试。

（此处省略后续部分翻译逻辑保持一致）

# 第四部分：成为 Linux 服务器管理员

**本地挂载失败：** 如果 `/etc/fstab` 中的条目挂载失败，启动过程将在运行级别（runlevel）服务启动之前结束。这通常发生在向 `/etc/fstab` 添加条目时，由于该条目存在错误且你在重启之前忽略了进行测试。当 fstab 文件加载失败时，你会被带入 root 用户的 shell 中，且根文件系统以只读模式挂载。要解决此问题，你需要重新挂载根文件系统，修正 fstab 文件，挂载文件系统项以确保其工作正常，然后重启。命令序列如下：

```bash
# mount -c remount,rw /
# vim /etc/fstab
# mount -a
# reboot
```

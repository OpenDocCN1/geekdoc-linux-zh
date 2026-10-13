
- 5. 保存并退出文件。
- 6. 若要在重启时启用重新配置，执行 `touch reconfigure` 并回车。
- 7. 要停止并重启系统，输入 `sync; reboot` 并回车。

更多信息可从 Sun 的 http：http://access1.sun.com/cgi-bin/rinfo2html?226002，“如何在非标准 IRQ 上添加串口”，以及 http://access1.sun.com/cgi-bin/rinfo2html?223402，“向 Solaris 2.6 添加即插用设备”。

## Solaris 7 IA (2.7) 和 COM2

注意。本章节于 1999 年 2 月添加，没有许多读者的帮助是不可能的。贡献者包括 Cagri Yucel (`cyucel@is.ku.edu.tr`) 和 Jim McCusker (`puppy@bios.net`)。感谢大家！

根据你更喜欢操作文件还是点击，选择下方的自动或更手动的方法。

### 自动方法，使用设备配置助手

- 1. 启动机器并在启动过程中按 `ESC` 键进入设备配置助手。
- 2. 选择添加设备或查看/编辑并添加 IO = 2F8 IRQ = 3 的串口。
- 3. 继续重启，Solaris 将自动执行重新配置启动。新端口应该神奇出现。

### 手动方法，使用设备配置助手

- 1. 确保 BIOS 中与调制调器对应的端口是禁用的。
- 2. 启动系统，以 `root` 身份登录，并将以下内容添加到 `/platform/i86pc/kernel/drv/asy.conf`：

```
name="asy" class="sysbus" interrupts=12,4 reg=0x3f8,0,0 ioaddr=0x3f8;

ignore-hardware-nodes=1;

name="asy" class="sysbus" interrupts=12,3 reg=0x2f8,0,0 ioaddr=0x2f8;
```

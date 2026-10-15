
# Section 2: Using Modems

## Tip 11.2.1: Choosing a Modem

Choosing a good modem for your Linux system requires care. There are a lot of modems on the market but not all of them are ideal for Linux.

# 让 Linux 运行起来：核心技巧与技术

Linux 可以使用大多数 PC 调制调器。然而，在为 Linux 选择调制调器时，你应该记住以下几点：

- 由于它们使用了 `LED` 显示灯，用户可以使用这些灯来调试配置问题，并且更容易安装和配置，许多用户更倾向于外部调制调器。

## Note

某些低端打印机使用 `Windows` 打印系统。`IDE` 硬盘对于当今要求密集的桌面应用程序提供了良好的性价比，由于如此，`IDE` 磁盘是今天几乎所有桌面 `PC` 系统预装磁盘的常态。

对于 most home PCs, off-line UPSs will be sufficient. For mission-critical servers and systems with large loads (for example, multimedia PCs with numerous), consider an-online. At the technical level, two types of UPSs are available:

- `Off-line`. `Off-line` UPSs pass `AC` power from the main source straight to the `PC` until the power is lost the `UPS` switches to battery. Generally, lower-end UPSs are off-line.

- `Dumb`. `Dumb` UPSs provide limited communication with connected PCs. They simply signal if the main power source is available, or not, if the battery level is too low.

- `Smart`. `Smart` UPSs extend the communication capabilities of dumb UPSs by adding a control language through which connected PCs can query the `UPS`, set parameters on the `UPS`, and control the `UPS` (including turning it off).

Generally, smart UPSs are not supported by `Linux`. Some smart UPSs can operate in dumb mode and therefore can be used with `Linux`.

A good source of information selecting a `UPS` for `Linux` is the `UPS` `HOWTO` at `http://www.linuxdoc.org/HOWTO/UPS-HOWTO.html`

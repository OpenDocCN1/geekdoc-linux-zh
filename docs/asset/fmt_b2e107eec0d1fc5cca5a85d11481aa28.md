
Plug and Play (`PnP`) is a Microsoft and Intel standard designed to make PCI detection of hardware easier. It has both good and bad effects. Both ISA and PCI devices can be Plug and Play. The PCI bus has been constructed so that every device can be configured with Plug and Play. This is a good thing and makes configuration easier. However, a few ISA cards are also Plug and Play. This makes things complicated because not all Plug and Play devices behave in the same way. The `isnaptools` package has been made to handle these ISA Plug and Play devices.

If you know you Plug and Play devices (and most computer users do...) and your BIOS is Plug and Aware, a setting exists in your configuration.

# 编译自己内核的优势

...（服务器在上面上可以连续运行几个月而没有任何问题），但如果你有奇特的硬件或以异常的方式使用计算机，可能会遇到问题。这些问题随着时间的推移得到了修复，因此获取最新、最稳定的内核可能会消除问题。

> 有时，Red Hat 会发布更新的编译好的内核，通常在所交付的版本中发现严重漏洞时。然而，如果你想跟上那些较小的修复，你必须自己进行编译。

此外，编译自己的内核允许你根据需要选择并包含你想要的部分。毕竟，内核中（或任何软件中）的代码越少，出现问题的几率就越低。

## 特性

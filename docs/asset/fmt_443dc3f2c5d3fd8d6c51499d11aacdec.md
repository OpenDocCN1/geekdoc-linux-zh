
`linux-2.6.14/arch/ppc/platforms/Makefile`

`linux-2.6.14/arch/ppc/platforms/powerdna.c`

`linux-2.6.14/arch/ppc/platforms/powerdna.h`

`linux-2.6.14/drivers/net/fec_mpc52xx/fec.c`

`linux-2.6.14/drivers/net/fec_mpc52xx/fec.h`

`linux-2.6.14/drivers/net/fec_mpc52xx/fec_phy.h`

`linux-2.6.14/include/asm-ppc/mpc52xx.h`

第一个文件是默认配置，它基于默认值启用了快速的内核配置。通过如下方式调用 `make` 即可启用它：

```text
$ make ARCH=ppc CROSS_COMPILE=<cross- prefix> powerdna_defconfig
```

我们已经讨论过对 Kconfig 文件的更改。对 makefile 的修改很简单——其目的是添加基于 `CONFIG_POWERDNA` 的新内核配置支持。更改内容包括添加一行：

```text
obj-$(CONFIG_POWERDNA)		+= powerdna.o
```

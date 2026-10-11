
![](img/739a35b59067f8a55eff80a58765146f_392_0.png)

© 2016 NXP B.V.

将这些信号 (`CSPI1_CLK`, `CSPI1_MISO`, `CSPI1_CSO`) 连接到 DC934 J1 连接器的信号 (`CS`, `SCK`, `MISO`) 这些信号连接到 LTC2422 spi 设备）。忘记在 i.MX6 SABRE 板板和 DC934 板板之间连接 GND。

![](img/739a35b59067f8a55eff80a58765146f_392_1.png)

你必须像所示添加设备树项，允许用户空间访问 `spidev` 驱动：

```
spidev@0 {
    compatible = "spidev";
    reg = <0>; /* reg 是 cs-gpios 列表中的索引 */
    spi-max-frequency = <1000000>;
};
```

`ecspi` 驱动代码通过 "`speed_hz`" 设置频率。如果未声明，则它将 `spi-max-frequency` 视为实际频率。

# 从用户空间测试 SPI

## 1. 配置内核-imx 并添加 addidev 驱动

Device Drivers -> SPI support -> <> User mode spi device driver。编译新镜象并将其复制到 tftp 文件夹：

```bash
~my-linux-imx$ make menuconfig ARCH=arm
~/my-linux-imx$ source /opt/poky/1.7/environment-setup-cortexa9hf-vfp-poky-linux-gnueabi
~/my-linux-imx$ make zImage
~/my-linux-imx$ cp /arch/arm/zImage /var/lib/tftpboot
```

## 2. 在设备树中添加 spidev

在 `ecspi1` 节点内部向设备树文件 `imx6adl-sabresd.dtsi`（位于 Linux/`/arch/arm/boot/dts`）中添加 "`spidev`" 。一旦 `spidev` 驱动加载，`/dev/spidev0` 将被创建。

### ecspi1

```text
ecspi1 {
    fsl,spi-num-chipselects = <1>;
    ncs-gpios = <<gpio4 9 0>;
    pintrl-names = "default";
    pintrl-0 = <%pintrl_ecspi1>;
    status = "okay";

    chip:spidev0 {
        compatible = "spidev";
        spi-max-frequency = <200000000>; /* SPI CLK Hz */
        reg = <0>;
    }

    m25p8080 {
        #address-cells = <1>;
        #size-cells = <1>;
        compatible = "st,m25p32";
        spi-max-frequency = <200000000>;
        reg = <0>;
    }
};
```

## 3. 构建新的设备树并将其复制到 tftp 文件夹

```bash
~my-linux-imx$ source /opt/poky/1.7/environment-setup-cortex9hf-neon-poky-linux-gnueabi
~/my-linux-imx$ make imx66q-sabresd.dt
~/my-linux-imx$ cp /arch/arm/boot/dt/imx66q-sabresd.dt /var/lib/tftpboot
```

## 4. 在 my_apps 项目中创建 LTC2422-spidev 应用

修改 Makefile 并部署 LTC2422-spidev。

# Listing 9-3: LTC2422_spidev.c


第一个节点为 `i2C` 控制器添加了多个属性。在第二个节点中，你可以看到 `pinctrl-0` 属性，它指向 `i2c1_pins` 配置节点，该节点配置了 I2C 模式下的控制器引脚。`i2C` 控制器在 `/arch/arm/boot/dts/` 的 `bcm2835.dtsi` 文件中描述：

```
i2c1: i2c@7e0040 {
  compatible = "brcm,cm2835-i2c";
  reg = <0x7e0040>
  interrupts = <23 1>;
  clocks = <BCM2835_CLOCK>;
  address-cells = <1>;
  size-cells = <0>;
  status = "disabled";
};
```

在 7.5 中，你为 `bcm2710-rpi-3.dts` 文件中的 `i2c` 和 `gpio` 节点添加了以下子节点和属性：

```
&i2c1 {
  pinctrl-names = "default";
  pinctrl-0 = <&i2c1_pins>;
  clock-frequency = <100000>;
  status = "okay";

cy8c9520: cy8c9520@20 {
  compatible = "cy8c9520";
  reg = <0x20>;
  interrupt-controller;
  interrupt-cells = <2>;
  gpio-controller;
  gpio-cells = <2>;
  interrupts = <23 1>; interrupt-parent = &gpio;

  pwm-cells = <2>;
  pwm0 = <2>; // pwm不支持
  pwm1 = <3>;
  pwm2 = <2>; // pwm不支持
  pwm3 = <2>;

  pinctrl-names = "default";
  pinctrl-0 = &accel_int_pin &cy8c9520_pullups &cy8c9520_pullldowns;
};

cy8c9520_pullups: pinmux1 {
    pins = "gpio0", "gpio1";
    bias-pull-up;
};

cy8c9520_pullldowns: pinmux2 {
    pins = "gpio2";
    bias-pull-down;
};

/* pwm通道 */
cy8c9520_drive_strength: pinmux3 {
    pins = "gpio3";
    drive-strength;
};
```

该叠加层将被编译为 `.dtbo` 文件。要进行编译，需要在内核源码树的 `arch/arm/dts/overlays/Makefile` 中引用它：

```
[...]
upstream.dtbo
upstream-pi14.dtbo
vc4-kms-v3d.dtbo
vc4-kms-7inch.dtbo
vc4-kms-v3d.dtbo
vc4-kms-pi14.dtbo
vga66.dtbo
w1-gpio.dtbo
w1-gpio-pullup.dtbo
w5500.dtbo
wittipy.dtbo
cy8c9520a.dtbo
```

```
&gpio {
  spi0_pins: spi0_pins {
    pins = <9 10 11>;
    function = <4>; /* alt0 */
  };

  spi0_cs_pins: spi0_cs_pins {
    pins = <8 7>;
    function = <1>; /* 输出 */
  };

  i2c0_pins: i2c0 {
    pins = <0 1>;
    function = <4>;
  };

  i2c1_pins: i2c1 {
    pins = <2 3>;
    function = <4>;
  };

  ...

  accel_int_pin: accel_int_pin {
    pins = <23>;
    function = <0>; /* 输入 */
    pull = <0>; /* 无 */
  };
}
```

现在，你将移除或注释之前的粗体代码以测试在实验 7.6 中开发的设备树叠加层。你还将像下面的代码段所示注释 `int_gpio` 节点，以避免在编译设备树时出现错误。在本实验中，你将使用 `gpio_int` 从用户空间请求 CY8C9520A 中断。

```
int_gpio {
  compatible = "arrow,int_gpio_expand";
  pinctrl-names = "default";
  interrupt-parent = <&cy8c9520>;
  interrupts = <0 IRQ_TYPE_EDGE_BOTH>;
}
```

你可以查看下方的 I2C 覆盖层 (`i2c-overlay.dts`)，它位于 `arch/arm/boot/dts/overlays/` 文件夹中：

```
/dts-v1/
/plugin;
```

```
{
  compatible = "brcm,bcm2835";

fragment@0 {
  target = <i2c1>;
  __overlay__ {
    status = "okay";
    pinctrl-names = "default";
    pinctrl-0 = <i2c1_pins>;
  }
}

fragment@1 {
  target = <i2c1_pins>;
  pins1: __overlay__ {
    brcm, pins = <2 3>;
    brcm, function = <4>; /* alt 0 */
  };
}

fragment@2 {
  target = <i2c1_pins>;
  pins2: __dormant__ {
    brcm, pins = <44 45>;
    brcm, function = <6>; /* alt 2 */
  };
}

fragment@3 {
  target = <i2c1>;
  __dormant__ {
    compatible = "brcm,bcm2708-i2c";
  }
}

__overrides__ {
  pins_2_3 = <0>,"1=2";
  pins_44_45 = <0>,"1=2";
  combine = <0>,"1=3";
};
```

为了避免需要大量的设备树覆盖层（Device Tree overlays），并减少外设用户修改 DT 文件的需求，树莓派加载程序支持了一项新功能 - 设备树参数（Device Tree parameters）。这些参数通过在根节点下添加 `__overrides__` 节点在 DT 中定义。你可以在以下树莓派文档的链接中阅读有关不同类型的参数：

# 第 7 章

## 设备驱动程序中的中断处理

https://www.raspberrypi.org/documentation/configuration/device-tree.md

`I2C1` 覆盖层将使用 `overlay/fragment` 参数。DT 参数机制具有若干局限性，包括在使用参数时无法更改节点名称，也无法向任意属性写入任意值。克服这些局限性的方法之一是根据条件包含或排除某些片段（fragments）。通过将 `_overlay_` 节点重命名为 `_dormant_`，可以将该片段从最终合并过程中排除（禁用）。参数声明语法已扩展，允许使用非零零 `target` 属性指示后续字符串包含在 `fragment` 或 `overlay` 范围内的操作。目前已实现四种操作：

```
+cn
+// Enable fragment <n>
-cn Disable fragment <n>
+cn 如果分配的参数值为 true，则启用 fragment <n>，否则禁用
-cn 如果分配的参数值为 false，则启用 fragment <n>，否则禁用
```

下方是 `I2C1` 的 `_overlay_` 节点中包含的属性含义：

```
__overrides {
pins_2_3 = <>,"!2"; // 如果值为 true，pins_2_3 参数将启用 fragment 1 并禁用 fragment 2
pins_44_45 = <>,"!2"; // 如果值为 true，pins_44_45 参数将启用 fragment 2 并禁用 fragment 1
combine = <>,"3"; // 如果分配的参数值为 false，则启用 fragment 3，否则禁用；
}
```

编译修改后的设备树和设备覆盖层，并将它们复制到树莓派设备：

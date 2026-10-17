
```dts
&pi0 {
    names = "default";
    pinctrl-0 = &spi0_pins &spi0_cs_pins;
    cs-gpios = &gpio 8, &gpio 7;

    /* CE0 */
    spidev@ {
        compatible = "spidev";
        reg = <0>;
        address-cells = <1>;
        size-cells = <0>;
        spi-max-frequency = 1250000;
    };

    /* CE1 */
    spidev@ {
        compatible = "spidev";
        reg = <1>;
        address-cells = <1>;
        size-cells = <0>;
        spi-max-frequency = 1250000;
    };

max11300@ {
    size-cells = <0>;
    address-cells = <1>;
    compatible = "maxim,max11300";
    reg = <0>;
    spi-max-frequency = 10000000;

    channel0@ {
        reg = <0>;
        port-mode = PORT_MODE_7;
        AVR = <0>;
        adc-range = ADC_TAGE_RANGE_PLUS10;
        adc-samples = <1>;
    };

    channel1@ {
        reg = <1>;
        port-mode = PORT_MODE_7;
        AVR = <0>;
        adc-range = ADC_TAGE_RANGE_PLUS10;
        adc-samples = <128>;
    };

    channel2@ {
        reg = <2>;
        port-mode = PORT_MODE_5;
        dac-range = DAC_TAGE_RANGE_PLUS10;
    };

    channel3@ {
        reg = <3>;
        port-mode = PORT_MODE_5;
        dac-range = DAC_TAGE_RANGE_PLUS10;
    };

    channel4@ {
        reg = <4>;
        port-mode = PORT_MODE_8;
        AVR = <0>;
        adc-range = ADC_TAGE_RANGE_PLUS10;
        adc-samples = <1>;
        negative-input = <5>;
    };

    channel5@ {
        reg = <5>;
        port-mode = PORT_MODE_9;
        AVR = <0>;
        adc-range = ADC_TAGE_RANGE_PLUS10;
    };

    channel6@ {
        reg = <6>;
        port-mode = PORT_MODE_6;
        AVR = <0>;
        dac-range = DAC_TAGE_RANGE_PLUS10;
    };

    channel7@ {
        reg = <7>;
        port-mode = PORT_MODE_1;
    };

    channel8@ {
        reg = <8>;
        port-mode = PORT_MODE_3;
    };

    channel9@ {
        reg = <9>;
        port-mode = PORT_MODE_0;
    };

    channel10@ {
        reg = <10>;
        port-mode = PORT_MODE_0;
    };

    channel11@ {
        reg = <11>;
        port-mode = PORT_MODE_0;
    };

    channel12@ {
        reg = <12>;
        port-mode = PORT_MODE_0;
    };

    channel13@ {
        reg = <13>;
        port-mode = PORT_MODE_0;
    };

    channel14@ {
        reg = <14>;
        port-mode = PORT_MODE_0;
    };

    channel15@ {
        reg = <15>;
        port-mode = PORT_MODE_0;
    };

    channel16@ {
        reg = <16>;
        port-mode = PORT_MODE_0;
    };

    channel17@ {
        reg = <17>;
        port-mode = PORT_MODE_0;
    };

    channel18@ {
        reg = <18>;
        port-mode = PORT_MODE_1;
    };

    channel19@ {
        reg = <19>;
        port-mode = PORT_MODE_3;
    };

    /*Accel: ADXL1345@
    compatible = "arrow,adxl1345";
    spi-max-frequency = <5000000>;
    spi-cpl;
    sppi-cph;
    reg = <0>;
    pintrl-0 = &accel_int_pin;
    int-pios = &gpio 23 0>;
    interrupts = <23 1>;
    interrupt-parent = &gpio>
    */
    ;
};
```

你还需要在 `bcm2710-rpi-3-b.dts` 中包含新的头文件：

```dts
#include "bcm2710-rpi-3-b.dts"
#include "dt-bindings/iio/spi.h"
#include "dt-bindings/iio/maxim,max1300.h"
```

`maxim,max1300.h` 文件包含了用于通道子节点的 DT 值。你必须将 `maxim,max1300.h` 文件放在内核源码的 `iio` 文件夹下：

`maxim,max1300.h` 的内容所示：

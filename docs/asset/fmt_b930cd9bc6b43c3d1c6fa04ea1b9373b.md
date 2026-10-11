
```c
    device_for_each_child_node(st->dev, dev, child) {
        ret = device_property_read_u32(child, "reg", &reg);
        if (ret || reg >= ARRAY_SIZE(st->port_modes))
            continue;

        /* 将 DT "port_mode" 属性的值存储在全局结构中，
         * 以便在驱动程序的其他函数中知道每个端口的模式 */
        ret = device_property_read_u32(child, "port_mode", &tmp);
        if (!ret) {
            st->port_modes[reg] = tmp;
        } else {
            dev_info(st->dev, "port-mode found");
            continue;
        }

        /* 根据使用的 "port_mode" 属性存储其他 DT 属性 */
        switch (st->port_modes[reg]) {
        case PORT_MODE_7:
            ret = device_property_read_u32(child, "adc-range", &tmp);
            if (!ret)
                st->adc_range[reg] = tmp;
            else
                dev_info(st->dev, "Get default ADC range");
            ret = device_property_read_u32(child, "AVR", &tmp);
            if (!ret)
                st->adc_reference[reg] = tmp;
            else
                dev_info(st->dev, "Get default ADC reference");
            ret = device_property_read_u32(child, "adc-samples", &tmp);
            if (!ret)
                st->adc_samples[reg] = tmp;
            else
                dev_info(st->dev, "Get default ADC sampling");
            dev_info(st->dev, "the channel %d is set in port mode %d\n", reg, st->port_modes[reg]);
            break;

        case PORT_MODE_8:
            ret = device_property_read_u32(child, "adc-range", &tmp);
            if (!ret)
                st->adc_range[reg] = tmp;
            else
                dev_info(st->dev, "Get default ADC range");
            ret = device_property_read_u32(child, "AVR", &tmp);
            if (!ret)
                st->adc_reference[reg] = tmp;
            else
                dev_info(st->dev, "Get default ADC reference");
            ret = device_property_read_u32(child, "adc-samples", &tmp);
            if (!ret)
                st->adc_samples[reg] = tmp;
            else {
                dev_info(st->dev, "Get default ADC sampling");
                ret = device_property_read_u32(child, "negative-input", &tmp);
                if (!ret)
                    st->negative_port[reg] = tmp;
                else {
                    dev_info(st->dev, "Bad value for negative ADC");
                    return -EINVAL;
                }
            }
            dev_info(st->dev, "the channel %d is set in port mode %d\n", reg, st->port_modes[reg]);
            break;

        case PORT_MODE_9:
        case PORT_MODE_10:
            ret = device_property_read_u32(child, "adc-range", &tmp);
            if (!ret)
                st->adc_range[reg] = tmp;
            else
                dev_info(st->dev, "Get default ADC range");
            ret = device_property_read_u32(child, "AVR", &tmp);
            if (!ret)
                st->adc_reference[reg] = tmp;
            else
                dev_info(st->dev, "Get default ADC reference");
            dev_info(st->dev, "the channel %d is set in port mode %d\n", reg, st->port_modes[reg]);
            break;

        case PORT_MODE_5:
        case PORT_MODE_6:
            ret = device_property_read_u32(child, "dac-range", &tmp);
            if (!ret)
                st->dac_range[reg] = tmp;
            else
                dev_info(st->dev, "Get default DAC range");
            /* 模式6 端口将生成 IIO sysfs 条目，
             * 一个用于写入 DAC 端口，另一个用于读取 ADC 端口 */
            if ((st->port_modes[reg]) == PORT_MODE_6) {
                ret = device_property_read_u32(child, "AVR", &tmp);
                if (!ret)
                    st->adc_reference[reg] = tmp;
                else
                    dev_info(st->dev, "Get default ADC reference");
                /* 获取设置为 mode_6 的端口数量，以便为
                 * 相关 iio 通道分配空间 */
                port_mode_6_count++;
                dev_info(st->dev, "there are %d channels in mode_%d\n", port_mode_6_count, reg);
            }
            dev_info(st->dev, "the channel %d is set in port mode %d\n", reg, st->port_modes[reg]);
            break;

        case PORT_MODE_1: /* 端口在 DT 中配置为 GPIO */
            dev_info(st->dev, "the channel %d is set in port mode %d\n", reg, st->port_modes[reg]);
            /* 将 gpio offset 与端口号绑定，
             * 从 offset = 0 开始 */
            st->gpio_offset[offset] = reg;
            /* 存储每个 gpio offset 的 port_mode，
             * 从 offset = 0 开始 */
            st->gpio_offset_mode[offset] = PORT_MODE_1;
            dev_info(st->dev, "the gpio number %d is using the gpio offset number %d\n", st->gpio_offset[offset], offset);
            /* 增加 gpio offset 和
             * 配置为 GPIO 的端口数量 */
            offset++;
            st->num_gpio++;
            break;

        case PORT_MODE_3: /* 端口在 DT 中配置为 GPO */
            dev_info(st->dev, "the channel %d is set in port mode %d\n", reg, st->port_modes[reg]);
            /* 将 gpio offset 与端口号绑定，
             * 从 offset = 0 开始 */
            st->gpio_offset[offset] = reg;
            break;
        }
    }
}
```

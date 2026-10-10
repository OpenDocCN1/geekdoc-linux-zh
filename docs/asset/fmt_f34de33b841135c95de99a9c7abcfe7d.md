
这种切换可以使用示波器进行可视化。

### 列表 6-1: `/home/pi/flash.bash`

```bash
#!/bin/bash
# 以最高频率切换 GPIO 引脚的短脚本
echo 17 > /sys/class/gpio/export
echo out > /sys/class/gpio/
while true; do
  echo 1 > /sys/class/gpio/gpio17/value
  echo 0 > /sys/class/gpio/gpio17/value
done
```

## GPIO 数字输入

下一个应用是使用 GPIO 作为数字输入，这允许树莓派软件读取按钮或任何逻辑高低电平输入。

如果你从 RPI GPIO 引脚座抽取电流，最大电流也会受到限制。3.3V 引脚座（1 和 17）共同可以提供最大 50 mA。5V 引脚座（2 和 4）共同可以提供约 200 mA–300 mA。对于更大的电流，你需要外部电源，但你必须特别注意，在 RPI 掉电时你的电路不要向 GPIO 引脚供电。

RPI GPIO 是 3.3V 耐压的，每个引脚应仅向外抽取或向内消耗约 2mA–3mA。如果 GPIO 利用率稀疏，每个引脚都能抽取/消耗略大的电流，但最好避免这种依赖关系。在图 6-2 中，使用 5V 电源驱动 LED 是安全的，因为 FET 的漏极-源电路没有连接到栅极输入。你还会注意到，与第 4 章的示例不同，FET 的栅极上没有电阻。在这种特定情况下没有必要，因为 RPi 在该引脚上默认启用了内部下拉电阻。稍后将讨论。

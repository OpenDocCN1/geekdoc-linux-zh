
```c
#include <stdio.h>
#include <stdlib.h>
#include <fcntl.h>
#include <stdint.h>
#include <sys/mman.h>
#include <unistd.h>
#include <string.h>

#define GPIO_BASE 0x3F200000

volatile uint32_t *gpio;

int main() {
    int fd;
    int x;

    if(getuid() != 0) {
        printf("你没有以 root 身份运行。\n");
        return -EPERM;
    }

    if ((fd = open("/dev/mem", O_RDWR | O_SYNC)) < 0) {
        printf("无法打开 /devmem: %s\n", strerror(errno));
        return -EBUSY;
    }

    gpio = (uint32_t *)mmap(0, getpagesize(), PROT_READ | PROT_WRITE, MAP_SHARED, fd, GPIO_BASE);
    if (gpio == MAP_FAILED) {
        printf("内存映射失败: %s\n", strerror(errno));
        return -EBUSY;
    }

    printf("GPIO 操作测试开始。\n");

    // 这里 gpio 指针指向外设基地址。
    // 设置 FSEL17 模式=001 位于 GPIO1 (0004)。
    gpio[1] &= ~(7 << 21);
    gpio[1] |= (1 << 21);

    // 设置 FSEL27 模式=000 位于 GPIO2 (0008)。
    gpio[2] &= ~(7 << 21);
    gpio[2] |= (0 << 21);

    // 注意 FSEL17 和 FSEL27 是位，但在不同的寄存器中。
    while ( { 
        // 使用 GPIOSET0 寄存器上的第 17 位开启 LED
        gpio[6] = (1 << 17);
        // 不要使用非阻塞 - 会延迟！
        usleep(10);
        for(x=0;x<50;x++) { // 使用简单循环进行阻塞延迟
            gpio[7] = (1 << 17); // 关闭 LED
            for(x=0;x<49;x++) { // 为了平衡 while() 而做的延迟技巧
            }
        }
    } while ((gpio[0] & (1<<27)) == 0); // 仅当第 27 位为高平时为真

    printf("按钮被按下 - 程序结束。\n");
    munmap((void *)gpio, getpagesize());
    close(fd);
    return 0;
}
```

# 第 6 章 与树莓派输入/输出接口

此电路处于断开状态，GPIO 状态为高电平，因为上拉电阻将断开的输入“拉高”到 3.3V 线路。可以通过 `sysfs` 观察到这一点（GPIO04 未连接任何电路）：

```
pi@peri /sys/class/gpio echo 4 export
pi@peri /sys/class/gpio $ cd gpio04
pi@peri /sys/class/gpio/gpio04 $ echo in-direction
pi@peri /sys/class/gpio/gpio04 $ cat value
```

**图 6-15：** 列表 6-9 中内存映射示例的输出

![](img/8d97725dcf071daded8acede3920e981_278_0.png)

通过配置图 6-14 中的 `GPUPD` (0094) 寄存器，可以调整该 GPIO 在上拉电阻内部启用拉低电阻，其中 `0x00` =关闭（即禁用），`0x01` = 启用拉低，`0x02` = 启用上拉。此值通过 `GPUDPCLK0` (0098) 寄存器连接时钟输出——即通过设置和移除特定 GPIO 的时钟位。GPIO04 是第 4 位，二进制为 10000 (`0x10`)。因此，要设置 GPIO 启用拉低电阻，首先使用 `0x20000094` 将其他 RPI 上的 `GPUPD` (0094) 寄存器设置为 PI2/3 上的拉低：

```
pi@peri /sys/class/gpio/gpio04 $ sudo -devmem2 0x01 w 0x01
/dev/mem opened. Memory mapped at address 0x76ed3000.
Value at address 0x3F200094 (0x76ed3094): 0x02
```

在 `GPUDCLK0` 寄存器上设置第 4 位，清除 `GPUPD` 寄存器，并从 `GPUDCLK0` 移除时钟控制信号，如下：

```
pi@peri /sys/class/gpio $ sudo -devmem2 0x3F200098 w 0x10
pi@peri /sys/class/gpio/gpio04 $ sudo -devmem2 0x3F200094 w 0x00
pi@peri /sys/class/gpio/gpio04 $ sudo -devmem2 0x3F200098 w 0x00
```

此过程仅将 `GPUPD` 寄存器模式应用到 GPIO04，因为它是 `GPUDCLK0` 寄存器中识别出的唯一 GPIO。

当随后读取 GPIO 时（仍未连接电路），它将返回值为 0，这表明 GPIO4 上现在启用了拉低电阻，而不是之前的上拉电阻：

```
pieri /sys/class/gpio/gpio4 cat value
0
```

若要将 GPIO 恢复置为上拉配置，请使用以下命令：

```
pieri /sys/class/gpio/gpio4 sudo ~ /devmem 0x3F200094 w 0x02
pieri /sys/class/gpio/gpio4 sudo ~ /devmem 0x3F200098 w 0x10
pieri /sys/class/gpio/gpio4 sudo ~ /devmem 0x3F200094 w 0x00
pieri /sys/class/gpio/gpio4 sudo ~ /devmem 0x3F200098 w 0x00
pieri /sys/class/gpio/gpio4 cat value
1
```

## WiringPi

`WiringPi` (www.wiringpi.com) 是一个用于树莓派平台的广泛的 GPIO 控制库，由 Gordon Henderson (@drogen) 编写和维护。该库函数语法与 Arduino Wiring 库类似，是树莓派用户的热门选择。`WiringPi` 库还提供了 Python、Ruby 和 Perl 的第三方绑定。

`WiringPi` 利用了前述描述的 `sysfs` 和内存映射技术，创建了一个为树莓派平台开发的、高效库和命令集。建议在需要快速切换时使用此库来控制树莓派上的 GPIO；但请注意，这种方法在很大程度上特定于树莓派平台，而不是通用的嵌入式 Linux 设备。

### 安装 WiringPi

为了确保你拥有最新版本的 `WiringPi`，请克隆其仓库并并在你的树莓派上直接构建，如下所示：

```
- git clone https://github.com/drogon.net/WiringPi
- cd WiringPi
- make --prefix=$PREFIX install
- make --prefix=$PREFIX
- ls /local/lib/
```

编译好的库会自动复制到 `/local/lib/`，C 头文件被复制到 `/local/include/`，这些路径会被默认库路径包含。如果你在编译 wiringPi 程序遇到困难，请在 `gcc` 调用中添加 `-I/local/include/ -L/local/lib/`。

### gpio 命令

`gpio` 程序作为 `wiringPi` 的一部分，是一个非常实用的命令行工具，用于访问和控制树莓派上的 GPIO。由于历史原因，`wiringPi` 使用的编号方案与物理引脚编号不同。`gpio` 命令可以通过 `-g` 参数来使用 GPIO 编号。

```
gpio -v
```

WiringPi version 2.61

(c) 2018-2021 Gordon Henderson

Website: https://www.wiringpi.org

| 命令 | 示例 | 说明 |
| :--- | :--- | :--- |

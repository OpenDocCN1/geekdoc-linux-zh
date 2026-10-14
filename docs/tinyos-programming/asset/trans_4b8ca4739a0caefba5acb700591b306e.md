

## 2.3 接线与回调

将组件连接的决策留给程序员做的不仅仅是简化在多个服务实现之间切换。它还提供了一种高效的机制来支持回调，我们通过定时器的例子来展示这一点。TinyOS 提供可变数量的周期性或截止时间定时器；与每个定时器相关联的是一个回调，当定时器触发时每次都会执行该函数。我们首先看看在 C 中如何表达这样的定时器，通过修改 Powerup 使 LED 0 以 2 Hz 闪烁，而不是一次打开后就一直保持：

```
#include "mote.h"

timer_t mytimer;

void blink_timer_fired(void)
{
    leds0_toggle();
}

int main()
{
    mote_init();
    timer_start_periodic(&mytimer, 250, blink_timer_fired);
    sleep();
}
```

清单 2.5 C 中的闪烁 LED 的 Powerup

在这个例子中，Blink 应用程序声明了一个全局 mytimer 变量来保存定时器状态，并调用 timer_start_periodic 来设置一个周期为 250 ms 的周期性定时器。每次定时器触发时，定时器实现都会回调在设置定时器时指定的 blink_timer_fired 函数。该函数只是调用一个库函数来切换 LED 0 的开/关。

nesC 版本的 Blink 与 C 版本类似，但使用接口和接线来指定定时器与应用程序之间的连接：

```
module BlinkC {
    uses interface Boot;
    uses interface Timer;
    uses interface Leds;
}
implementation {
    event void Boot.booted() {
        call Timer.startPeriodic(250);
    }
    event void Timer.fired() {
        call Leds.led0Toggle();
    }
}
```

清单 2.6 nesC 中闪烁 LED 的 Powerup（略有简化）

BlinkC 模块在启动时启动周期为 250 ms 的定时器。startPeriodic 命令启动定时器与 fired 事件闪烁 LED 之间的连接是通过将命令和事件放在同一个接口中隐式指定的：

```
interface Timer {
command void startPeriodic(uint32_t interval);
event void fired();
...
}
```

最后，这个 Timer 必须连接到提供实际定时器的组件。BlinkAppC 将 BlinkC.Timer 接线到新分配的定时器 MyTimer：

```
configuration BlinkAppC { implementation { components MainC, LedsC, new TimerC() as MyTimer, BlinkC; BlinkC.Boot -> MainC.Boot; BlinkC.Leds -> LedsC.Leds; BlinkC.Timer -> MyTimer.Timer; } }
```

清单 2.7 闪烁 LED Powerup 配置（略有简化）

在 C 版本中，定时器到应用程序的回调是 timer_start_periodic 函数的运行时参数。定时器实现将此函数指针存储在保存定时器状态的 mytimer 变量中，并在每次定时器触发时执行间接函数调用。相反，在 nesC 版本中，定时器与 Blink 应用程序之间的连接是在 BlinkAppC 中在编译时指定的。这避免了存储函数指针的需要（节省了宝贵的 RAM），并允许 nesC 编译器在回调之间执行优化（特别是内联）。

## 2.4 总结

表 2.1 总结了 C、C++ 和 nesC 中程序结构的不同方式。在 C 中，典型的高级编程单元是文件，其关联的头文件指定并记录了文件的行为。链接器通过匹配全局名称将应用程序从文件构建出来；当这不足以表达程序结构时（例如回调），程序员可以使用函数指针来推迟在何时调用哪个函数的决策。

## 水彩特辑

LOOKING FOR FREEDOM

但自由并不等同于放任，也不是不要技法的“无为”，自由的画水彩反而是建立在熟练的基础之上。

只有掌握了水彩的“脾气”，才能收放自如。

![](img/53ede4f4266a5731b93bff15d85fa06a_40_0.png)

![](img/53ede4f4266a5731b93bff15d85fa06a_40_1.png)

![](img/53ede4f4266a5731b93bff15d85fa06a_40_2.png)

![](img/53ede4f4266a5731b93bff15d85fa06a_40_3.png)

## Part II

## Basic programming


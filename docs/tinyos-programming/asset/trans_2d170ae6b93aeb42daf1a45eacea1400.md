

精度、采样率和抖动要求因应用而异：一个简单的环境监测应用可能每 5 分钟采样几个传感器，而地震监测系统可能每天仅一次采样数秒的加速度，采样频率为数千赫兹。

因此，TinyOS 并未提供统一的方式来访问所有传感器。相反，它定义了一组用于采样传感器的通用接口，以及一组用于构建可访问特定传感器的组件的指导原则。

### 6.2.1 简单采样

两个主要的采样接口是 Read（我们在第 3.4 节中见过）和 ReadStream，分别涵盖获取单个样本和以固定速率采样（抖动低）的情形。作为回顾，Read 提供了一个分阶段的 read 命令，用于启动采样，以及一个 readDone 事件，用于报告样本值和发生的任何错误，适用于任意类型 val_t。

```
interface Read<val_t> {
  command error_t read();
  event void readDone(error_t result, val_t val);
}
```

列表 6.7 Read 接口

与大多数 TinyOS 分阶段接口类似，你一次只能启动一个采样操作，即在 readDone 信号发出前再次调用 read 将会失败（read 不会返回 SUCCESS）。然而（同样与其他分阶段接口一致），在 readDone 事件处理程序中调用 read 是合法的，这使得连续读取变得容易。

我们可以通过检测盗窃企图使防盗应用更真实。一种最初的简单尝试基于以下观察：被盗物品通常被放入袋子和口袋中，即黑暗位置。DarkC 模块通过定期（每隔 DARK_INTERVAL）采样光传感器（使用 Read 接口）并检查光值是否低于某个阈值（DARK_THRESHOLD）来检测黑暗位置。然后它通过点亮黄色 LED（micaZ 上的 LED 2）报告盗窃：

```
module DarkC {
  uses {
    interface Boot;
    interface Leds;
    interface Timer<TMilli> as TheftTimer;
    interface Read<uint16_t> as Light;
  }
}
implementation {
enum { DARK_INTERVAL = 256, DARK_THRESHOLD = 200 };

event void Boot.booted() {
  call TheftTimer.startPeriodic(DARK_INTERVAL);
}

event void TheftTimer.fired() {
  call Light.read(); // Initiate split-phase light sampling
}

/* Light sample completed. Check if it indicates theft */
event void Light.readDone(error_t ok, uint16_t val) {
  if (ok == SUCCESS && val < DARK_THRESHOLD)
    call Leds.led2On(); /* ALERT! ALERT! */
  else
    call Leds.led2Off(); /* Don't leave LED permanently on */
}
}
```

列表 6.8 防盗：检测黑暗条件

我们本可以在现有的 AntiTheftC 模块中实现黑暗检测，并重用现有的 WarningTimer。虽然这会略微减少定时器子系统中的 CPU 和存储需求，但会增加 AntiTheftC 的代码复杂度，因为它混合了两个本质上不相关的活动的代码。通常最好让一个模块专注于一项任务（闪烁 LED、检测黑暗条件）做得很好，而不是构建一个试图处理许多任务的复杂模块，从而付出显著的复杂性代价。

目前，DarkC 非常简单：它在 booted 事件中启动周期性采样。每秒四次，TheftTimer.fired 使用表示光传感器的分阶段 Read 接口（Light）请求新的光样本。如果采样成功（ok == SUCCESS），则将光与指示黑暗条件从而盗窃的阈值进行比较。DarkC 不检查 Light.read 的错误返回值，因为当无法启动光采样时没有有用的恢复操作——它无论如何都会在 1/4 秒后重试检测。

### 6.2.2 传感器组件

传感器在 TinyOS 中由提供 Read 和/或 ReadStream 接口的通用组件表示，并且可能还有其他传感器特定的接口（例如用于校准）。一个组件通常代表一个传感器，例如 mts310 传感器板上的光传感器的 PhotoC：

```
generic configuration PhotoC() {
  provides interface Read<uint16_t>;
}
```

如果两个传感器密切相关（例如加速度计的 X 轴和 Y 轴），它们可能由单个组件提供。同样，如果传感器同时支持单次（Read）


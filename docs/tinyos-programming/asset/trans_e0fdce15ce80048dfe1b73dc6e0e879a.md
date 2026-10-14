

```c
uint16_t accelSamples[ACCEL_NSAMPLES];

task void checkAcceleration();

event void Boot.booted() {
    call TheftTimer.startPeriodic(ACCEL_INTERVAL);
}

event void TheftTimer.fired() {
    // Get 10 samples at 100Hz
    call Accel.postBuffer(accelSamples, ACCEL_NSAMPLES);
    call Accel.read(ACCEL_INTERVAL);
}

/* The acceleration read completed. Post the task to check for theft */
event void Accel.readDone(error_t ok, uint32_t usActualPeriod) {
    if (ok == SUCCESS)
        post checkAcceleration();
}

/* Check if acceleration variance above threshold */
task void checkAcceleration() {
    uint8_t i;
    uint32_t avg, variance;

    for (avg = 0, i = 0; i < ACCEL_NSAMPLES; i++) avg += accelSamples[i];
    avg /= ACCEL_NSAMPLES;
    for (variance = 0, i = 0; i < ACCEL_NSAMPLES; i++)
        variance += (int16_t)(accelSamples[i]-avg)*(int16_t)(accelSamples[i]-avg);

    if (variance > ACCEL_VARIANCE * ACCEL_NSAMPLES)
        call Leds.led2On(); /* ALERT! */
    else
        call Leds.led2Off(); /* Don't leave LED permanently on */
}

event void Accel.bufferDone(error_t ok, uint16_t *buf, uint16_t count) { }
```

## 清单 6.11 防盗：检测移动

MovingC 的基本结构和 DarkC 相同：每秒启动四次采样（TheftTimer.fired），如果采样成功，则检查采样结果以确定它们是否表明发生了盗窃（Accel.readDone）。主要的区别有以下三点：

-   在采样开始前调用 postBuffer 来注册加速度缓冲区
-   MovingC 必须实现 bufferDone 事件，当每个已提交的缓冲区被填满时会发出该事件信号——这里我们不需要做任何事，因为我们只往一个缓冲区中采样
-   样本在一个单独的任务（checkAcceleration）中被检查，以避免 Accel.readDone 的执行时间过长（见 5.2.2 节）

MovingC 的连接配置与 DarkC 相同，只不过它连接的是一个流式加速度计传感器：

```
components new AccelXStreamC();
...
MovingC.Accel -> AccelXStreamC;
```

## 6.3 单跳网络

TinyOS 采用典型的分层网络结构，如图 6.1 所示。网络协议栈由一组层组成，每一层定义了头部和尾部的布局，并为上一层提供一个大小可变的有效载荷空间；最上层（通常是应用程序）只保存应用数据。每一层的头部通常包含一个“类型”字段，用于指明该层有效载荷的含义，进而决定有效载荷的布局——这使得在单个应用程序中使用多个独立的数据包变得容易。例如，在图 6.1 中有两类数据包：一类包含应用程序 1 的消息，构建在 layer2a 之上，而 layer2a 又构建在 layer1 之上；另一类包含应用程序 3 的消息，构建在 layer2b 之上，而 layer2b 又构建在 layer1 之上。

TinyOS 所暴露的最低网络层称为主动消息（Active Messages，AM）[29]。AM 通常直接在节点的射频模块之上实现，提供不可靠的单跳数据包发送和接收。每个数据包由一个 AM 类型标识，这是一个标识数据包类型的 8 位整数。“主动消息”这个名字源于这样一个事实：类型字段被用于将接收到的数据包自动分派到合适的处理程序。从某种意义上说，数据包（消息）是主动的，因为它们通过其类型标识了将要执行的代码。

一个 message_t 类型的变量保存一个 AM 数据包。每个数据包最多可以承载用户指定的有效载荷，长度达 TOSH_DATA_LENGTH 字节——通常为 28 字节，

![](img/53ede4f4266a5731b93bff15d85fa06a_112_0.png)

图 6.1 TinyOS 数据包布局

但可以在编译时将其更改为最多 255 字节。² 注意，增大 TOSH_DATA_LENGTH 会增加每个 message_t 变量的大小，因此可能导致 RAM 使用量大幅增加。

一些简单的节点应用直接构建在 AM 之上，而更复杂的应用通常使用更高级的协议，例如我们将在下一节讨论的分发和收集协议。这些更高级的协议本身也构建在 AM 之上。值得注意的是，用于访问 AM 的接口（AMSend、Receive）有时会在一些高级协议中被复用（例如，树形收集使用 Receive）——这使协议之间的切换更容易，并促进了代码复用。

### 6.3.1 发送数据包

我们的防盗应用目前通过点亮 LED 来报告盗窃，这很可能效果不佳。更好的方法是提醒某人，例如给相关人员发送一条无线电消息。这条消息应将被盗节点的身份标识作为其有效载荷。如第 3.5.3 节所述，TinyOS 的有效载荷始终使用平台无关类型来定义，以确保互操作性。因此，盗窃报告有效载荷的定义是一个简单的平台无关结构体，声明在 antitheft.h 头文件中：

```
#ifndef ANTITHEFT_H
#define ANTITHEFT_H

typedef nx_struct theft {
  nx_uint16_t who;
} theft_t;
...
#endif
```

AMSend（“主动消息发送”）接口包含填充和发送数据包所需的全部命令：

```
interface AMSend {
  command error_t send(am_addr_t addr, message_t* msg, uint8_t len);
  event void sendDone(message_t* msg, error_t error);
  command error_t cancel(message_t* msg);

  command uint8_t maxPayloadLength();
  command void* getPayload(message_t* msg, uint8_t len);
}
```

清单 6.12 AMSend 接口


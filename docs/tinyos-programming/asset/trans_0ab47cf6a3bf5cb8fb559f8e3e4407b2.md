
### 清单13.1 SynchronizerC：SoundLocalizer的时间同步

```
event message_t *RCoordination.receive(message_t *m, void *payload, uint8_t len){
    uint32_t arrivalTime = now(); // Note arrival time.

    if (len == sizeof(coordination_msg_t)) // Validate received message
    {
        coordination_msg_t *cmsg = payload;

        if (... first message from coordinator ...)
        {
            t0 = arrivalTime;
            call VotingTimer.stop();
            call Stats.reset();
        }

        call Stats.data(cmsg->count, arrivalTime - t0);

        // Prepare for event detection when its time is close
        if (cmsg->count >=
            cmsg->sample_at - (MICROPHONE_WARMUP / cmsg->interval) - 3)
            scheduleSampling(cmsg->sample_at);
        return m;
    }
    ...
}
```

这段代码的第一步是通过调用`Counter<TMicro, uint32_t>`接口的`get`命令来记录消息的到达时间。`Counter`是一个与硬件无关的计时接口。与其他时间接口一样，`Counter`接受类型参数，这些参数指示其时间测量的精度（毫秒(`TMilli`)、微秒(`TMicro`)等）和宽度（16位(`uint16_t`)、32位(`uint32_t`)等）：

### 清单13.2 `Counter`接口

```
interface Counter<precision_tag, size_type> {
    async command size_type get();
    async command bool isOverflowPending();
    async command void clearOverflow();
    async event void overflow();
}
```

`get`命令返回当前时间，而其余的命令和事件允许`Counter`用户优雅地处理计数器溢出——一个32位微秒计数器每71分钟溢出一次，一个16位微秒计数器每秒溢出15次，因此处理溢出对许多应用来说是一个实际需求。然而，在SoundLocalizer的情况下，我们可以忽略溢出问题。SynchronizerC将

```
event void RadioControl.stopDone(error_t error) {
  // Once the radio is stopped, schedule event detection
  call Detector.start(t0 + TIME_SHIFT, localSampleTime - t0 - TIME_SHIFT);
}
```

SoundLocalizer在`scheduleSampling`中关闭无线电，因为无线电活动可能导致事件检测中的显著抖动。例如，如果一个不相关的应用程序与SoundLocalizer使用相同的无线电频道，那么SoundLocalizer将接收并处理（并希望忽略）这个其他应用程序的消息。然而，所有这些工作都会影响事件检测，可能导致某些节点延迟检测到响亮的声音，甚至完全错过响亮的声音。

```
interface Detector {
  command void start(uint32_t t0, uint32_t dt);
  async event void detected();
  event void done(error_t ok);
}
```

`start`命令请求在时间`t0+dt`进行事件检测——这种指定时间的方式与TinyOS时序接口使用的基于截止日期的方法一致（参见第6.1.1节）。当DetectorC检测到响亮的声音时，它会立即发出`detected`事件。为了最大化响应速度并最小化抖动，DetectorC的事件检测发生在中断处理程序中，因此`detected`事件是异步的。DetectorC在完成事件检测后的清理工作后，会发出`done`事件（在任务上下文中，以`SUCCESS`作为参数）。此外，如果发生错误，DetectorC将直接发出`done`事件（以`FAIL`作为参数）。

```
norace uint32_t localDetectTime;
uint32_t detectTime;

async event void Detector.detected() {
  localDetectTime = now();
}

event void Detector.done(error_t ok) {
  // If event detection was successful, convert local detection time to
  // a global time, and start broadcasting our detection reports
  if (ok == SUCCESS)
  {
    detectTime = 100000 * call Stats.estimateT0(localDetectTime - t0);
    call VotingTimer.startPeriodic(VOTING_INTERVAL);
    call Leds.led2On(); // Assume we're closest
  }
  call RadioControl.start();
}
```

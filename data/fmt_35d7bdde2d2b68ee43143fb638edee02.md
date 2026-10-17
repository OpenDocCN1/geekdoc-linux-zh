
# 教程

## 13 录制代码

回看我们在开始创建的样本类，你可以看到它正在录制，然后我们添加一个字典到当前位置小节的样本列表中。该字典包含可以播放的样本的引用，还包含了已添加的循环，在必要时可以将其移除。播放和撤销录制的代码见下方：注意，如果直接使用 `btn.play()` 播放声音，那么在播放声音时就不会触发录制。

### 步骤 IV

```python
if self.quantize_n == 0:
    # 录制逻辑
    # ...
```

## 14 完成它

为了完成它，我们需要一个主函数，其中我们加载一些样本并启动主循环。你需要使用 `Ctrl+C` 停止它。快乐演奏！

### 步骤 V

```python
if __name__ == "__main__":
    sampler = PiSampler(tempo=120)
    sampler.add('kick', 'kick01.wav', sampler)
    sampler.add('snare', 'snare01.wav', sampler)
    sampler.add('chord1', 'chord01.wav', sampler)
    sampler.metronome = True
    sampler.run()
```

## 15 可能的改进

对采样器可以进行许多改进。这里：
- 一个用于开启和关闭节拍器
- 能够拉伸样本（如和弦）以适应节奏
- 对文件进行音偏移
- 使用寄存器点亮 LED 时使用更简单的方案
- 保存录制以便以后回放

### 步骤 VI

## 完整代码列表（续）

### 步骤 06

```python
GPIO.setup(undo, GPIO.IN)
GPIO.add_event_detect(undo, GPIO.RISING,
    callback=self.undo_previous_loop,
    bounce_debounce=200)
```

### 步骤 07

```python
@property
def tempo(self):
    return self._tempo
```

```python
@tempo.setter
def tempo(self, value):
    self._tempo = value
    self.seconds_per_beat = 60.0 / value
    self.quantize_per_beat = self.quantize / 4
    self.seconds_per_quantize = self.seconds_per_beat / self.quantize
```

```python
def add(self, sample):
    self.samples.append(sample)
```

```python
@property
def recording(self):
    return self._recording
```

```python
@recording.setter
def recording(self, value):
    self._recording = value
    GPIO.output(output_led, value)
```

```python
def record_next(self, channel):
    self.record_count[channel] += 1
    self.samples.append(sample())
```

### 步骤 13

```python
def play_recording(self):
    for sample in self.recording_data[bar[n_quant]]:
        if sample['loop'] != 1:
            sample['sample'].play()
```

```python
def undo_previous_loop(self, channel):
    if len(self.last_recorded_loop) == 0:
        print("no previous loop to undo")
        return

    loop = self.last_recorded_loop.pop()

    for sample in loop.recording:
        for quantize in bar:
            removes = []

            for sample in quantize:
                if sample['loop'] == loop:
                    removes.append(sample)
```

### 步骤 11

```python
def de_led(self, leds, n):
    count = 0
    for led in leds:
        if count == n:
            GPIO.output(led, True)
```

如果正在录制，将发出声音并添加到录制数据中。在我们编写了 `GPIO` 采样器类后，将清楚它是如何工作的。`GPIO` 事件处理器会将引脚传递给触发事件的事件处理器，因此存在 `channel` 变量但从未被使用。

# 06 采样器初始化

这是采样器类的开头。在值中，`Pygame Mixer` 是缓冲区。如果我们创建了地基，可能需要将其增加到 `1024` 或更高。我们使用字典来存储状态。然后添加节拍器及其音量。我们还创建了一个存储样本。

我们创建了数组来记录样本按下。每个小节（`bar`）都有一个数组。小节每个可能的值有一个数组。小节的值有 `64` 个可能的位置来存储被节拍器击中的。

# 07 Tempo 属性

该变量可以通过自定义的 `setter` 进行调整。当分配一个值时，它会选择一个。在我们的情况下，我们计算需要如何检查录制的音符，以便稍后播放该循环。

# 08 辅助函数

类中有两个函数。其中一个将样本添加到 `samples` 中。另一个则尝试录制下一个循环的开始。有一个函数在循环被录制时运行。现在我们向前跳，处理代码列表末尾的主循环。

# 09 启动主循环

主循环不必执行任何播放样本的工作，因为那是由事件处理器完成的。主循环更新节拍器，更新我们当前处于哪个节拍/小节/量化（`quantize`），并在时更新 LED 和录制。

在循环之前，我们创建了最后的变量。`recorded` 是一个我们用作栈的列表。它是一个字典列表，允许我们通过移除在循环计数位于栈顶部值时录制的每个样本来多次使用录制。

在循环开始时，我们有一个我们创建的 `de-led` 函数。由于 LED 的工作方式与四个 LED 的开启或关闭相同，我们使用一个自定义函数和一组整数，并打开索引为该值的 LED。当我们调用节拍器函数时，它将应用相应的节拍器。然后我们开始一些录制逻辑：如果我们正在录制，则开始；如果我们刚刚录制，则停止，并将循环次数添加到 `last_recorded_loop` 栈中。在此之后我们增加循环计数。

# 制作 Raspberry Pi 采样器

## 完整代码列表（续）

# 10 主循环

这段代码位于录制之后的缩进级别。在处理完 `True` 语句后，我们需要播放已录制的音符。我们可能想在之后这样做。之后，我们可以睡眠直到量化完成。一旦发生，我们必须执行处理量化以及任何与节拍或小节相关的逻辑，如果有必要增加或删除它们。

### 步骤 II

```python
GPIO.output(led, False)
```

# 11 点亮 LED

LED 代码非常简单。它简单地获取你提供的列表中的每个引脚，并用相应的 LED 点亮，关闭所有其他。

### 步骤 III

```python
def de_metronome(self):
    if not self.metronome:
        return
```

```python
if self.beat_n == 0:
    high.play()
else:
    low.play()
```

# 12 节拍器

如果节拍器变量设置为，节拍器将在剩余节拍的第一个节拍或小节上播放音调。

```python
def run(self):
    self.loop_count = 0
    self.last_recorded_loop = []
    self.bar_n = 0
    self.quantize_n = 0
```

```python
While
```

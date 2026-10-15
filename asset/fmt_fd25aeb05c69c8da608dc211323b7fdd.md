
### 09 init 方法

```python
class FreqAnalyser:
    # Filtering based on
    # http://wiki.scipy.org/Cookbook/ButterworthBandpass
    
    def __init__(self, channels, sample_rate, leds=None):
        self.leds = leds  # Not needed if just plotting
        self.channels = channels
        self.sample_rate = sample_rate
        self.nyquist = float(sample_rate) / 2
        
        # Filter order - higher the order the sharper
        # the curve
        order = 3
```

在存储输入参数后，我们计算奈奎斯特频率，它是采样率的一半。奈奎斯特定理指出，任何模拟信号的采样率至少应为模拟频率的两倍。这就是为什么 CD 以 44.1kHz 采样（人类听力范围截止在 20kHz 左右）。然后设计两个巴特沃斯滤波器（一种旨在具有尽可能平坦的频率响应的滤波器）。低通滤波器的截止频率为 200Hz，高通滤波器的截止频率为 4000Hz。这些参数稍后将用于按照这些特性进行过滤。

```python
        # Cut off two frequencies:
        # Low pass filter
        cutoff = 200 / self.nyquist
        # Numerator (b) and denominator (a)
        # polynomials of the filter.
        b, a = butter(order, cutoff, type='lowpass')
        self.low_b = b
        self.low_a = a
        
        # High pass filter
        cutoff = 4000 / self.nyquist
        b, a = butter(order, cutoff, type='highpass')
        self.high_b = b
        self.high_a = a
```

### 10 颜色

最后，我们希望对灯带的颜色变化做出明显且可察觉的效果，并减少闪烁。为了做到这一点，我们可以存储最大值，并使用它让颜色以特定幅度下降，直到歌曲的能量将其推高。下降列表按 `(R, G, B/低音, 中音, 高音)` 的顺序设置每种颜色/频率的速率。颜色的取值范围在 0 到 255 之间。LED 设置的频率为 采样率/`CHUNK`，其中 `CHUNK` 是一次读取的数据量。我们将 `CHUNK` 设置为 512，因此 44100/512 = 每秒 86 次。在设置下降值时请牢记这一点，因为它们取决于你认为看起来如何以及音乐风格。

步骤 10

```python
        # Keep track of max brightness for each colour
        self.max = [0.0, 0.0, 0.0]
        # Make different frequencies fall faster
        # bass needs to be punchy.
        self.fall = [15.0, 2.5, 5.0]
```

### 11 滤波函数

滤波函数相当直观。传入一个名为 `data` 的样本数组，其中样本是 -1.0 到 1.0 之间的值。这是信号处理的标准格式，而 WAV 文件和 CD 中使用的 16 位整数则不然。然后使用我们在步骤 9 中计算好的参数应用低通和高通滤波器。我们通过从原始信号中减去低通和高通滤波器之和来获得中频段。

步骤 11

```python
    def filter(self, data):
        # Apply low filter
        self.low_data = lfilter(self.low_b,
                               self.low_a,
                               data)
        
        # Apply high filter
        self.high_data = lfilter(self.high_b,
                                 self.high_a,
                                 data)
        
        # Get mid data by doing signal - (low + high)
        self.mid_data = np.subtract(data,
                                    np.add(self.low_data,
                                           self.high_data))
```

## 可视化音乐

### 完整代码列表（续）

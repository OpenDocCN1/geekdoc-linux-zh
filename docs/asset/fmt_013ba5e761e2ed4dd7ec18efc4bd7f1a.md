
```
正在创建 socket() 线程
在 inTraverse() 线程中
正在合并 inTraverse() 线程 ************
进入 Traverse() 函数 *
inTraverse(): 正在等待 audio_config ..
butime:
Inf socket():
等待音频配置
=================
rtsetparams: 44100 1
arg: 0x000a000e
out缓冲区: 16384
音频设置: 44100.000000 采样率, 1 通道
音频设置完成。
================<rt-queuing>=
START: 0.000000 8.000000 0.300000 0.200000 1000.000000 1.000000
================<rt-queuing>=
START: 0.200000 8.010000 0.300000 0.200000 1000.000000 1.000000
================<rt-queuing>=
START: 0.400000 8.020000 0.300000 0.200000 1000.000000
================<rt-queuing>=
START: 0.600000 8.030000 0.300000 0.200000 1000.000000
================<rt-queuing>=
START: 0.800000 8.040000 0.300000 0.200000 1000.000000
================<rt-queuing>=
START: 1.000000 8.050000 0.300000 0.200000 1000.000000
================<rt-queuing>=
START: 1.200000 8.060000 0.300000 0.200000 1000.000000
================<rt-queuing>=
START: 1.400000 8.070000 0.300000 0.200000 1000.000000
================<rt-queuing>=
START: 1.600000 8.080000 0.300000 0.200000 1000.000000
================<rt-queuing>=
START: 1.800000 8.090000 0.300000 0.200000 1000.000000
================<rt-queuing>=
START: 2.000000 8.100000 0.300000 0.200000 1000.000000
================<rt-queuing>=
START: 2.200000 8.110000 0.300000 0.200000 1000.000000 1.000000
================<rt-queuing>=
START: 2.400000 8.120000 0.300000 0.200000 1000.000000 1.000000
```

... 此时你应该能听到用类似吉他的音色弹出的中速音阶。

随附的 CD-ROM 中包含了一个带有界面的更为复杂的 Garton's Loothing（如图 9-42 所示）。该 Loothing 示例展示了 RTcmix 实时交互性能界面的可能性。

## RTcmix 中的实时效果处理

最后一个示例演示了应用于从 `csound` 麦克风输入读取的实时音频流的延迟效果处理器：

```c
/* rt_delay.sco */
load("DELAY") /* 加载 DELAY */
rtsetparams(44100, 1, 64) /* 设置实时参数：采样率、通道数、缓冲区大小 */
rtinput("AUDIO") /* 告诉调度器输入来源 */
makegen(1, 24, 1000, 0.0, 0.5, 3.5) /* 将幅度包络应用于输出 * */
DELAY(0, 0, 7) /* 将效果应用于输入信号 */
```

该分数使用以下命令运行：

```
CMIX < rt_delay.sco
```

即使在 P16 上实时响应良好。更快的机器可以处理复杂的任务。

## RTcmix 的未来

虽然 Cmix 用户群相比之下较小，但这是一个致力于改进语言功能的活跃群体。Dave Topper 慷慨地投入时间和精力维护 Linux 版本的 RTcmix，并希望不断改进它。随着图形界面的出现，我预计 Cmix 的人气将会增加。

## 其他语言

凭借其 UNIX 血缘，Linux 继承了丰富的学术音乐和软件传统。Csound 和 Cmix 只是 Linux 上许多音频合成语言中的两种；其他的包括 Common LISP Music、SAOL、Nyquist 和 Music4C。这些许多语言扩展了 MusicN 系列计算机音乐技术，但也出现了新的方法，例如直接用于 C++ 语言的音频处理类。

## Sig++

- 作者：Craig Stuart Sapp
- 版本：1.0.0
- 网站：http://hummer.stanford.edu/sig/
- FTP 站点：n/a
- 维护：是
- 可用性：免费，开源
- 版权：归作者所有
- 摘要：声音合成与预定义函数

以下是一个白噪声生成器示例：

```cpp
// 白噪声生成器
// 程序员：Craig Stuart Sapp
// 日期：1997年4月30日 周三 14:17:37 GMT
// 修改：1998年1月19日 周一 04:21:05 GMT

#include "WhiteNoise.h"
#include <iostream>
#include <stdlib.h>
#include <limits.h>
#include <time.h>

void setAmplitude(float aAmplitude) {
    // 实现细节
}

void action() {
    // 实现细节
}

float getAmplitude();

void output(int channel) {
    // 实现细节
}

void printState() {
    std::cout << "State information" << std::endl;
}

void seed(int aSeed) {
    // 实现细节
}
```

```
//
// 以下样本均来自 analogue2@aol.com 收集的
// Moog Rogue 采样集。
//
```

```
global {
rate 44100;
krate 100;
outchannels 1;
table noise(sample,-1,"noise.wav");
table bass(sample,-1,"bass.wav");
}
```

```
// 以三种尺寸播放的噪声
```

```
template <noise, twicoise, halfnoise> ()
map <factor, size> with {<1, 381952>, <2, 2*381952+1>, <0.5, 190976> {
imimports exports table noise;
table newnoise(empty,size);
speed(noise,newnoise,factor);
output(0.4*oscil(newnoise));
}
```

```
// 以三种尺寸播放的低音
```

```
template <bass, twicebass, halfbass> ()
map <factor, size> with {<1, 110848>, <2, 2*110848+1>, <0.5, 55424> {
imports exports table bass;
table newbass(empty,size);
speed(bass,newbass,factor);
output(0.4*oscil(newbass));
}
```

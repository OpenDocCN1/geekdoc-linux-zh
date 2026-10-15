

# 使用 nice 控制作业优先级

假设你需要从互联网上下载一个巨大的文件，这可能需要一整个下午的时间。下载它会占用大量系统资源，并使系统对其他用户的响应时间变得慢得多。好吧，例子不太好。假设你的同事需要下载一个巨大的文件，并且会占用一整个下午的系统资源。你希望她能有礼貌，不要占用你需要使用的系统资源。

幸运的是，她可以使用 nice 来做到这一点，nice 允许她控制作业优先级。如代码清单 9.9 所示，你使用 1 到 19 之间的数字来设定作业的优先级，其中 1 表示有点友好（优先级较高），19 表示非常友好（优先级较低）。Unix 系统使用你提供的数字来确定要投入多少注意力处理该作业。

## 要使用 nice 控制作业顺序：

- nice 19 slow script
  在 shell 提示符下，输入 nice，后跟适当的调整值（此处为 19），以及要运行的程序或脚本名称（代码清单 9.9）。在此示例中，slow script 以可能的最低优先级运行。

## 提示

- 要了解你需要有多友好，可以查看当前在 Unix 系统上运行了多少进程（以及是哪种类型）。你可以使用 ps 来做到这一点，如本章后面所述。
- 你可以使用 nice 并在后台运行作业——例如，使用 nice 12 funscript & 以 niceness 级别 12 在后台运行 funscript。

```
[ejr@hobbes ej]$ nice 19 slow script
```

代码清单 9.9 通过使用 nice 加上调整值，你可以让 Unix 决定对你的作业努力工作到什么程度。

- 你可以直接输入 nice 加上作业名称（如 nice sortaslow）。这样会自动指定 10 作为友好度级别（默认设置）。
- 如果你是系统管理员并以 root 身份登录，你可以使用负数（低至 -20）与 nice 一起使用来提高优先级（nice -16 priorityjob）。
- 使用 renice 来更改正在运行作业的友好度。例如，使用 renice 18 2958（作业编号）。如果你是系统管理员，你可以增加或减少任何作业的友好度；如果你是平民——哎呀，我们是说你在公司里的普通计算机用户——你只能降低自己作业的优先级，而不能提高它。

# 使用 time 计时作业

有时，你可能想知道作业完成需要多长时间。你可以使用 time 命令来做到这一点，该命令根据内置的 Unix 计时器对作业进行计时。如代码清单 9.10 所示，你所要做的就是输入 time，后跟你想要计时的命令。

## 要使用 time 计时作业：

- time slowscript

在 shell 提示符下，输入 time 后跟完整的命令。命令完成后，系统会告诉你它花费了多长时间，如代码清单 9.10 所示。

## 要使用 time 比较作业时间：

1. time ls /usr
   在 shell 提示符下，输入 time 后跟一个作业（此处为 ls）。

2. time nice -n 19 ls /usr
   然后，输入 time 后跟另一个作业。在此示例中，我们比较常规 ls 命令与 nice ls 命令。如代码清单 9.10 所示，nice ls 命令的经过时间明显长于常规 ls 命令。

continued on next page

```
[ejr@hobbes running]$ time slowscript
0.0s user 0.0system 0:50.12elapsed 0%CPU
[ejr@hobbes running]$ time ls
bigdog, tar.gz  slowscript  testing.gif
0.03user 0.00system 0:00.08elapsed 78%CPU
[ejr@hobbes running]$ time nice -19 ls
bigdog, tar.gz  slowscript  testing.gif
0.03user 0.03system 0:00.06elapsed 93%CPU
[ejr@hobbes running]$ time -p nice -n 19 ls
foo
real 0.00
user 0.00
sys 0.00
[ejr@hobbes running]$
```

代码清单 9.10 输入 time 加上完整的作业命令即可了解作业时间。

# 提示

- 请记住，作业运行所需的时间可能会根据系统的当前负载或容量而有所不同。例如，作业在凌晨 2 点运行可能比下午 2 点运行所需的时间更短，因为凌晨时使用 Unix 系统的人很少，而下午时使用的人更多。

- 不同系统产生的 time 输出略有不同。在某些系统上，你会得到 real（时钟）时间、用户时间和系统时间。Real 时间是指程序运行期间时钟经过的秒数，而用户时间和系统时间则分别指系统运行作业所需时间的不同度量。在其他系统上，你可能会得到一堆垃圾，如代码清单 9.11 所示，但信息的要点是相同的。

- 在 ls 示例的情况下，你实际上并不关心输出或错误——只关心时间——因此你可以创造性地将其全部丢弃。尝试 time ls /usr > /dev/null 2>&1 以将标准输出发送到 /dev/null（位桶）并将错误消息发送到标准输出（从而发送到位桶）。有关详细信息，请参阅第 17 章。

- 尝试 time -p 以获得更易于人类阅读的输出。

```
$ time slowscript
0.0User 0.0System 0:50.13elapsed 0%CPU
(0avgtext+0avgdata 0maxresident)k
0inputs+0outputs (219major+59minor)pagefaults
0swaps
$
```

代码清单 9.11 time 输出因系统而异。在这里，我们除了时间信息外，还得到了一堆需要解读的垃圾。



# 硬件兼容性检查

| 硬件 | 需要检查的要求 |
| :--- | :--- |
| 内存 | 随机访问内存 (`RAM`)、缓存、虚拟内存 |
| 视频 | 分辨率、颜色数 |
| 磁盘空间 | 空闲空间、兼容的分区等 |
| 指示设备 | 鼠标、触摸板、操纵杆、轨迹球、光笔 |
| 外围设备 | 打印机、滚筒、扫描仪 |
| 多媒体设备 | 声卡、视频采集卡、视频播放能力 |

除了硬件要求外，还需要检查软件兼容性。如果你的应用程序要求系统中有 `libc6.0`，你的安装程序必须验证已安装 `libc6.0`。如果你的应用程序需要 2.0 或更高版本的 Linux 内核，不要在内核低于 2.0 的系统安装应用程序。表 12-2 列出了在 Linux 环境安装应用程序之前应该检查的一些软件组件。

# 表 12-2 软件组件要求

| 软件 | 需要检查的要求 |
| :--- | :--- |
| `libc` 版本 | 许多 Linux 应用程序和程序所需的共享库 |
| 内核版本 | 特定硬件和软件功能的支持；芯片组、数据库、外围接口等 |
| `XFree86` 版本 | 视频驱动程序；对芯片组、笔记本和其他移动设备的软件支持 |
| `gnu` `cc` | 类库兼容性、`ANSI/ISO` 遵循、编译源码分发应用程序的能力 |
| `JRE` | `Java` 兼容性，可能影响浏览器功能和插件等 |

## 第 12 章 安装注意事项

共享库在 Linux 环境的软件兼容性中起着重要作用。检查 `libc`、`KDE`、`Qt` 和 `gnome` 版本是非常重要的。如果你的应用程序仅以源码形式分发，那么用户将不得不进行编译。这意味着用户的环境中必须有适当版本的编译器、头文件和库文件，以编译你的程序。在向用户系统上加载应用程序文件之前，必须检查这种类型的软件兼容性。可以使用自定义的 shell 脚本或 `autoconf` 来检查特定库文件和头文件是否存在。

### 使用 `sysinfo()` 确定某些系统能力

使用 `sysinfo()` 函数查找系统内存限制。`sysinfo()` 函数返回有关整体 `RAM`、交换空间（`swap`）和并发进程限制的信息。这些信息通过如下所示的 `sysinfo` 结构体返回：

```cpp
struct sysinfo {
    long uptime;      /* 自启动以来的秒数 */
    unsigned long loads[3]; /* 1、5 和 15 分钟平均负载 */
    unsigned long totalram;  /* 总可用主内存大小 */
    unsigned long freer;     /* 可用内存大小 */
    unsigned long sharedram; /* 共享内存数量 */
    unsigned long bufferram; /* buffer 使用的内存 */
    unsigned long totalswap; /* 总交换空间大小 */
    unsigned long freeswap;  /* 剩余可用交换空间 */
    unsigned short procs;    /* 当前进程数 */
    char *f[22];             /* 将结构体填充到 64 字节 */
}
```

例如，列表 12-1 中的程序显示了系统的总 `RAM` 以及可用内存检查。

> 列表 12-1：执行可用内存检查的程序

```cpp
// Listing 12-1
// 可用内存检查示例

#include <iostream.h>
#include <linux/kernel.h>
#include <linux/sys.h>

extern "C" int sysinfo(struct sysinfo *X);

int main(int argc, char *argv[]) {
    struct sysinfo SystemInfo;
    if (sysinfo(&SystemInfo) != -1) {
        cout << "Total Memory ";
        cout << SystemInfo.totalram << endl;
        cout << "Available Memory ";
        cout << SystemInfo.freeram << endl;
    } else {
        cerr << "sysinfo() call failed" << endl;
    }
    return (0);
}
```

`sysinfo` 结构体还提供了缓冲区信息、交换空间大小信息以及用户允许执行的并发进程数。如果你的应用程序需要多任务处理并被分为多个进程，则 `sysinfo` `procs` 参数可能会很有用。

### 使用 `sysconf()` 确定运行时系统限制

`sysconf()` 函数返回多个系统限制的值。例如，你可以使用 `sysconf()` 函数返回每秒的时钟滴答数，或者进程可以打开的最大流数。你也可以用它来返回进程可能打开的最大文件数，或每个用户 ID（user ID）允许的最大并发进程数。如果你的应用程序打开许多文件、需要特定的 `CPU` 吞吐量或生成了许多进程，那么可以在安装过程中使用 `sysconf()` 函数来检测用户的环境是否能够支持你的程序。`sysconf()` 函数根据传递的参数返回系统限制值。表 12-3 列出了 `sysconf()` 参数及其含义。

通过带有表 12-3 中的任一个参数来调用 `sysconf()` 函数。例如：

```cpp
#include <unistd.h>
cout << sysconf(_SC_CHILD_MAX);
```

这将显示单个用户 ID 允许拥有的最大并发进程数。你可以使用 `sysinfo()` 和 `sysconf()` 函数来获取安装程序所需的大部分信息。

#### 表 12-3

`sysconf()` 的参数

| 参数 | 说明 |
| :--- | :--- |
| `_SC_STREAM_MAX` | 进程在任意时间打开的最大流数 |
| `_SC_OPEN_MAX` | 进程在任意时间打开的最大文件数。 |
| `_SC_ARG_MAX` | `exec()` 族函数参数的最大长度。 |
| `_SC_TZNAME_MAX` | 时区名称中的最大字节数。 |
| `_SC_CHILD_MAX` | 每个用户 ID 的并发进程数。 |
| `_SC_CLK_TCK` | 每秒的时钟滴答数。 |
| `_SC_JOB_CONTROL` | 告知是否支持 `POSIX` 风格的任务控制。 |
| `_SC_SAVED_IDS` | 告知进程是否具有保存的用户-ID 和保存的组-ID。 |
| `_SC_VERSION` | `POSIX.1` 标准通过的年份和月份；格式为 `YYYYML` |

### 使用 `statfs()` 确定磁盘空间

`statfs()` 函数是安装程序可以另一个有用函数，用于查找用户系统是否满足你的应用程序的要求。`statfs()` 函数返回有关挂载文件系统的大量有用信息。请记住 Linux 环境支持多种文件系统，例如（`ext2`, `vfat`, `mdos`, `minix` 等）。你可以使用 `statfs()` 函数获取信息，如文件大小的最大长度、文件系统中的总块数、文件系统中的空块数、最佳的数据块传输大小以及安装的文件系统类型。`statfs()` 函数以以下 `statfs` 结构体返回其信息：

```cpp
struct statfs {
    int type;
    long bsize;
    long blocks;
    long free;
    long bavail;
    long files;
    long ffree;
    dev_t fsid;
    long namelen;
    int spare[6];
};
```

`statfs()` 函数通过文件系统路径和 `statfs` 结构体调用。`statfs` 结构体会被填充信息。表 12-4 列出了 `statfs` 结构体中信息的类型及其含义。

#### 表 12-4

`statfs` 结构体中的信息

| `stats` 结构体字段 | 说明 |
| :--- | :--- |
| `long type` | 文件系统类型 |
| `long bsize` | 最佳传输大小 |
| `long blocks` | 文件系统中的总块 |
| `long free` | 文件系统中的空块 |
| `long bavail` | 可供非用户的块 |
| `long files` | 文件系统中的总节点 |
| `long ffree` | `fs` 中的空节点 |
| `dev_t fsid` | 文件系统 ID |
| `long namelen` | 名字的最大长度 |
| `int spare` | 预留 |

`statfs()` 函数成功时返回 0，否则返回 -1。列表 12-2 中的程序使用 `statfs()` 函数返回系统的总块和系统的空块数。

#### 列表 12-2：使用 `statfs()` 函数的程序

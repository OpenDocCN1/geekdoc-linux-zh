
# Python 嵌入教程

你现在可以开始嵌入 Python 了。需要的第一个函数是 `Py_Initialize()`。你需要的其他函数是 `PySetMainThread()`、`PyEvalSaveThread()`、`PyEval_InitThread()` 和 `PyEval_ReleaseLock()`。一旦完成初始化，你就可以开始与解释器交互并加载模块：`__main__` 和 `sys`。但其他模块呢？你可以设置搜索路径，查找模块并使用 `Py_SetPathHome` 函数加载它。如果你需要相关信息，可以通过 `Py_GetPathHome()` 函数找到当前路径。

然而，它并不包含 `sys.argv`，你需要使用函数 `PySys_SimpleString`：

```c
Py_SimpleString(char *argv, int flags)
s = Py_SimpleString("The line is: Hello World");
```

这是 `Py_SimpleStringFlags(char *command, PyCompilerFlags *command)` 的简单版本，它还接受一个用于编译器的标志结构体。如果你需要检查标志，可以在编译器中查看详细信息。

假设你有一段 C 代码，其功能等同于 Python 脚本。文件使用 `Py_SimpleFlags *File, const char filename` 初始化。如果你想从脚本中获取从 C 获取的函数，如果它是对脚本的引用，你可以通过读取文件获取函数。

```c
int PyRun_SimpleFileFlags(char *filename, int flags)
```

你还需要用该文件打开 Python 解释器。该函数将带有正确的标志来打开此脚本。Python 从此处返回函数的返回值：

```c
PyObject *Object = PyString_FromFromString("Hello World");
```

然后你就可以配合函数使用 Python 对象。例如，如果你在字符串名称中开始一个 Python 模块名，可以通过函数调用导入它。你也可以从 C 代码中获取对象。你可以在此处引用问题中模块的字典：

```python
my_module = PyImport_GetDict(name="__main__")
```

一旦获取了字典，你就可以通过以下方式获取特定对象的引用：

```python
my_func = PyDict_GetItemString(dict, name="my_func")
dict = PyDict_GetItem(dict, name="my_func")
```

## 完整代码列表

```c
// 简单的运行 Python 代码的方法
#include <Python.h>

int main(int argc, char *argv[]) {
    Py_SetProgramName(argv);

    // 初始化 Python 解释器
    Py_Initialize();

    // 运行 Python 代码
    Py_RunSimple("from time import time, time\nprint('Today is', time())\n");

    Py_Finalize();

    return 0;
}

// 你创建一个交互式 Python 控制台
#include <Python.h>

int main(int argc, char *argv[]) {
    Py_SetProgramName(argv);

    // 初始化 Python 解释器
    Py_Initialize();

    // 运行 Python 代码
    Py_RunSimple("from time import time, time\nprint('Today is', time())\n");

    Py_Finalize();

    return 0;
}

// 你创建一个交互式控制台
#include <Python.h>

int main(int argc, char *argv[]) {
    FILE *fp;

    fp = fopen("script.py", "r");

    Py_RunSimpleFileFlags(fp, 0);

    Py_Finalize();

    fclose(fp);
}
```

# 教程：使用树莓派控制灯光

## 使用你的 Pi 控制灯光

冬夜变得越来越长了；使用树莓派和移动设备远程控制你的灯光。

Energetie 的朋友们创建了一些天才的插座，可以通过你的树莓派进行开启和关闭。你可以购买一个入门套件，其中包含 RF 发射器扩展板和两个插座来开始尝试。该扩展板使用简单的 Python GPIO 库进行控制。一旦完成安装和设置，你就可以使用树莓派配合 `Pi-mote`，通过简单的程序控制多达四个 Energetie 插座。本教程将介绍如何设置插座以及如何调整程序以使其在你的设备上运行。

`Dan Aldred` 是一位树莓派认证教育者和首席学校教师。他最近成为了 Astro Pi 中学组比赛的获得者。

- `sudo apt-get update`
- `sudo apt-get upgrade`

取决于你正在使用的操作系统版本，你可能需要安装 Python GPIO 库。（Raspbian Jessie 预装了这些库，所以你可以跳过此步）。输入：

- `sudo apt-get install-rpi.gpio`

完成后，重启你的 Pi。这将安装 Python GPIO 库，这意味着你可以用 Python 代码访问并控制引脚。

### 01 设置

要开始之前，启动你的树莓派并加载 LX Terminal，然后通过输入更新你的软件：

![](img/df5857e82a6482b0f2db5a2e61e6012c_71_0.png)

#### 你需要什么

- 带有 RC 插座的 Pi-mote IR 控制板
- 台灯
- 附件

上方 使用智能手机控制你的家庭环境

## 安装 Energetie 库

### 02

接下来，启用 Energetie 库。这些库让 `Pi-mote` 板和树莓派与 Python 交互。在 LX Terminal 中，根据你使用的 Pi 版本，执行以下操作：

`sudo apt-get install python3-pip`
`sudo pip3 install energie`

...针对 Python 3，或者：

`sudo apt-get install python3-pip`
`sudo pip install energie`

...针对旧版本。未来，Energetie 将更新软件，你可能需要运行更新检查以确保你拥有最新版本。要更新类型，代码：

`sudo apt-get install --update`

左侧 `Pi-mote` 发射器非常易用，它由 Pi 供电并使用仅限发射器的开环系统。

![](img/df5857e82a6482b0f2db5a2e61e6012c_72_0.png)

### 03 安装 Pi-mote

在安装 `Pi-mote` 之前，请断开插座的电源。拔掉电源并将模块插入你的树莓派。电路板上的“L”部分标记为 L。将其插入与你处于同一房间或区域的某个 Energetie 插座中。范围相当非常好，但墙壁可能会阻塞传输信号。你可以通过插上一盏灯，然后按下连接到插座的绿色按钮进行测试。触发器将关闭插座，然后灯会亮起熄灭。

## 07 开启插座的代码

Energetie 库让创建一个用于开启插座的代码变得极其简单，这将开启你的灯。在不知不觉中，你将使用树莓派来开启或关闭电水壶或电视。
启动一个新程序，导入 `energie` 库（第 2 和 3 行），然后添加切换插座的代码（第 4 行）。保存并运行你的程序。插座会发出点击声作为应答，然后你的灯就会亮起。

```python
import RPi.GPIO as GPIO
import time
from energie import switch_on
switch_on()
```

## IP 地址

每个联网设备都有互联网协议地址（IP 地址）。此标签用于识别每个设备，可能包含你家庭网络中的 IP 地址，如 `192.168.1.1`。

### 04 关闭插座

在树莓派 之前，你可以连接插座并关闭它，使用编程学习来自插座的代码。每个插座都有独特的代码可以控制。Energetie 设置代码可以在你的教程资源中找到。

### 05 设置你的插座

一旦完成了设置程序，运行它。它应该是插座正方的 LED 指示。LED 将闪烁几秒钟并引导信号。开启状态下，程序将返回。

```python
import RPi.GPIO as GPIO
import time
import energie
from energie import switch_on
```

```python
switch_on()
time.sleep(5)
switch_off()
```

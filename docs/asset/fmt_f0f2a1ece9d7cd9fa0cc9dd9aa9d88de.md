
# term 和 X

`term` 工具可以从 X 终端使用。X（或带有大多数 Linux 版本的 XFree86）允许你专门打开一个窗口来运行 `term`。大部分的 X 连接处理是由一个名为 `txconn` 的工具完成的。`txconn` 进程必须在远程机器上执行（通过网络连接，因为 X 在调制调器上无法以合理的速度工作），并作为守护进程放在后台。当 `txconn` 进入后台时，它会返回一个带有显示器数字的消息，用于标识该进程：

```
Xconn bound to screen 11
```

当你从 X 窗口连接到远程 `txconn` 守护进程时，你使用这个数字来识别屏幕。这被分配给 `DISPLAY` 环境变量。如果绑定到屏幕 11，如上一条消息所示，你会这样设置变量（对于 C shell）：

```bash
setenv DISPLAY remotename:11
```

其中 `remotename` 是远程机器的名称。对于 Bourne 或 Korn shell，我们通过这些命令实现相同的环境变量设置：

```bash
DISPLAY=remotename:11
export DISPLAY
```

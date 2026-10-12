
所有这些命令都需要以 `root` 身份运行，因此必要时使用 `sudo`。某些程序可以与 `Airmon` 的操作集成，但我们继续使用

### `airmon-ng wlp250`

将显示进程列表及其 `PID`。你可能不需要杀死所有进程，但终止 `NetworkManager` 绝对是一个好主意。使用 `kill <PID>` 执行，其中 `PID` 显示在表中。此外，如果你看到一个表格，例如：

> 带有 `<PID>` (`dhClient`) 的进程正在接口 `wlp250` 上运行

杀死任何客户端实例也是明智的，我们可以通过以下命令监控无线流量：

- `airmon-ng wlp250`

这将显示所有附近的 `AP` 以及任何连接到它们的设备。按 `Ctrl+C` 停止你所有的黑客工具，不要攻击你没有权限的对象。现在攻击上一个命令中的目标（其 `MAC` 地址）、`SSID`（网络名称）和 `BSSID`：

- `airmon-ng -a <BSSID> --essid <SSID> -c <Channel> wlp250`

注意这创建了一个新接口：

- `Created interface at0`

对于我们的下一步，我们将对所有连接到我们网络的用户进行去身份认证。当他们尝试重新连接时，我们将撤销其与我们网络的连接。在实际中运行此命令：

- `aireplay-ng -a 0 <BSSID>`

## 让我们的桥接有用

我们使用 `HTTP` 版本的网页，以便收获密码。`SSID` 攻击流量被重定向。

(此处由于后续文本完全重复，已按指令要求停止输出)

```python
pg_explore(find=(0x0884453, avoid=0x0884461))
```

以下是你可以使用 `Angr` 探索整个程序的方法，以寻找以 `0x0884453` 结尾的数值路径，同时避开地址 `0x0884461`。第一个地址是打印 `"Password OK"` 的地方；第二个地址是输出 `"Invalid password"` 消息的地方。

对二进制文件进行符号执行后，你可以要求 `Angr` 求解查询。我如何获取路径 `0x0884087`？如果你在 `0x0884453` 找到了路径，你可以要求 `Angr` 重构你需要的值；字符串或描述符内部有一个值（第 4-6 行）。

```python
int len(pg.path());
```

## 跨二进制文件分析

`Angr` 允许你分析多种架构的二进制文件，而不仅仅是 `x86/x64`。请为 `ARM` 安装交叉工具链（在开发机上）或查看文档。你可以编译修改过的 `fauxware.arm-linux-gnueabihf -o=fauxware.arm --entry=/factory`。使用 `Angr` 查找目标路径和需要避开的路径；此程序有两个函数 `connected()` 和 `rejected()`，所以你可以使用 `radon` 中的命令来定位这些偏移量：

```
0x0001058 af-connected, rejected
```

| address | size | status |
|---|---|---|
| `0x0001058` | `1` | `sym_connected` |
| `0x000106c` | `24` | `sym_rejected` |

因此，你告诉 `Angr` 定位 `0x0001058` 或 `0x000106c`（在二进制文件中），这些偏移量在你的系统上有所不同。

## 尝试符号值和具体值

你可能已经使用过符号值。符号执行速度很快，但你需要对其进行调试。在二进制分析的实验中，二进制文件通常比像 `LLVM` 示例那样简单的破解程序复杂得多。要对 `fauxware.arm` 进行符号分析，你可以使用 `pc2_solver.fauxware.arm` 为任何元素创建一个符号值，并查看第 32-33 行。

```python
sym_arg_username=claripy.BV('sym_arg_username', 8)
symym_arg_password=claripy.BV('sym_arg_password', 8)
```

在这里你使用 `Clarity` 创建了两个符号输入缓冲区，分别为 `sym_arg_username` 和 `sym_arg_password`，长度均为 9 字节。执行符号分析后，这两个缓冲区将包含满足以下条件的值：

```
1. int a = a, b = b, c = y;
2. // symbolic
3. int x = 0, y = 0, z = 0;
4. if (a) {
5. x = 2;
6. if (a & (c < 5)) {
7. y = 1;
8. else {
9. z = 2;
10. }
11. assert(x+y+z=3);
```

![](img/80af6fd0c5ad221222cba94201825f7f_38_0.png)

符号执行通过对 `0x010568` 搜索路径问题中的值应用路径和约束来工作。最后，你可以指示 `Angr` 将二进制文件的起点设置为其入口点，沿路径传递构造好的参数数组（第 41 行）。

```python
state = factory.entry_state(path='path')

if len(state.args) > 0:
    print(state.args[0]('sym_arg_username'))
    print(state.args[1]('sym_arg_password'))
```

一旦符号执行结束，并且你成功到达了 `0x010568`，你就可以通过 `tell()` 获取符号输入缓冲区的具体值（第 50-57 行）。执行它你将看到打印的具体字符串被拒绝了 (2)；即 `sym_arg_password`：

## `Angr` 是一个用于下一代二进制分析的符号执行 (concolic) `Python` 框架，可用：`filesilo.com`

![](img/80af6fd0c5ad221222cba94201825f7f_38_1.png)

调用图允许你静态分析二进制文件。你可以使用 `Angr` 获取其函数和约束信息。你可以使用 `hooks()` 探索它：

```
pc2_solver.fauxware.arm
Arg[1](Username):
Arg[2](Password):
```

这意味着无论向程序传递什么用户名，密码始终是常数；快速后门！

## `Angr` 教程

在 2015 年，`PhD` 学生和 `Angr` 的创建者开始使用 `Python` 寻找漏洞。符号执行不是魔术；更好的方法是通过对符号值设置约束来引导它。你可以使用程序 `state` 和 `add_constraints` 方法固定八个字符的长度，第九个是（以空字符结尾的）：

## 修改流

```python
for i in range(8):
    state.add_constraints(sym_arg_username)
    state.add_constraints(sym_arg_username.get(i) != 0)
```

在二进制仿真过程中，你可以获取任意点的二进制文件的详细描述。该描述包括寄存器、内存和栈。所以你想到达程序中的某个路径，但不想在求解它上浪费时间，因为它太复杂或无法用原语求解。例如，`Angr` 之后可能存在漏洞，你可以在任意一点开始执行。`authenticate()` 的返回值存储在 `state` 中。该值随后位于 `fp = local_8`。其内容存储在 `r3` 中。程序检查 `authenticate()` 的返回值。如果为真，则用户已通过验证。使用 `Angr`，你可以在 `0x06b08` 执行之前更改 `r3` 的值，使用以下脚本 `poc3_execution_flow.py`：

```python
### poc3_execution_flow.py
At 0x06b08, value for r3
Value: 0x00
Value: 0x01
Branches to: 0x15e8
Branches to: 0x15ec
```

拒绝路径可能会暴露技巧！这里是如何使用 `Angr` 逐步执行二进制文件（第 77, 99 行）：

```python
while len(state.step()) > 0:
```

一旦指令指针位于 `0x66b8`（从 `authenticate()` 返回后），你就可以控制 `r3` 的值使其为 `1`（第 77-79 行）。

```python
if state.active_state.frame.addr == 0x66b8:
    state.active_state.regs.r3 = 1
```

之后，路径在偏移量 `0x6b00` 持续，这将执行，避开了拒绝路径。

### 插桩二进制文件

```
0x0066b4 authenticate
0xa2ffff bl sym
```

跳转到 `0x066b4` 处的指令并使用以下代码反汇编：

```
0x0006b44+4
0x0006b48 3
0x0006b48 0000be5 str r0[fp - local_8]
0x0006b4c 0831be5 ldr r3[fp - local_8]
```

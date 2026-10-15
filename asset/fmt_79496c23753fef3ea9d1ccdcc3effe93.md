
### `/usr/lib/lpsched`

在上述过程中，如果路径被设置为包含 `/usr/lib` 目录，则不需要指定完整路径。上述过程

| 表 5.4 lpadmin 命令的选项 |
| lpadmin 选项 | 描述 |
| :--- | :--- |
| `-c` | 设置打印机类（例如：laser、line 等） |
| `-d` | 通过打印机名称或类名指定系统默认目标。 |
| `-h` | 识别直接连接到计算机的打印机。 |
| `-l` | 识别通过登录终端访问的打印机。 |
| `-i` | 指定接口程序的绝对路径。 |
| `-m` | 提供打印机接口程序的名称。 |
| `-e` | 为指定的打印机复制现有打印机接口程序的名称。 |
| `-p` | 指定打印机名称 |
| `-r` | 移除打印机类 |
| `-v` | 提供打印机设备的路径 |
| `-x` | 按名称移除特定打印机。 |

### 硬件维护 — 87

使用 `lpshut` 停止调度器，然后定义了一个名为 `laser2` 的新打印机，使用 `-m` 指定了名为 `dumb` 的接口，这允许其作为标准打印机运行。`-v` 选项告知关联设备文件，在此例中为 `/dev/tty10`。注意此设备文件也在 `iptab` 文件中，通过 `getdefs` 配置通信的协议。在 `iptab` 中，该标识应关闭以防止连续打印信息。你也可以通过执行 `lpadmin -dlaser2` 将 `laser2` 设置为默认，在建立打印之后。

在使用打印机之前，必须告诉 `lpsched` 开始向打印机添加请求，`enable` 开始指定的打印机，`accept` 仅在添加打印机时需要使用，除非由于某些原因被拒绝或禁用。

你可能希望使用打印机的特殊功能，指定合适的接口文件。接口文件允许你的系统与打印机正确交互，否则可能会得到奇怪的打印结果。接口文件通常位于 `/usr/spool/lp/model`。

要将打印机分配到打印机类（例如 `laser`），输入 `lpadmin placer2 -claser`。设置类通常是为了便于管理员管理打印机。建立类有助于标准化类类型的打印机名称，使用户更好地理解可用打印机是如何命名的。

要从网络移除打印机，使用 `lpshut` 停止调度器，使用 `/usr/lib/lpadmin -xlaser2` 移除打印机，然后使用 `ipsched` 重启调度器。

网络共享打印机非常常见，特别是组织希望网络用户可以使用它们时。带有 `-R` 选项的 `lpadmin` 设置远程机器打印服务。购买网络打印机时，请确保制造商有适用于你的 UNIX 类型的驱动程序，以便设置并添加到网络。

## 获取打印机状态

在运行 `lpadmin` 之前，必须停止 `lpsched`。在完成 `lpadmin` 任务后，必须重启调度器，之后验证它正在运行、打印服务可用以及打印机已安装。使用 `lpstat` 命令执行此操作。表 5.5 列出的各种选项允许你查看打印系统的全部或部分状态。

使用 `-t` 选项显示打印系统完整状态的示例

```
### lpstat -t
```

`scheduler is running`

`system default destination: laser1`

`members of class jet:`

`jet1`

`members of class laser:`

`laser1`

`laser2`

`device for jet1: /dev/jet1`

`device for laser1: /dev/laser1`

`device for laser2: /dev/laser2`

`jet1 accepting requests since Aug 5 9:00`

`jet accepting requests since Jul 1 6:00`

`laser1 accepting requests since Aug 5 9:05`

`laser accepting requests since Jul 1 6:02`

`laser2 accepting requests since Aug 7 13:43`

`printer jet1 is idle. enabled since Aug 5 9:00`

`printer laser1 is idle. enabled since Aug 5 14:12`

`printer laser2 is idle. enabled since Aug 7 13:44`

### 表 5.5 lpstat 命令的选项。

| lpstat 选项 |  |
| :--- | :--- |
| `-a` | 显示打印机的接受状态。 |
| `-c` | 显示打印机类以及类内打印机的目的地。可以使用 `-c[classname]` 请求特定的类。 |
| `-o` | 显示输出请求的状态。 |
| `-p` | 提供打印机状态。 |
| `-r` | 返回调度器状态。 |
| `-s` | 返回状态摘要。 |
| `-t` | 返回打印系统的完整状态。 |
| `-u` | 返回请求 ID 的统计信息。可以通过 `-u[request-id[n]]` 查询特定的请求 ID。 |
| `-v` | 返回打印机列表和设备名称。 |

## 硬件维护 — 89

如表 5.5 所示，你还可以使用 `-a`、`-p` 和 `-v` 选项请求特定打印机的信息。例如：

```
### lpsat -plaser2
```

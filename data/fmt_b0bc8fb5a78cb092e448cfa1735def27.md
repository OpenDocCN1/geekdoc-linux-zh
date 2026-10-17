
说明备份服务器正在运行。在开始配置 `Arkeia` 之前，确保你的 `X-Windows` 正在运行。然后在命令行中输入：

```
Arkeia
```

你将看到一个如图 232 所示的对话框。

![](img/4e6a76e57a4105be55d8a1cc0750b023_238_0.png)

图 232. `Arkeia` 初始窗口

`服务器名称` 字段默认填充了你当前工作的系统名称。如果你在另一个系统上安装了服务器组件，则必须更改此字段。

`登录名称` 字段默认填充为 `root`。如果你更改了 `Arkeia` 管理员的名称，请对其进行更改。

`密码` 字段默认为空。当你更改密码时，必须输入密码。`Arkeia` 的主对话框窗口出现（图 233）：

![](img/4e6a76e57a4105be55d8a1cc0750b023_239_0.png)

图 233. `Arkeia` 主对话框窗口

如果你想要窗口布局更简单，请前往菜单栏中的 `Utilities -> Setting`（工具 -> 设置）并修改窗口的外观。点击 `OK` 按钮保存新设置，然后再次点击 `OK` 按钮。现在，你将获得一个与图 234 窗口类似的窗口。

![](img/4e6a76e57a4105be55d8a1cc0750b023_240_0.png)

图 234. 新的 `Arkeia` 主对话框窗口

在窗口底部，你可以点击如图 235 所示的按钮：

![](img/4e6a76e57a4105be55d8a1cc0750b023_240_1.png)

图 235. 主窗口底部部分

这些按钮的含义从左到右分别是：

- 刷新作业 (`Refresh job`)
- 交互式备份 (`Interactive backup`)
- 周期性备份 (`Periodic backup`)
- 恢复 (`Restoration`)
- 保存包 (`Savepacks`)
- 磁带管理 (`Tapes management`)
- 池管理 (`Pools management`)
- 驱动器管理 (`Drives management`)
- 驱动器包 (`Drivepacks`)
- 库管理 (`Libraries management`)
- 备份完成 (`Backup done`)

- `OK` 按钮。点击此按钮打开一个新的欢迎对话框。
- `Cancel` 按钮。点击此按钮退出 `Arkeia`。
- 帮助 (`Help`)

在开始第一次备份之前，你必须执行以下配置步骤：

- 池管理 (`Pool management`)
- 磁带管理 (`Tape management`)
- 驱动器管理 (`Drives management`)
- 驱动器包管理 (`Drivepacks management`)
- 保存包管理 (`Savepacks management`)

让我们从磁带池管理开始。点击主对话框底部的 `pools management` 按钮，或点击菜单上的 `Tapes -> Pools management`。出现的 `Pools` 管理窗口如图 236 所示：

![](img/4e6a76e57a4105be55d8a1cc0750b023_241_0.png)

图 236. `Pools` 管理主对话框窗口

默认存在一个空闲池 (`scratch pool`)。要创建一个新的磁带池（例如用于你的备份磁带），点击 `new`（新建）按钮。出现的池创建对话框如图 237 所示：

![](img/4e6a76e57a4105be55d8a1cc0750b023_242_0.png)

在对话框字段中填写相应信息并点击 `OK` 按钮。出现 `Pools` 管理主窗口，池列表更新为如图 238 所示：

![](img/4e6a76e57a4105be55d8a1cc0750b023_242_1.png)

图 238. 更新了池列表的 `Pools` 管理主窗口

返回主对话框请点击 `OK` 按钮。现在我们可以用磁带填充 `Full Backup` 池。要执行此操作，点击 `tape management` 按钮，或点击菜单中的 `Tapes -> tapes management`。出现 `Tapes` 管理窗口（图 239）：

![](img/4e6a76e57a4105be55d8a1cc0750b023_243_0.png)

图 239. `Tapes` 管理主窗口

点击 `new` 按钮输入新磁带（图 240）：

![](img/4e6a76e57a4105be55d8a1cc0750b023_244_0.png)

磁带名称由一个固定部分和一个变量部分组成。固定部分可以是任何文本，而变量部分是一个数字。输入磁带名称的第一部分、要使用的磁带的第一个和最后一个数字，以及磁带类型（`DAT`、`DLT` 等）。选择磁带应所属的池，并在注释行输入注释。点击 `OK` 按钮返回 `Tapes` 管理窗口。`Tapes` 管理主窗口显示磁带列表已更新。

在创建磁带池后，我们可以创建驱动器。点击以下按钮：

![](img/4e6a76e57a4105be55d8a1cc0750b023_240_0.png)

点击 `new` 按钮输入新驱动器（图 241）：

![](img/4e6a76e57a4105be55d8a1cc0750b023_241_0.png)

在字段中填写相应信息。出现的 `Drives` 窗口（图 241）。

在创建驱动器后，我们可以创建驱动器包。点击 `new` 按钮进入驱动器包（图 242）。出现的对话框（图 242）：

![](img/4e6a76e57a4105be55d8a1cc0750b023_242_0.png)

在对话框中填写相应信息并点击 `OK` 按钮。出现的 `Drivepacks` 管理主窗口列表已更新，如图 242 所示：

![](img/4e6a76e57a4105be55d8a1cc0750b023_242_1.png)

返回主对话框请点击 `OK` 按钮。现在我们可以填充保存包。点击 `savepacks` 按钮，或点击菜单上的 `Tapes -> savepacks management`。出现的 `Savepacks` 管理窗口（图 243）：

![](img/4e6a76e57a4105be55d8a1cc0750b023_243_0.png)

点击 `new` 按钮创建新的保存包（图 244）：

![](img/4e6a76e57a4105be55d8a1cc0750b023_244_0.png)

在对话框中填写相应信息并点击 `OK` 按钮。出现的 `Savepacks` 管理主窗口列表已更新，如图 245 所示：

![](img/4e6a76e57a4105be55d8a1cc0750b023_245_0.png)

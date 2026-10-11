
`service nfs start`

4. 运行以下命令检查所有服务是否运行正常：

```
rpcinfo -p
```

5. 现在连接到 `192.168.0.101` 并挂载 `/home` 目录，请使用以下命令：

```bash
# mount 192.168.0.100/home /mnt/home
```

将 `/mnt/home` 挂载点替换为适合你的路径。

6. 在服务器上使用以下命令来列出所有当前导出的目录。

```bash
# showmount -a
```

至此，你已成功设置了 NFS。

# 实验-10：分配代理

## 目标

- 在客户端机器上分配代理。

## 要求

- 一台连接互联网的计算机
- Mozilla Firefox 浏览器

代理服务器调解两台或多台计算机之间的连接，以增加网络的安全性和隐私。你可以通过 Squid 代理服务器在客户端上分配代理。
让我们执行以下步骤，使用 Squid 代理服务器在客户端上分配代理：

1. 从 GNOME 桌面的顶部面板点击 Mozilla Firefox 图标，如图 1 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_203_0.png)

▲ 图 1：GNOME 桌面

出现 Firefox 窗口（图 2）。出现下拉列表（图 2）。

2. 从菜单栏选择“编辑（Edit）”。
3. 从下拉列表中选择“首选项（Preferences）”，如图 2 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_203_1.png)

▲ 图 2：编辑菜单

出现 Firefox 首选项窗口（图 3）。

4. 从 Firefox 窗口选择“高级（Advanced）”选项卡（图 3）。
出现高级选项卡（图 4）。

5. 点击连接（Connection）选项下方的“设置（Settings）”按钮，如图 4 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_204_0.png)

▲ 图 3：Firefox 首选项对话框

出现连接设置对话框（图 5）。

6. 选择“手动代理配置（Manual proxy configuration）”单选按钮（图 5）。

7. 在 HTTP 代理文本框内输入 IP 地址。在本例中，我们输入了 `192.168.1.36`（图 5）。

8. 在端口框内输入端口号。在本例中，我们输入了 `3128`（图 5）。

9. 勾选 HTTP 代理部分下的“所有协议使用此服务器（Use this server for all protocols）”（图 5）。

10. 点击“确定（OK）”按钮（图 5）。

再次出现 Firefox 首选项窗口（图 6）。

11. 点击“关闭（Close）”按钮关闭 Firefox 首选项，如图 6 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_204_1.png)

▲ 图 5：连接设置对话框

▲ 图 6：选择高级选项卡

12. 点击 Linux 桌面顶部的 Mozilla Firefox 图标，如图 7 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_205_0.png)

▲ 图 7：点击 Mozilla Firefox 图标

13. 在 Mozilla Firefox 窗口的地址栏中输入 `google.com` 地址（图 8）。
14. 按下回车（ENTER）键。出现 Google 首页，如图 9 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_205_1.png)

▲ 图 8：输入 google URL

▲ 图 9：Google 首页

代理设置已应用到客户端机器 `192.168.1.36` 上。
你需要确保防火墙设置配置恰当。如果某些网站被列在限制网站列表中，你将打开该网站。例如，如果 Gmail 网站地址（`http://www.gmail.com`）在防火墙设置中被列为限制网站，你将在 浏览器中看到错误信息，如图 10 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_205_2.png)

▲ 图 10：显示错误页面

# 实验-11：使用 C 语言编程

## 目标

- 使用 C 语言编写并运行程序。

## 要求

- 安装了 LINUX 操作系统的系统
- `gedit` 文本编辑器

### 列表 1：显示简单的 C 程序

```c
#include <stdio.h>

/* 在标准输出打印 welcome to ABC world */

int main() {
    printf("welcome to ABC world\n");
    return 0;
}
```

列表-1 包含以下代码语句：

- `include <stdio.h>`: 指代使用哈希 (`#`) 符号的预处理器语句，用于输入/输出函数。
- `/* ... */`: 代表注释，提供额外信息。
- `int main()`: 程序执行开始的地方的主函数。
- `printf()`: 用于打印欢迎消息的函数。
- `return 0;`: 终止函数的语句。
- `{}`: 用于封装函数体的大括号。

执行以下步骤编写程序：

1. 打开 `gedit` 文本编辑器（图 1）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_206_0.png)

▲ 图 1：gedit 编辑

2. 选择“文件（File）”菜单（图 2）。
3. 选择“另存为（Save As）”选项（图 3）。
4. 出现另存为对话框（图 4）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_207_0.png)

▲ 图 3：另存为对话框

5. 在名称（Name）框输入文件名（图 5）。
6. 选择你想保存的位置（图 5）。
7. 点击“保存（Save）”按钮（图 5）。

文件已保存在 `gedit` 窗口中（图 6）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_207_1.png)

▲ 图 5：选择位置

`gedit` 窗口显示代码（图 6）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_207_2.png)

▲ 图 6：gedit 窗口

保存程序后，让我们编译并执行它。在编译程序期间，编译器将源代码翻译成机器码。在编译和执行程序之前，你必须已编写并保存为 `.c` 扩展名。在 Linux 中，可以使用 GNU C (`gcc`)。

```bash
gcc Hello.c -o Hello
```

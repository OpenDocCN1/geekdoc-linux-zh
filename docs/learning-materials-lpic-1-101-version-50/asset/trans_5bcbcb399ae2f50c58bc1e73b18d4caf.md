
## 6. 输入 `ps` 命令以显示由 Apache HTTPD Web 服务器用户（`www-data`）启动的所有进程

- 使用 BSD 语法：
  ```
  $ ps U www-data
  ```
- 使用 UNIX 语法：
  ```
  $ ps -u www-data
  ```
- 使用 GNU 语法：
  ```
  $ ps --user www-data
  ```

## 探索性练习

1. **SIGHUP** 信号可以作为重启某些守护进程的一种方式。以*Apache HTTPD Web 服务器*为例——向父进程（由 *init* 启动的那个）发送 **SIGHUP** 会终止其子进程。然而，父进程会重新读取其配置文件、重新打开日志文件并生成一组新的子进程。请执行以下任务：

   - 启动 Web 服务器：
   - 确保你知道父进程的 PID：
   - 通过向父进程发送 **SIGHUP** 信号使 Apache HTTPD Web 服务器重启：
   - 检查父进程未被终止且新的子进程已生成：

2. 虽然 `ps` 的输出最初是静态的，但可以通过结合 *ps* 和 *watch* 将其*变为动态*。我们将监控 *Apache HTTPD Web 服务器* 的新连接。在执行下方描述的任务之前，建议你先阅读 [Apache MPM 通用指令](https://httpd.apache.org/docs/2.4/mod/mpm_common.html) 中 **MaxConnectionsPerChild** 指令的说明。

   - 在 *apache2* 的配置文件中添加值为 1 的 **MaxConnectionsPerChild** 指令——在 *Debian* 及其衍生系统中，该文件位于 */etc/apache2/apache2.conf*；在 *CentOS* 系列中，位于 */etc/httpd/conf/httpd.conf*。不要忘记重启 *apache2* 以使更改生效。
   - 输入一个使用 *watch*、*ps* 和 *grep* 来查看 *apache2* 连接的命令。
   - 现在打开一个 Web 浏览器或使用 *lynx* 等命令行浏览器，通过其 IP 地址与 Web 服务器建立连接。你在 *watch* 的输出中观察到了什么？

3. 正如你所学到的，默认情况下 *top* 按 CPU 使用率百分比降序排列任务（数值较高的排在前面）。这种行为可以通过交互式按键 M（内存使用量）、N（进程唯一标识符）、T（运行时间）和 P（CPU 时间百分比）进行修改。然而，你也可以通过在启动 top 时使用 -o 开关按照自己的喜好对任务列表进行排序（更多信息，请查看 top 的手册页）。现在，执行以下任务：

   - 启动 `top`，使任务按内存使用量排序：
   - 通过高亮显示内存列来验证你输入了正确的命令：

4. `ps` 还有一个 `o` 开关用于指定你想要显示的列。请调查此选项并执行以下任务：

   - 启动 `ps`，使其仅显示 `user（用户）`、`percentage of memory used（内存使用百分比）`、`percentage of CPU time used（CPU 时间使用百分比）` 和 `full command（完整命令）` 的信息：
   - 现在，启动 `ps`，使其仅显示用户及其正在使用的程序名称的信息：

## 总结

在本课中，你学习了*作业*和*作业控制*。需要牢记的重要事实和概念是：

- 作业是被发送到后台的进程。
- 除了*进程 ID*（*process ID*）之外，作业在创建时还会被分配一个*作业 ID*（*job ID*）。
- 要控制作业，需要作业规范（jobspec）。
- 作业可以被带到前台、发送到后台、挂起或终止（或*杀死*）。
- 作业可以与其所在的终端和会话分离。

同样，我们也讨论了*进程*和*进程监控*的概念。最相关的想法是：

- 进程是正在运行的程序。
- 进程可以被监控。
- 不同的工具让我们能够找出进程的*进程 ID*以及向它们发送信号以终止它们。
- 信号可以通过名称（例如 -SIGTERM）、数字（例如 -15）或选项（例如 -s SIGTERM）来指定。
- 在监控进程方面，top 和 ps 功能非常强大。前者的输出是动态的，会不断更新；而后者静态地显示输出。

本课使用的命令：

| 命令 | 描述 |
| :--- | :--- |
| `jobs` | 显示活动作业及其状态。 |
| `sleep` | 延迟特定时间。 |
| `fg` | 将作业带到前台。 |
| `bg` | 将作业移到后台。 |
| `kill` | 终止作业。 |
| `nohup` | 将作业与进程/会话分离。 |
| `exit` | 退出当前 shell。 |
| `tail` | 显示文件中最新的行。 |
| `watch` | 重复运行一个命令（默认周期为 2 秒）。 |
| `uptime` | 显示系统已运行的时间、当前用户数和系统平均负载。 |
| `free` | 显示内存使用情况。 |
| `pgrep` | 根据名称查找进程 ID。 |
| `pidof` | 根据名称查找进程 ID。 |
| `pkill` | 按名称向进程发送信号。 |
| `killall` | 按名称终止进程。 |
| `top` | 显示 Linux 进程。 |
| `ps` | 报告当前进程的快照。 |

## 引导练习答案

1. `oneko` 是一个有趣的程序，它显示一只猫追逐你的鼠标光标。如果桌面系统中尚未安装，请使用你的发行版的包管理器安装它。我们将使用它来研究作业控制。

   - 启动该程序。你该怎么做？
     通过在终端中输入 `oneko`。
   - 移动鼠标光标以查看猫如何追逐它。现在挂起该进程。你该怎么做？输出是什么？
     通过按下组合键 `Ctrl` + `Z`：
     ```
     [1]+  Stopped                 oneko
     ```
   - 检查你当前有多少个作业。你输入什么？输出是什么？
     ```
     $ jobs
     [1]+  Stopped                 oneko
     ```
   - 现在指定其作业 ID 将其发送到后台。输出是什么？如何判断该作业正在后台运行？
     ```
     $ bg %1
     [1]+  oneko &
     ```
     猫又开始移动了。
   - 最后，指定其作业 ID 来终止该作业。你输入什么？
     ```
     $ kill %1
     ```

2. 使用两个不同的命令发现由 *Apache HTTPD* Web 服务器（`apache2`）生成的所有进程的 PID：
   ```
   $ pgrep apache2
   ```
   或
   ```
   $ pidof apache2
   ```

3. 不使用它们的 PID，使用两个不同的命令终止所有 **apache2** 进程：
   ```
   $ pkill apache2
   ```
   或
   ```
   $ killall apache2
   ```

4. 假设你必须终止所有 **apache2** 实例，且没有时间找出它们的 PID。如何使用 `kill` 配合默认的 `SIGTERM` 信号以单行命令完成此操作：
   ```
   $ kill $(pgrep apache2)
   $ kill ‘pgrep apache2’
   ```
   或
   ```
   $ kill $(pidof apache2)
   $ kill ‘pidof apache2’
   ```

   > 由于 `SIGTERM (15)` 是默认信号，因此没有必要向 `kill` 传递任何选项。

5. 启动 `top` 并通过执行以下操作与其交互：

   - 显示**进程**的森林视图：
     按 `V`。
   - 显示进程的完整路径，区分用户空间和内核空间：
     按 `c`。

6. 输入 `ps` 命令以显示由 *Apache HTTPD Web 服务器* 用户（`www-data`）启动的所有进程：

   - 使用 BSD 语法：
     ```
     $ ps U www-data
     ```
   - 使用 UNIX 语法：
     ```
     $ ps -u www-data
     ```
   - 使用 GNU 语法：
     ```
     $ ps --user www-data
     ```

## 探索性练习答案

1. SIGHUP 信号可以作为重启某些守护进程的一种方式。以**Apache HTTPD Web 服务器**为例——向父进程（由 init 启动的那个）发送 SIGHUP 会终止其子进程。然而，父进程会重新读取其配置文件、重新打开日志文件并生成一组新的子进程。请执行以下任务：

   - 启动 Web 服务器：
     ```
     $ sudo systemctl start apache2
     ```
   - 确保你知道父进程的 PID：
     ```
     $ ps aux | grep apache2
     ```
     父进程是由 root 用户启动的那个。在我们的例子中，是 PID 为 1653 的那个。
   - 通过向父进程发送 SIGHUP 信号使 Apache HTTPD Web 服务器重启：
     ```
     $ kill -SIGHUP 1653
     ```
   - 检查父进程未被终止且新的子进程已生成：
     ```
     $ ps aux | grep apache2
     ```
     现在你应该能看到父 apache2 进程以及两个新的子进程。

2. 虽然最初是静态的，但通过结合 ps 和 watch，ps 的输出可以*变为*动态。我们将监控**Apache HTTPD Web 服务器**的新连接。在执行下方描述的任务之前，建议你先阅读 **Apache MPM 通用指令**中 MaxConnectionsPerChild 指令的说明。

   - 在 apache2 的配置文件中添加值为 1 的 **MaxConnectionsPerChild** 指令 —— 在 *Debian* 及其衍生系统中，该文件位于 /etc/apache2/apache2.conf；在 **CentOS** 系列中，位于 /etc/httpd/conf/httpd.conf。不要忘记重启 apache2 以使更改生效。

     需要包含在配置文件中的行是 **MaxConnectionsPerChild 1**。重启 Web 服务器的一种方式是使用 **sudo systemctl restart apache2**。


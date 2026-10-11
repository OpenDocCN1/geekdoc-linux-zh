
在 Ubuntu 等 Debian 发行版中，你可以使用 `sysv-rcconf` 命令（如果已安装）。要关闭通过 `xinetd` 程序启动的服务，只需编辑 `/etc/xinetd/d/` 目录下的服务配置文件。对于传统的基于 System V 的服务，你也可以使用 `chkconfig` 命令禁用服务。例如，要禁用服务，你可以运行：

```
chkconfig --level 3 rpcbind off
```

在使用 `systemd` 的 Linux 发行版（如 Fedora）中，你可以改为使用 `systemctl` 禁用服务。例如，要禁用服务，使用以下命令：

```
systemctl disable xinetd.service
```

## 跨发行版的关闭方法

要防止服务在启动时运行，请更改相应运行级别 `rc.d` 目录中的符号链接（symbolic link）。这是通过进入 `/etc/rc.d/` 目录（Debian 为 `/etc/rc.d`）并在 `rc.d` 目录中找到指向启动脚本的符号链接来实现。（有关启动脚本的信息请参见第 6 章。）将符号链接重命名为 X。如果你决定重启，很容易再次重命名为 S。如果你重命名了启动脚本但想停止正在运行的进程，请使用 `ps` 命令找到进程 ID，然后使用 `kill` 命令终止进程。例如，这里是杀死 `portmap` 进程的命令及其输出：

```
ps aux | grep portmap

bin      255 0.0 0.1 1084 440 p/0 S     Jul08 00:00 portmap

root    6634 0.0 0.1 1152 440 p/0 S     01:55 00:00 grep portmap

kill 255
```

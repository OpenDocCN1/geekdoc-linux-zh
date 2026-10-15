
### Systemd

Systemd（类似于 Upstart——见 p62）可以并行启动服务，并可以在需要时延迟启动服务。与其使用许多组件的脚本，不如设置一个目标（target），`systemd` 会解析其依赖关系直到达到该目标，从而避免了固定的启动顺序。文件位于 `/etc/systemd/system`，其中有很多内容需要学习，但对于任何用户需要记住的一点是，`systemd` 及其服务管理器通过 `systemctl` 命令控制。

```
sudo systemctl restart ssh
```

将重启 `ssh`——如果你更改了它监听的端口，例如，你就需要这样做。为了兼容性，除了使用 `/etc/init.d` 脚本来启动和停止服务外，在旧版本 Raspberryian 中运行的服务命令仍然有效，例如

```bash
sudo service apache2 reload
```

...（在这里我们让运行中的 Apache2 服务器重新读取其配置文件）。在 `/etc/systemd/system/multi-user.target` 下，你会发现像 `cron.service` 等文件，当使用 `ls -l` 仔细检查时，你会看到它们指向 `/lib/systemd/system` 中同名文件的链接（其他 GNU/Linux 发行版可能将文件放在 `/usr/lib` 下）。不要担心这些文件内部的内容看起来很困惑；它们的条件依赖有其逻辑，但在为你的 Pi 项目让软件在每个系统上自动运行之前，你可以安全地忘记它们。即使那时，我们将向你展示另一种使用 `crontab` 的方法——否则你需要了解以下内容，因为那些链接不是手动创建的：

![](img/db18fe165e1f1a64ee0c5d815560917d_59_0.png)

### 链接 (Linked In)

`Systemd` 会自动创建符号链接文件，但有时可能希望某个文件在其他地方的同时出现在本地目录中，这时我们需要我们还没有机会向你展示的实用命令：`ln`。

`ln` 创建一个链接，允许文件实际上同时存在于两个地方。在下面的示例中：

```bash
sudo ln -s /usr/share/doc/python-numpy/THANKS.txt numpy-THANKS.txt
```

...一个文件将出现在你的工作目录中。但通过 `ls -l` 你会发现它是特殊类型的文件，指向实际文件的链接。编辑 `numpy-THANKS.txt`，你会发现链接目录中的 `THANKS.txt` 也会被修改。

软链接（或“符号”链接）通过 `-s` 创建——如果你是跨网络链接，或者链接到可移动驱动器，你甚至不需要所链接的文件实际存在。

`Systemd` 是一个复杂的系统，包含许多元素 - `systemd-unit` - 但它们都有自己的 man 手页，每个都值得仔细读一遍以掌握整体概念。

它保持了与 `init.d` 脚本甚至运行级别（run levels）向后兼容性。

![](img/db18fe165e1f1a64ee0c5d815560917d_59_1.png)

```ini
### X-Stop-Before:
is
### X-Start:
is
### Default-Start:
2 3 4 5
### Default-Stop:
0 6
### X-Wanted-By:
true
### Short-Description: Example instances
### Description:此文件用于构建放置在 /etc/init.d/ 中的脚本
### END INIT INFO
```

关于该格式的更多信息可以在 `update-init(8)` 中找到。这些信息用于在启动过程中动态为启动级别分配序列号。请参见 `/usr/share/doc/etc/init.d/README`。

```bash
pi@raspberry:/etc/systemd $ ls -l
mountall.sh  rc ssh
networking  dev-final
avavami  mountdevfs.sh rc,local sudo
bluetooth  faker-lock triggerhappy
hostname.sh  README
bootstrap.sh  mountdevfs.clean
mntifs.sh  reboot umntfs
checks.sh  kbd rmlogin umntfs
checks.clean.sh rcbd umroot
console-setup rpy rysync umroot
dbus  lightdm python3 urandom
cdrom  modd  procs sendsig xii-common
pi@raspberry:/etc/systemd $ all-boot-clean.sh raspi-config skeleton
```

60 MagPi | 章节元素

它被称为符号链接，是因为它通过链接到目标文件名本身来工作。创建一个硬链接：

```bash
sudo ln /etc/bluetooth/main.conf mybluetooth.conf
```

...你为同一个文件有了两个名字（位置）——听起来是一回事吗？并不完全：如果你在第一个示例中删除了原始文件，你可以用同名但内容不同的新文件替换它，符号链接将指向新文件。在硬链接的情况下，删除原始文件，链接仍然指向数据。

### 位置，位置 (Location, location)

启动脚本——无论是 `init.d` 还是 `systemd`——通常都是守护进程，即你希望一直运行的进程，如 Web 服务器和数据库。有很多执行清理工作的程序需要定期运行——每小时、每天、每周。为此，`cron` 实用是调度此类程序和任务运行的理想选择。`Cron` 会搜索它的配置目录并运行它找到的脚本——查看 `/etc` 中以 `cron` 开头的不同文件夹。

要找到你的系统中没有安装此类内容最简单的方法是搜索 `locate` —— 它在树莓派上默认没有安装。使用 `sudo apt-get install locate`，然后运行 `locate cron` —— 将找到每个包含该名称或作为其名称一部分的文件或目录。

`locate` 工具维护着系统上每个文件的数据库，该数据库由 `cron` 每天更新。如果你做了很多更改，或者想寻找某些内容，运行 `sudo updatedb`。

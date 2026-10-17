
- 编辑`/etc/inittab`。

- 重新启动。

让我们详细看看每个步骤。

## 使用`telinit`测试`xdm`

`telinit`命令用于更改Red Hat Linux系统的“运行级别”。运行级别控制系统操作的各个方面，包括是否应启动`xdm`。由于`xdm`在运行级别5下启动，你需要执行以下命令：

```
/sbin/telinit 5
```

请注意：你必须以`root`身份登录才能使用`telinit`。另外注意，更改运行级别时，不应在Red Hat Linux系统上运行任何其他程序，因为运行级别的更改可能会终止正在运行的程序。如果一切配置正确，稍等片刻后你应该会看到`xdm`登录屏幕。登录并确认X桌面出现。然后注销以确保`xdm`再次出现。如果确实如此，说明你的系统已正确配置为自动启动X。如果有问题，你可以使用`telinit`返回到运行级别3（例如“`/sbin/telinit 3`”），或重新启动。

## 编辑`/etc/inittab`

文件`/etc/inittab`除其他用途外，还用于确定系统的默认运行级别。我们需要将默认运行级别从3改为5；因此，我们需要编辑`/etc/inittab`。使用你喜欢的文本编辑器，更改`/etc/inittab`中的这一行：

```
id:3:initdefault:
```

完成后，它应该看起来像这样：

```
id:5:initdefault:
```

请注意：确保你只将数字3改为5！不要更改其他任何内容，否则你的Red Hat Linux系统可能根本无法启动！完成更改后，退出编辑器，并使用以下命令检查你的成果：

```
less /etc/inittab
```

（按[空格键]翻页浏览文件；按[Q]退出。）如果一切正常，就该重新启动了。使用`shutdown`命令正确关闭系统，然后你就完成了！

## 退出X

完成后，如果想退出X，请选择面板栏上的GNOME脚标，选择“注销”并回答“是”以确认你的决定。然后你将从系统注销。

请注意：如果使用GNOME作为桌面环境，所有当前正在运行的程序将在你重新登录时重新启动。

## 更换你的桌面

你可以使用`Switchdesk`功能来更换桌面环境。`Switchdesk`将显示一个屏幕，允许你在你安装的任何桌面环境之间切换。

运行程序并输入`switchdesk`。

on your system. You will then be asked to exit and restart X. You will see your new desktop of choice after X has restarted. To use the Switchdesk feature you can type `switchdesk` at the command line of an Xterm. If you are using GNOME, click on the GNOME foot, choose

## Virtual Consoles and X

Note that even if you’re running X, you still have access to the regular character-cell user interface. That’s because Red Hat Linux uses virtual consoles while X is running. To switch to a virtual console, press [Ctrl]-[Alt]-[Fn], where [Fn] is any one of the first six function keys. When switching virtual consoles, you should see a standard login prompt; at this point you can login and use the system normally on any (or all) of the virtual consoles. When you’d like to go back to your X session, simply press [Ctrl]-[Alt]-[F7].

Please Note: Some people remap keys under X; if you do this, be aware that your X keyboard mappings will only be active when in X. This can be confusing if, for example, you’ve swapped the [Ctrl] and [Caps Lock] keys under X, as you will have to use two different keystrokes to switch between X and non-X virtual consoles.

## Handy X-Based Tools

There are several tools that can make life easier for the new Red Hat Linux user. They perform tasks that either require root access, or can only be done by memorizing arcane commands. They all require X to run, so you’ll need to get that set up first. These tools are:

- User Information Tool — Makes it easy to update your “gecos,” or basic account information. Run `/usr/bin/userinfo` to start it.

- User Password Tool — Changing passwords is simple with this tool. It’s started by running `/usr/bin/userpasswd`

- Filesystem Mounting Tool — Makes mounting and unmounting filesystems simple. Every user-mountable filesystem must have the user option present in `/etc/fstab` (see the `mount` man page for more information on the user option). Run `/usr/bin/usermount` to start it.

- Network Device Tool – Starting and stopping network interfaces becomes a point-and-click operation with this tool. Run `/usr/bin/usernet` to start this tool. Requires that every interface to be controlled by usernets is configured to be "user-controllable." This can be done by using `netcfg`, and selecting the interface's Allow any user to (de)activate interface checkbox.

## Configuring Your Red Hat Linux System For Sound

By default, the only sound you'll hear out of your newly installed Red Hat Linux system is the ordinary, boring, default beep. If your computer system has sound hardware, chances are you can make it work under Red Hat Linux. In some cases successfully getting sound support to work requires a kernel rebuild. However, most of the time it's possible to use the modular sound drivers.

## Modular Sound Drivers

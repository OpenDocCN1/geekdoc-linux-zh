

- **--firstboot script**
  此选项与 --execscript 类似，只是它会将你指定的脚本复制到 VM 中，并在 VM 第一次启动时执行它。

- **--firstlogin script**
  大多数自动化安装程序选项的缺点是它们要求脚本是非交互式的。--firstlogin 选项没有此限制。它会获取你指定的脚本，并在用户首次登录到 VM 时执行它。由于第一个登录的用户会看到脚本，因此你可以使其具有交互性。你可能还想使用此脚本在 VM 上安装任何具有交互式安装程序的软件包。

一旦你使用 virt-builder 成功创建了 VM，你就可以首次启动 VM 并使用 virsh 管理它。

## Manage VMs with virsh

virsh 命令是你用来管理 VM 的主要工具之一。KVM 的基本语法是 virsh -c qemu:///system 后跟某种命令。例如，要列出所有正在运行的 VM，请输入

```
$ virsh -c qemu:///system list
Connecting to uri: qemu:///system
 Id Name State
---------------------------
```

现在你已经创建了一个新的 VM，你可以使用 start 命令启动它：

```
$ virsh -c qemu:///system start test1
Connecting to uri: qemu:///system
Domain test1 started
```

```
$ virsh -c qemu:///system list
Connecting to uri: qemu:///system
 Id Name State
---------------------------
 9 test1 running
```

请注意，start 命令后跟你想要启动的 VM。与 start 类似的命令有 shutdown 和 destroy，它们将分别关闭 VM 并切断 VM 的电源。如果你希望 VM 在启动时自动启动，请使用 autostart 命令：

```
$ virsh -c qemu:///system autostart test1
Connecting to uri: qemu:///system
Domain test1 marked as autostarted
```

如果你想删除 autostart 选项，请在命令中添加 --disable：

```
$ virsh -c qemu:///system autostart --disable test1
Connecting to uri: qemu:///system
Domain test1 unmarked as autostarted
```

KVM 还支持快照，因此你可以保存 VM 的当前状态并稍后回滚到该状态。要拍摄快照，请使用 save 命令，后跟 VM 和保存状态的文件：

```
$ virsh -c qemu:///system save test1 test1-snapshot.state
Connecting to uri: qemu:///system
Domain test1 saved to test1-snapshot.state
```

稍后你可以使用 restore 命令，后跟之前保存的状态文件，以将 VM 恢复到该状态：

```
$ virsh -c qemu:///system restore test1-snapshot.state
Connecting to uri: qemu:///system
Domain restored from test1-snapshot.state
```

你也可以使用 suspend 和 resume 命令挂起和恢复 VM。请记住，挂起的 VM 仍然会消耗内存资源。挂起的 VM 在列表中会显示为 paused 状态：

```
$ virsh -c qemu:///system suspend test1
Connecting to uri: qemu:///system
Domain test1 suspended
```

```
$ virsh -c qemu:///system list
Connecting to uri: qemu:///system
```

```
Id Name State
-----------------------------
11 test2 running
12 test1 paused
```

```
$ virsh -c qemu:///system resume test1
Connecting to uri: qemu:///system
Domain test1 resumed
```

```
$ virsh -c qemu:///system list
Connecting to uri: qemu:///system
Id Name State
-----------------------------
11 test2 running
12 test1 running
```

使用 VM 的一个特别好的功能是，如果 VM 需要更多 RAM 而你的主机有可用资源，你可以相对轻松地进行更改。首先使用 dominfo 命令查看 VM 当前使用的 RAM 量。VM 关闭后，使用 setmaxmem 命令更改 VM 可用的最大 RAM，并使用 setmem 命令更改 VM 当前可使用的 RAM（两者可以是不同的值，前提是最大内存更大）。重新启动 VM 后，它将使用新的 RAM 量启动：

```
$ virsh -c qemu:///system dominfo test1
Connecting to uri: qemu:///system
-
Id:
Name: test1
UUID: e1c9cbd2-a160-bef6-771d-18c762efa098
OS Type: hvm
State: shut off
CPU(s): 1
Max memory: 131072 kB
Used memory: 131072 kB
Autostart: disable
Security model: apparmor
Security DOI: 0
```

```
$ virsh -c qemu:///system setmaxmem test1 262144
Connecting to uri: qemu:///system
```

```
$ virsh -c qemu:///system dominfo test1
Connecting to uri: qemu:///system
```

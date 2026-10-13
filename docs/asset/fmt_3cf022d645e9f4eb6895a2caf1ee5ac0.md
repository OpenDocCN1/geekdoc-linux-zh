
创建一个指向 `/etc/fstab` 的符号链接 `/run/fstablink`。永远不要原子地删除此行。

# 配置文件优先级

配置文件可能存在于三个地方：

- `/etc/tmpfiles.d/*`
- `/run/tmpfiles.d/*`
- `/usr/lib/tmpfiles.d/*`

`/usr/lib/tmpfiles.d/` 下的文件与 `/run/tmpfiles.d/` 中的文件同名，不应编辑这些文件。`/run/tmpfiles.d/` 下的文件本身是易性文件，通常用于守护进程管理它们自己的临时文件。`/etc/tmpfiles.d/` 下的文件用于管理员配置自定义的临时位置，并覆盖供应商提供的默认设置。

如果 `/run/tmpfiles.d/` 中的文件与 `/usr/lib/tmpfiles.d/` 下的文件同名，则使用 `/run/tmpfiles.d/` 下的文件。如果 `/etc/tmpfiles.d/` 下的文件与 `/run/tmpfiles.d/` 或 `/usr/lib/tmpfiles.d/` 下的文件同名，则使用 `/etc/tmpfiles.d/` 下的文件。

根据这些优先级规则，你可以通过将相关文件复制到 `/etc/tmpfiles.d/` 并进行编辑来覆盖供应商提供的设置。这种工作方式确保了管理员提供的设置可以从中央配置管理系统轻松管理，而不会被软件包更新所覆盖。

> 注意：在测试新的或修改的配置时，仅应用一个配置文件中的命令可能会很有用。这可以通过在命令行上指定配置文件的名称来实现。

> 参考：`systemd-tmpfiles(8)`、`tmpfiles.d(5)`、`stat(1)`、`stat(2)` 和 `systemd.timer(5)` 帮助页

## 引导式练习

## 管理临时文件

在本次次练习中，你将配置 `systemd-tmpfiles` 以更改它从 `/tmp` 移除临时文件的速度，并定期清理另一个目录中的文件。

### 预期结果

你应该能够：

- 配置 `systemd-tmpfiles` 从 `/tmp` 移除未使用的临时文件。
- 配置 `systemd-tmpfiles` 定期清理另一个目录中的文件。

# 在开始之前

使用密码 `student` 以 `student` 用户登录工作站。
在工作站上，运行 `lab scheduling-tmpfiles start` 开始练习。该脚本会创建临时文件并确保环境设置正确。

```
[student@workstation -]$ lab scheduling-tmpfiles start
```

- 1. 从工作站开始，以 `student` 身份向 `servera` 开启 SSH 会话。

```
[student@workstation -]$ ssh student@servera
...输出已省略...
[student@servera -]$
```

- 2. 配置 `systemd-tmpfiles` 清理 `/tmp` 目录，使其不包含五天内未使用的文件。确保配置不会被任何软件包更新覆盖。

2.1. 使用 `sudo -` 命令切换到 root 用户。

```
[student@servera -]$ sudo -i
[sudo] password for student: student
[root@servera -]#
```

2.2. 将 `/usr/lib/tmpfiles.d/tmp.conf` 复制到 `/etc/tmpfiles.d/tmp.conf`。

```
[root@servera -]# cp /usr/lib/tmpfiles.d/tmp.conf /etc/tmpfiles.d/
tmp.conf
```

2.3. 在 `/etc/tmpfiles.d/tmp.conf` 中搜索适用于 `/tmp` 目录的配置行。将配置行中临时文件的现有时长替换为新的 5 天。删除该文件中所有其他行（包括注释掉的行）。你可以使用 `vim /etc/tmpfiles.d/tmp.conf` 命令编辑配置文件。`/etc/tmpfiles.d/tmp.conf` 文件应该显示如下：

```
d /tmp 1777 root root 5d
```

上述配置导致 `systemd-tmpfiles` 确保 `/tmp` 目录存在，且八进制权限设置为 1777。`/tmp` 的所有者和组都必须是 root。`/tmp` 目录必须不包含五天未使用的临时文件。

2.4. 使用 `systemd-tmpfiles --clean` 验证 `/etc/tmpfiles.d/tmp.conf` 文件包含正确的配置。

```
[root@servera ~]# systemd-tmpfiles --clean /etc/tmpfiles.d/tmp.conf
```

由于上一个命令没有返回任何错误，这确认配置设置是正确的。

- 添加一个新配置，确保 `/run/momentary` 目录存在，且用户和组所有权设置为 root。该目录的八进制权限必须为 0700。配置应清理此目录中任何在 30 秒内未使用的文件。

3.1. 创建名为 `/etc/tmpfiles.d/momentary.conf` 的文件，内容如下。你可以使用 `vim /etc/tmpfiles.d/momentary.conf` 命令创建该文件。

```
d /run/momentary 0700 root root 30s
```

上述配置导致 `systemd-tmpfiles` 确保 `/run/momentary` 目录存在，用户和组所有权设置为 root。该目录的八进制权限必须为 0700。配置应清理此目录中任何在 30 秒内未使用的文件。

3.2. 使用 `systemd-tmpfiles --clean` 验证 `/etc/tmpfiles.d/momentary.conf` 文件包含正确的配置。

```
[root@servera ~]# systemd-tmpfiles --clean /etc/tmpfiles.d/momentary.conf
```

由于上一个命令没有返回任何错误，这确认配置设置是正确的。

-. 重新编辑 `/etc/tmpfiles.d/momentary.conf` 确保 `/run/momentary` 目录的用户和组所有设置为 root。

```
[root@servera -]# vim /etc/tmpfiles.d/momentary.conf
```

内容应为：

```
d /run/momentary 0700 root root 30s
```

上述配置导致 `systemd-tmpfiles` 确保 `/run/momentary` 目录存在，用户和组所有权设置为 root。该目录的八进制权限必须为 0700。配置应清理此目录中任何在 30 秒内未使用的文件。

3.3. 使用 `systemd-tmpfiles --clean` 验证 `/etc/tmpfiles.d/momentary.conf` 文件包含正确的配置。

```
[root@servera ~]# systemd-tmpfiles --clean /etc/tmpfiles.d/momentary.conf
```

由于上一个命令没有返回任何错误，这确认配置设置是正确的。

# 第 2 章 | 任务调度

## 管理临时文件

在本次练习中，你将配置 `systemd-tmpfiles` 以更改它从 `/tmp` 移除临时文件的速度，并定期清理另一个目录中的文件。

### 预期结果

你应该能够：

- 配置 `systemd-tmpfiles` 从 `/tmp` 移除未使用的临时文件。
- 配置 `systemd-tmpfiles` 定期清理另一个目录中的文件。

# 在开始之前

使用密码 `student` 以 `student` 用户登录工作站。
在工作站上，运行 `lab scheduling-tmpfiles start` 开始练习。该脚本会创建临时文件并确保环境设置正确。

```
[student@workstation -]$ lab scheduling-tmpfiles start
```

- 1. 从工作站开始，以 `student` 身份向 `servera` 开启 SSH 会话。

```
[student@workstation -]$ ssh student@servera
...输出已省略...
[student@servera -]$
```

- 2. 配置 `systemd-tmpfiles` 清理 `/tmp` 目录，使其不包含五天内未使用的文件。确保配置不会被任何软件包更新覆盖。

2.1. 使用 `sudo -` 命令切换到 root 用户。

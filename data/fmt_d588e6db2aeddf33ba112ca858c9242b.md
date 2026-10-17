
```
if [[ $UID -eq 0 ]]; then
    mount /dev/cdrom/media/cdrom
else
    echo "Sorry, you must be a superuser"
    echo "to mount a CD"
fi
```

- 3. 保存文件并关闭 `edit`。
- 4. 在终端窗口的命令行中，输入此命令：

```
chmod a +x /usr/local/bin/mount-cd
```

该命令使得该文件对系统上的所有人都是可执行的。

用户 `freddie` 登录时的 SID 为 500，但如果 `freddie` 切换超级用户权限，他的 EUID 会从 500 变为 0。

> 超级用户的 EUID 始终为 0。当用户拥有足够权限时，这是验证权限的一种快速简便的方法。

现在，你可以创建一个脚本来列出邮件程序中的用户名（可能是向会计部，即 `acctg` 部门的每个人发送消息）：

你可以在脚本中使用 `EUID` 来判断运行脚本的用户是否拥有额外权限。例如，编写一个为其他用户挂载 CD 驱动器的脚本非常简单：

```bash
$ grep acctg /etc/group | cut -d ':' -f 4

Subject: Downtime
```

如果你正在使用 Fedora 或 Mandrake，请按照以下步骤操作：

会计系统在本周末将维护  
-- Freddie

- 1. 打开你的终端并输入以下命令：

```bash
$ edit /usr/local/bin/mount-cd
```

该命令会打开编辑器并在 `/usr/local/bin` 目录下创建一个名为 `mount-cd` 的文件。

- 2. 输入以下文本：

```bash
#!/bin/bash
if [[ $EUID -eq 0 ]]
then
  mount /dev/cdrom /mnt/cdrom
else
  echo "Sorry, you must be a superuser"
  echo "to mount a CD"
fi
```

当你需要执行影响该组的命令时，使用变量来保存一组文件或名称。

如果你想在执行替换前查看替换后的命令预览，请按 `Esc-Ctrl-E`。如果预览看起来良好，按 `Enter` 执行命令。

# 42 技术 7：利用方便的自动变量少打字、做更多事

- 3. 保存文件并关闭 `edit`。
- 4. 在终端窗口的命令行中，输入此命令：

```
chmod a +x /usr/local/bin/mount-cd
```

该命令使得该文件对系统上的所有人都是可执行的。

如果你的系统运行的是 SuSE Linux，请按照以下步骤创建一个 shell 脚本，为有效用户 ID 为 0 的用户挂载 CD 驱动器：

- 7. 打开你的终端并输入以下命令：

```bash
$ /usr/local/bin/mount-cd
```

- 2. 输入以下文本：

```bash
#!/bin/bash
if [[ $UID -eq 0 ]]; then
    mount /dev/cdrom/media/cdrom
else
    echo "Sorry, you must be a superuser"
    echo "to mount a CD"
fi
```

- 3. 保存文件并关闭 `edit`。
- 4. 在终端窗口的命令行中，输入此命令：

```
chmod a +x /usr/local/bin/mount-cd
```

该命令使得该文件对系统上的所有人都是可执行的。

## 44 技巧 7：使用巧妙的自动变量少打字多做事

现在，为了执行你的程序并让你的自定义变量准备就绪，只需在命令行行的开头输入一个点（`.`）和一个空格，如下所示：

对于该脚本，`bash` 将启动一个新的 shell 会话，运行你的脚本，并立即终止该新 shell 会话。

```
$ setvars.bash
Your custom variables are ready for use
echo $SRC
/usr/local/src
$
```

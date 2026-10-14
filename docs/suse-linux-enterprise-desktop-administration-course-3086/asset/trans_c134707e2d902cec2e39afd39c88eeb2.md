

## gconf-editor

要设置或更改强制设置，在使用 gconf-editor 时必须以 root 身份登录。你采取的步骤取决于需要执行的操作：

- 第一次将首选项设为强制
- 更改现有的强制首选项

## 第一次将首选项设为强制

以 root 用户身份启动 gconf-editor。窗口左侧列出了可用的键。浏览树结构找到要设为强制的键并将其设置为所需值。然后用鼠标右键选择该条目；在上下文菜单中选择设为强制。

如果你再次点击该条目尝试更改它，错误消息会告诉你这是不可能的。

## 更改现有的强制首选项

以 root 用户身份启动 gconf-editor；然后选择文件 > 新建强制设置。窗口左侧列出了在 /etc/opt/gnome/gconf/gconf.xml.mandatory/ 仓库树中已设置的那些强制设置。你可以按照“用户定义设置”中说明的方式更改它们。

要从强制首选项中移除一个键，右键单击该条目并选择取消设置键。

此前未设置为强制值的键不会显示在此 gconf-editor 对话框左侧的仓库树中。

## gconftool-2

你也可以使用 gconftool-2 命令行工具将首选项设置为强制值。 （使用 gconftool-2 时，gconf-editor 可以帮助你浏览配置仓库树以找到正确的键及其路径。）

假设公司的安全策略要求桌面屏幕在 5 分钟不活动后锁定。作为管理员，你的任务是相应地配置工作站并确保所有用户都遵守此策略。

以普通用户身份使用 gconf-editor，你浏览仓库树并发现用于此目的的键是 /apps/gnome-screensaver/lock_enabled 和 /apps/gnome-screensaver/idle_delay。要将它们设置为强制值，以 root 身份登录并使用以下命令：

```
da10:~ # killall gconf-2
da10:~ # gconftool-2 --direct --config-source
xml:readwrite:/etc/opt/gnome/gconf/gconf.xml.mandatory --set --type
bool /apps/gnome-screensaver/lock_enabled true
Resolved address "xml:readwrite:/etc/opt/gnome/gconf/gconf.xml.mandatory"
to a writable configuration source at position 0
da10:~ # gconftool-2 --direct --config-source
xml:readwrite:/etc/opt/gnome/gconf/gconf.xml.mandatory --set --type
int /apps/gnome-screensaver/idle_delay 5
Resolved address "xml:readwrite:/etc/opt/gnome/gconf/gconf.xml.mandatory"
to a writable configuration source at position 0
```

下次用户登录并尝试在 GNOME 控制中心更改相应的屏幕保护程序设置时，用户将无法更改这些值。

![](img/9129877170834ca9d5fdac5319bf5f12_580_0.png)

并非所有可以设置的键值对似乎都能产生预期效果。例如，将 /apps/firefox/general/homepage_url 键设置为某个值似乎对 Firefox 浏览器的默认主页没有任何影响。其他此类键值对也可能表现不正常。因此，在依赖你的设置之前，你应该测试你的设置以确保它们具有预期效果并且用户无法更改。

## 使用桌面配置文件编辑器

桌面配置文件编辑器（sabay on package）允许你作为管理员按用户设置首选项。

使用桌面配置文件编辑器包括两个步骤：

- 定义配置文件
- 将配置文件分配给用户

## 定义配置文件

要启动桌面配置文件编辑器，选择计算机 > 更多应用程序 > 系统 > 桌面配置文件编辑器。系统会提示你输入 root 密码。会出现一个用户配置文件编辑器窗口，如图 14-6 所示。

![](img/9129877170834ca9d5fdac5319bf5f12_580_1.png)

图 14-6

由于不存在配置文件，你必须添加一个配置文件。选择添加并为新配置文件输入名称。此名称会出现在用户配置文件编辑器窗口中。选择该名称；然后选择编辑。将在 xnest 窗口中启动一个 GNOME 桌面。

在该窗口中，你可以根据需要配置桌面。

![](img/9129877170834ca9d5fdac5319bf5f12_580_2.png)

当 xnest 窗口中的屏幕保护程序锁定该屏幕时，你可以使用主机机器的 root 密码将其解锁。

完成后，在编辑配置文件 profilname 窗口中，选择编辑 > 更改。见图 14-7。

![](img/9129877170834ca9d5fdac5319bf5f12_581_0.png)

# 图 14-7

列表显示自会话开始以来或自上次保存更改以来所做的所有配置更改。要使更改成为强制性，请单击相应行上的锁。要忽略更改，请选中“忽略”复选框。如果你未选择任何一项，该值将用作默认值。

要保存配置文件，选择配置文件 > 保存。要关闭 xnest 窗口，选择配置文件 > 退出。配置文件保存在 /etc/opt/gnome/desktop-profiles/ profilname.zip 中。它包含诸如 .gtkrc 和包含诸如 .gconf.xml.mandatory/desktop/gnome/background/%gconf.xml 之类的键的 GConf 首选项等配置文件。

## 将配置文件分配给用户

创建配置文件后，你可以通过在用户配置文件编辑器中选择配置文件然后选择用户，将其分配给特定用户或所有用户。

会出现图 14-8 所示的对话框。

![](img/9129877170834ca9d5fdac5319bf5f12_582_0.png)

图 14-8

选择配置文件适用的用户，或选择对所有用户使用此配置文件。此信息存储在 /etc/opt/gnome/desktop-profiles/users.xml 中。

每次用户登录到其 GNOME 桌面时，都会执行 /etc/X11/xinit/xinitrc.d/sabayon-xinitrc.sh 脚本：

```
#!/bin/bash
#
# Apply the Sabayon profile for the current user (if any)
#
if [ "$XDISABLE_SABAYON_XINITRC" = "x" ] ; then
  if [ -x /opt/gnome/sbin/sabayon-apply ] ; then
    /opt/gnome/sbin/sabayon-apply
  fi
fi
```

这反过来会执行 /opt/gnome/sbin/sabayon-apply。对于具有配置文件的用户，此命令会将 .zip 文件中包含的文件复制到用户的主目录。然后 gconftool-2 按 /etc/opt/gnome/gconf/2/path 中给出的顺序读取各种仓库并相应地设置首选项。

作为管理员，你应该意识到用户至少可以暂时规避在 Sabayon 的配置文件编辑器中标记为强制的设置。用户只需

- 终止 gconfd-2
- 删除 ~/.gconf.* 文件和目录

之后，用户可以更改在编辑器中标记为强制的设置。在 /etc/opt/gnome/gconf/gconf.xml.mandatory 中设为强制的设置无法以这种方式规避。

下次用户登录到 GNOME 时，被删除的 GConf 文件会被复制回用户的主目录。

因此，Sabayon 应被视为一种提供可通过注销并重新登录轻松恢复的稳定配置的手段，而不是限制用户的方式。

![](img/9129877170834ca9d5fdac5319bf5f12_583_0.png)

## 练习 14-3：为首选项设置强制值

在此练习中，你使用桌面配置文件编辑器设置强制首选项。
使用桌面配置文件编辑器（Sabayon）使所有用户在 5 分钟不活动后锁定屏幕。

## 完成此练习的详细步骤

要设置强制首选项，请执行以下操作：

- 1. 在 GNOME 桌面上，选择计算机 > 更多应用程序 > 系统 > 桌面配置文件编辑器。在出现的对话框中输入 root 密码（n0v311）。
- 2. 在用户配置文件编辑器对话框中，选择添加。然后，在添加配置文件对话框中，输入 penguins 作为配置文件名称；然后选择添加。
- 3. 选择编辑；打开一个 xnest 窗口。
- 4. 在此窗口中，选择计算机 > 控制中心 > 屏幕保护程序。将会话空闲后设置为滑块移动到 5 分钟。
  还将会话空闲时激活屏幕保护程序和屏幕保护程序激活时锁定屏幕的设置切换一次开和关。
  关闭对话框。
- 5. 在 xnest 窗口的菜单中，选择编辑 > 更改。
  单击将 idle_delay 键设置为 5 分钟、会话空闲时激活屏幕保护程序以及屏幕保护程序激活时锁定屏幕的条目前的锁。
- 6. 在 xnest 窗口的菜单中，选择配置文件 > 保存。关闭 xnest 窗口。
- 7. 在用户配置文件编辑器窗口中，确保 penguins 已被选中；然后选择用户。
- 8. 在 Penguins 配置文件的用户对话框中，选择对所有用户使用此配置文件。
- 9. 从 GNOME 桌面注销。再次登录。尝试更改屏幕保护程序设置。

![](img/9129877170834ca9d5fdac5319bf5f12_583_1.png)

如果你仍能编辑屏幕保护程序设置，请打开一个终端窗口，执行 killall gconfd-2，删除 .gconf* 目录和文件，然后注销并重新登录。然后再次尝试更改屏幕保护程序设置。


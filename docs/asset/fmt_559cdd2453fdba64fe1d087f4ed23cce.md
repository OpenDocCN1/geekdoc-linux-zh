
1. 初始键盘设为 Default: Default Console Mapping（默认：默认控制台映射），它适用于大多数键盘。

2. 按 ⇩ 显示键盘列表。

3. 按 ⇧ 或 ↓ 滚动到您的键盘项，然后按 Enter 选择它。

4. 按 Tab 移动到下一个字段。

## 显示器配置

默认显示器设为 Generic 640x480 @ 60Hz 13 inch。

- 按 ⇩ 显示显示器列表。
- 按 ⇧ 或 ↓ 滚动到您的显示器项，然后按 Enter 选择它。
- 按 Tab 移动到下一个字段。
- 如果您需要更改屏幕宽度 (mm)，请在此处编辑。
- 按 Tab 移动到下一个字段。
- 如果您需要更改屏幕高度 (mm)，请在此处编辑。
- 按 Tab 移动到下一个字段。

## 屏幕保护程序

某些显卡和显示器支持显示电源管理系统 (DPMS)，它在用户停止输入时减少显示器的功耗。如果您的硬件具有此功能，可以在此部分控制 DPMS 阶段。典型的 DPMS 设置具有级联效应，各个阶段将根据您选择的延迟时间连续激活。

- 屏幕保护程序 (Screen Saver) - DPMS 的初步阶段，空屏但不降低功耗。
- 待机模式 (Standby Mode) - DPMS 的第一阶段，通过禁用向显示器的水平同步信号提供中等节能效果。
- 挂起模式 (Suspend Mode) - DPMS 的第二阶段，通过禁用向显示器的水平同步信号提供显著节能效果。
- 显示器关闭 (Monitor Off) - DPMS 的最终阶段，通过禁用向显示器的水平和垂直同步信号提供最大节能。

1. 在 X Screen Saver Delay（X 屏幕保护程序延迟）字段中，按 Enter 开启或关闭此选项。

2. 如果开启，按 Tab 移动到 Minutes（分钟）字段，然后使用按键设置值。

3. 按 Tab 移动到下一个字段。

4. 在 Standby Mode Delay（待机模式延迟）字段中，按 Enter 开启或关闭此选项。

5. 如果开启，按 Tab 移动到 Minutes（分钟）字段，然后使用 ← 或 → 设置值。

6. 按 Tab 移动到下一个字段。

7. 在 Suspend Mode Delay（挂起模式延迟）字段中，按 Enter 开启或关闭此选项。

8. 如果开启，按 Tab 移动到 Minutes（分钟）字段，然后使用 ← 或 → 设置值。

9. 按 Tab 移动到下一个字段。

10. 在 Monitor Off Delay（显示器关闭延迟）字段中，按 Enter 开启或关闭此选项。

11. 如果开启，按 Tab 移动到 Minutes（分钟）字段，然后使用 ← 或 → 设置值。

# 多屏幕配置

Metro-X 支持多达四个屏幕，并可以通过单个键盘和鼠标同时控制所有屏幕。这允许你运行许多应用程序而不会产生窗口重叠，对于图像处理工作特别有用。对于使用的每个屏幕，必须为该屏幕的显示器和显卡创建单独的配置。关于显卡要求请参见第 C.1.4 节。

# 添加屏幕

Metro-X 默认采用单屏设置。第一个配置的屏幕被标记为 Screen 0。当你添加第二个屏幕时，其所有默认配置都将复制 Screen 0 的当前设置。因此，如果所有屏幕的硬件相同，你可以在添加其他屏幕之前先配置 Screen 0，从而节省时间。同样，随着屏幕的增加，每当你添加另一个屏幕时，当前激活的屏幕的设置将决定新屏幕的默认设置。

1. 按 Alt-S 显示屏幕拉取菜单。

2. 输入 A 进行添加（Add）。

3. Screen 0 的显示器和显卡图标变为轮廓，而 Screen 1 显示两个全彩色图标。

4. 如果需要对新屏幕的配置进行任何更改，请参考本章前面介绍的步骤。

5. 使用 Page Down 和 Page Up 键移动到每个屏幕的配置页面。

# 删除屏幕

当删除一个屏幕时，所有编号更高的屏幕都会立即向下移动一个位置。例如：你配置了屏幕 0、1 和 2，然后删除了屏幕 1。该屏幕及其所有的配置信息将消失。屏幕 2 随后变为屏幕 1，但保留其自身的配置。你最后将剩下屏幕 0 和屏幕 1。

# 使用 Metro-X 进行 X Window 配置

1. 使用 Page Down 或 Page Up 键激活你想要删除的屏幕图标组。

2. 按 Alt-S 显示屏幕拉取菜单。

3. 输入 D 进行删除（Delete）。

4. 一组显示器和显卡图标消失。编号更高的屏幕（如果有）将立即填补被删除屏幕留下的空隙。

# 布局

屏幕布局（Screen Layout）窗口允许你指定多个屏幕在工作区中的排列方式，以便鼠标在屏幕之间的移动是合理的。

1. 按 Alt-S 显示屏幕拉取菜单。

2. 输入 L 进入布局（Layout）。

3. 屏幕布局窗口出现。

4. 按 Ctrl 和 Alt 查看你屏幕的各种布局组合。

5. 当显示你所需的布局时，按 Enter键选择它。

# 字体路径

如果需要，你可以在 Metro-X 配置工具内部编辑字体路径。如果你正在使用字体服务器代替或额外使用现有的字体，这将是必要的。

1. 按 Alt-C 显示配置拉取菜单，然后按 Enter。

2. 字体路径（Font Path）窗口出现。

3. 根据系统需要对文件进行编辑。Metro-X 按照文件中列出的目录的顺序查找字体。如果你使用字体服务器，请将其作为第一行输入：

```
tcp/<fontserver>:7000
```

# 安装后配置

如果端口号不是默认的 7000，请更改为适用于系统的端口号。

4. 按 Tab 在底部按钮之间移动，按 Enter 选择一个。如果信息正确，选择 OK 按钮。如果你想忽略已所做的更改，选择 Cancel 按钮。如果你编辑了字体路径并想回到原始设置，选择 Load Defaults 按钮。

# 保存并退出

1. 按 Alt-F 显示文件拉取菜单。

2. 输入 S 保存并退出（Save and Exit）。

3. 更改已保存，Metro-X 配置工具关闭，你的系统现在准备好运行 Metro-X！

# 不保存退出

1. 按 Alt-F 显示文件拉取菜单。

2. 输入 Q 退出（Quit）。

3. 出现警告框：在退出前保存当前配置！

4. 按 Tab 移动到 No 按钮，按 Enter 确认不保存更改并退出 Metro-X 配置工具。

# 6.4 鼠标配置

要配置你的鼠标（或在安装后重新配置），输入命令 `/usr/sbin/mouseconfig`。使用方向键向下滚动列表，直到你的鼠标类型被高亮。如果你连接的是 PS/2 类型的端口，应选择 PS/2。如果你连接的是 ATI 视频显卡，应选择 ATI。

# 5.5 鼠标

同时点击左和右鼠标按钮使用 Tab 键移动光标，按空格键切换选择。

# 6.5 Sendmail

默认的 `sendmail.cf` 文件将安装在 `/etc/`。默认配置对于大多数 SMTP 站点有效，但对于 UUCP 站点无效；如果你需要使用 UUCP 传输，请生成新的 `sendmail.cf`。如果你需要安装 m4 软件包，请生成新的 sendmail 源。关于创建 sendmail 配置的更多信息，请阅读 `README` 文件。一种常见的 sendmail 配置是让单台机器作为网络上所有机器的网关。例如，Red Hat Software 有一台机器接收并处理所有邮件。在那台机器上，我们只需要在 `/etc/sendmail.cf` 中添加所有机器的名称。如下：

```
# sendmail.cw - include all aliases for your machine
torgo.redhat.com
poodle.redhat.com
devel.redhat.com
```

然后在其他机器 torgo、poodle 和 devel 上，我们需要编辑 `/etc/sendmail.cf` 在发送邮件时“伪装”为 redhat.com，将任何本地邮件转发到 redhat.com。在 `/etc/sendmail.cf` 中找到 `DR` 和 `DM` 行并进行编辑：

```
# who send unqualified names to
# (null means deliver locally)
DRmailredhat.com
```

```
# who send unqualified names to
# (null means deliver locally)
DRmailredhat.com
```

```
# who send unqualified names to
# (null means deliver locally)
DRmailredhat.com
```

```
# who send unqualified names to
# (null means deliver locally)
DRmailredhat.com
```

```
# who send unqualified names to
# (null means deliver locally)
DRmailredhat.com
```

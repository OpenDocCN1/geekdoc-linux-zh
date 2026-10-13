
`output database: log, mysql, user=snort password=snortpass dbname=snort host=localhost`

`mysql`

```
mysql> SET PASSWORD FOR 'root'@'localhost'=PASSWORD('somepassword');
```

为 `root` 账户分配密码后，直接输入 `mysql` 将无法进入交互式命令模式。分配密码后，使用 `mysql -u<username>-p`。系统将提示输入指定用户（通常是 `root`）的密码。

4. 下一步是创建 Snort 数据库。
5. 现在你赋予 Snort 用户权限以向 Snort 数据库添加所需的表。使用这些命令：
6. 你应该将 Snort 用户的密码设置为 Snort 配置文件使用的相同密码。
7. 下一步是使用以下命令为 Snort 数据库添加额外的权限：

```
mysql> create database snort;
```

```
mysql> grant INSERT,SELECT on root.* to snort@localhost;
```

```
mysql> SET PASSWORD FOR 'snort'@'localhost'=PASSWORD('snortpass');
```

![](img/0eb7273a8d9e486628f6e18d37ab22c6_262_0.png)

```
mysql> grant ALL ON snort.* to snort@localhost;
mysql> grant ALL TO snort;
mysql> exit
```

8. 现在数据库已经创建，你需要用 Snort 使用的表来填充它。使用以下命令创建表：

```
mysql -u root -p /etc/snort/schemas/create_mysql snort
```

当命令完成时，它不会给出任何成功的迹象；因此，有必要手动验证表是否已创建。

> 如果你安装的包不包含 `/snort/schemas/` 目录，你可以下载源包并从那里提取该目录。对于 Fedora Core 5，由于某种原因，安装带 MySQL 支持的 Snort 并没有包含 schemas 目录。

9. 通过输入以下命令验证 Snort 数据库中是否创建了 MySQL 表。你应该能看到与示例所示类似的输出：

```
mysql -u root -p
show databases;
+----------------++
| Database |
+----------------++
| mysql    |
| snort    |
| test     |
+----------------++
use snort;
show tables;
```

| Tables_in_snort |
| :--- |
| data |
| detail |
| encoding |
| event |
| icmphdr |
| ipphdr |
| opt |
| reference |
| reference_system |
| schema |
| sensor |
| sig_class |
| sig_reference |
| signature |
| tcphdr |
| udphdr |

`exit`
数据库列表并不重要，只要 Snort 数据库存在即可（当然）。表列表必须是准确的。

# 配置入侵检测系统 • 第4章 25

请注意底部标记为 ACTION 的字段。这允许你配置告报组。告报组本质上是快捷方式，让你能够快速查看告报的子集，而无需在各种菜单中来回查找。例如，假设你想随时知道 `192.168.1.1` 何时生成了告报。你可以勾选 `192.168.1.1` 左侧的方框，然后使用 `{action}` 下拉菜单选择 AG（按名称）。在告报列中，输入 `._ALERTS` 作为告报组名称。最后，点击 Selected（已选择）。

接下来的屏幕将允许你为新创建的告报组输入描述。为该组输入有意义的文本描述，并点击 Save Changes（保存更改）。下一个屏幕将显示来自 `192.168.1.1` 的告报列表。此屏幕就是告报组。将来，如果你想快速查看组告报，可以点击每个页面底部的 Alert Group Maintenance（告报组维护），然后点击你想查看的告报组。通过这种方式，任何告报子集只需两次点击即可到达，类似于指向特定过滤过滤标准的快捷方式。

另一个值得注意的功能是每个页面底部的 Administration（管理）链接。这将带你进入一个可以在其中为 BASE 配置用户的屏幕。管理界面上有四个选项：list users（列用户）、create user（创建用户）、list roles（列角色）和 create role（创建角色）。这些屏幕允许你创建用户并将他们分配给各种角色。如果你点击 List Roles（列角色），你可以看到四个预定义的角色。如果你想分配一个管理员角色的用户，只需点击 Create user（创建用户）。输入登录名、全名或描述以及密码。使用下拉框选择角色，然后点击 Submit Query（提交查询）。在编辑 `base_conf.php` 文件并更改 `$Use_Auth_System = 1;` 的值之前，任何设置都不会生效。值 `0`（默认值）表示禁用身份验证，所有人都有 BASE 的完全访问权限。只有管理员角色可以访问管理界面。

![](img/0eb7273a8d9e486628f6e18d37ab22c6_268_0.png)

记住命令行中 Snort 的不同日志选项。之前，我们使用了 `–A console`，它会将 Snort 事件加载到 Snort 终端。如果你打算使用不同的前端来查看 Snort 告报，那么记录到控制台并没有太大价值。你可以

![](img/0eb7273a8d9e486628f6e18d37ab22c6_268_1.png)

在启动 Snort 时使用 `– none`，这将导致 Snort 不向 Snort 终端记录任何内容，从而提高性能。

# 其他 Snort 插件

Snort 实用工具和插件的数量令人印象深刻。其中一些工具解决的是关键问题，如保持你的 Snort 规则库更新到最新，而另一些工具则提供了额外的性能改进，例如更快的记录。如果你正在寻找某个特定的功能或选项，你应该在互联网上进行搜索，你可能会发现你寻找的功能已经存在了。如果你确实发现感兴趣感兴趣插件，请记住在部署到生产环境之前对其进行充分测试。

# 使用 Oinkmaster

你可能会对不断更新 Snort 签名文件感到厌倦。因为 Snort 是一种基于签名的 IDS，拥有当前的签名至关重要。如果没有当前的签名文件，你可能无法察觉发生在眼前的入侵尝试。虽然 Snort 本身不包含自动更新签名文件的方法，但还有另一个可以帮助的工具叫做 Oinkmaster (`http://oinkmaster.sourceforge.net/features.shtml`)。Oinkmaster 是一个 Perl 脚本，它可以从 Snort 网站更新你的 Snort 规则。因为它使用 Perl，Oinkmaster 将 Linux 或 Windows Snort 主机上运行。可以调度 Oinkmaster Perl 脚本运行，并按照你喜欢的频率检查更新。要在不等待 Snort 下一个版本发布的情况下下载 Snort 规则，你必须在 Snort 网站注册。你可以在 `https://snort.org/pub-bin/register.cgi` 免费注册。密码将发送到你在注册期间提供的邮箱。这里概述了 Oinkmaster 的配置。

- 1. 登录 Snort 网站后，点击显示 User Preferences（用户偏好）链接。
- 2. 页面底部有一个名为 Oink Code 的部分；点击 Get Code（获取代码）按钮。

![](img/0eb7273a8d9e486628f6e18d37ab22c6_269_0.png)

- 3. 复制此代码供 Oinkmaster 配置文件使用。
- 4. 从 Oinkmaster 网站下载最新的 tar.gz。
- 5. 将压缩包中的文件夹提取到 `/etc/oinkmaster`。
- 6. 编辑 `oinkmaster.conf` 文件。找到指定当前版本 URL 的行。（你可以搜索 CURRENT.）通过删除 `#` 来取消该行的注释，并将你的 oink 代码粘贴到该行中以替换 `<oinkcode>`。

```
url = http://www.snort.org/pub-bin/<oinkcode>/tar.gz
```

- 7. 使用以下命令启动 Oinkmaster：

```
oinkmaster.pl -C /etc/oinkmaster/oinkmaster.conf -o /etc/snortrules
```

完成后，Oinkmaster 会告诉你规则已更新。要配置 cron 守护进程，在 crontab 中添加以下行：

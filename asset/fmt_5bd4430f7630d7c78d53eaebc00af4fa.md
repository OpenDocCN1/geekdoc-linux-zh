
此部分的名称必须包含 `[backend_value_of_backend]` 下 `backend` 参数指定的名称。默认值是 `ndomy_1`。如果 `backend` 参数的值与任何定义的后端部分均不匹配，NagVis 将拒绝工作。

`backendtype` 定义后端的类型，目前 `ndomy`——一种基于 MySQL 的 NDO 数据库——是唯一可能的值。

`dbhost` 和 `dbport` 指定数据库的主机或 IP 地址以及相应的 TCP 端口，`dbname` 包含 NDO 数据库的名称，`dbuser` 和 `dbpass` 定义访问的用户和密码。

默认定义的 `prefix` 和 `dbinstancename` 值是为 NDOU 标准设置的。只要你没有更改 `ndom.cfg` 文件中的 `instance_name` 参数（参见第 384 页的 17.4.1 调整事件代理配置）以及 `ndo2db.cfg` 文件中的 `db_prefix`（参见第 385 页的 17.4.2 配置数据库访问），就可以使用此处给出的值。

`withoutupdate`: 这定义了允许 Nagios 状态更新出现的时间（秒）。如果超过了此处指定的时间，NagVis 将认为数据已过时并显示为错误。如果 Nagios 跨越分式服务器访问多个数据库，那么服务器之间的时钟同步至关重要，否则如果时间差超过了 `maxtimewithoutupdate` 秒，NagVis 将拒绝工作。

此时我们应该提到另一个涉及 NDO 数据库与 NagVis 之间数据交换的问题：NagVis 会评估当前状态。然而，3.0b1 之前的 Nagios 版本仅在夜间更改日志文件后将此状态写入 NDO 数据库。从 3.0b1 版本开始，Nagios 每几秒更新一次状态，因此 NagVis 始终拥有最新的信息。

## 18.1.3 用户身份验证

NagVis 要求用户进行身份验证。如果没有身份验证，它将只会发布错误消息。

如果 Nagios 的共享目录无法用于身份验证访问（如 1.5.1 设置 Apache 中的 Apache 配置中所示），您应该在 Apache 配置文件 `/etc/apache2/conf.d/nagios` 中进行更改。身份验证数据最好从 CGI 目录获取（参见第 47 页的 1.5 Web 配置）。

![](img/8e1ca2e9d03c845e2cebae88c24b6c80_416_0.png)

图 18-3. 在显示的图形上右键点击鼠标后，将出现菜单。

- [^185]http://www.nagvis.org/
- [^186]http://www.nagvis.org/screenshots
- [^187]如果 NagVis 配置文件 `config.ini.php` 中使用的参数 `gdglibs`（参见 18.1.1 安装源代码）设置为 0，则可以在不使用 GD 库的情况下进行。
- [^188]完整文档可以在 http://www.nagvis.org/docs/1.3/nagvis_config_format_description 找到。
- [^189]http://www.nagvis.org/downloads
- [^190]相应的指南可以在 http://www.nagvis.org/docs/extending/iconsets 找到。
- [^191]FAQ 条目 http://www.nagvis.org/docs/general/faq#how/to/run/nagvis/without/authentication 描述了在没有身份验证的情况下运行，但出于安全考虑你不应这样做。

## 18.2 创建 NagVis Maps

NagVis 界面通过 URL `http://nagiosserver/wui/index.php` 访问（请将 `nagiosserver` 替换为您自己的 Nagios 主机名，如图 18-3 所示）。点击右键按钮时会打开叠加菜单。对于浏览器，点击右键按钮将导致菜单消失。

如果没有可用的 PNG 格式背景，您可以通过“Manage | Backgrounds”（管理 | 背景）菜单创建一个新的空白背景图像（如图 18-4 所示）。例如，创建了一个 800 像素的灰色背景（如图 18-4 所示）。

![](img/8e1ca2e9d03c845e2cebae88c24b6c80_17.png)

此图像在屏幕上以原始大小显示，即不缩放。为了避免滚动条，它不应过大。

[滚动,1819]

![](img/8e1ca2e9d03c845e2cebae88c24b6c80_418_0.png)

图 18-6. 通过图形界面插入对象

图 18-5 创建的地图名称为 Test。图 18-5 创建的地图 Vis 为 Test。

将鼠标悬停在图标上时，会打开悬停菜单，如图 18-8 所示。它清晰地区分了哪些设置是继承的，哪些是直接在对象中指定的。如果你点击那里的“更改”（Change）链接，可以再次更改设置。

![](img/8e1ca2e9d03c845e2cebae88c24b6c80_420_0.png)

**图 18-8.** 将鼠标悬停在插入的对象上时，会打开悬停菜单

当你的工作完成后，忘记通过上下文菜单项保存更改（参见第 396 页的图 18-3）。NagVis 中的“打开地图”（Open Map）菜单项将带你进入完成后的视图，该视图现在显示实际状态。

在图 18-9 中，主机组图标上添加了一个文本框。下方显示的字段是一个悬停菜单，当你将鼠标悬停在对象上时，它会显示对象及其状态的信息。此示例显示了主机组中的两个主机显示“非 OK”状态，且该状态已通过确认得到确认。

## 总部

## 主机组

| 主机组名称 | 总部 |
| --- | --- |
| Alias | CRITICAL (已确认) |
| Summary State | 有 1 个 CRITICAL、1 个 WARNING、8 个 UP 主机。 |
| Summary Output | 输出 |
| 3 | CRITICAL (已确认) 主机为 UP。有 1 个 CRITICAL、13 个 OK 服务。 |
| ELIFS01 | WARNING (已确认) 主机为 UP。有 1 个 WARNING、8 个 OK 服务。 |
| ELITS05 | UP | 主机为 UP。有 11 个 OK 服务。 |
| ELITS06 | UP | 主机为 UP。有 11 个 OK 服务。 |
| ELITS07 | UP | 主机为 UP。有 11 个 OK 服务。 |
| ELITS03 | UP | 主机为 UP。有 37 个 OK 服务。 |
| AHPS01 | UP | 主机为 UP。有 23 个 OK 服务。 |
| AHDC01 | UP | 主机为 UP。有 30 个 OK 服务。 |

图 18-9. 完成视图中带有文本框和悬停菜单的对象

完成的地图可以通过 URL `http://nagiosserver/nagios/nagvis/index.php?map=mapname` 直接调用。

## 18.2.1 以文本形式编辑配置

NagVis 将地图的整个配置存储在文本文件中，可以使用文本编辑器进行编辑。`/usr/local/nagios/share/nagvis/etc/maps/`。如果你使用具有已知光栅的背景图像，可以在 WUI 中插入对象，并使用坐标继续编辑地图。图 18-2 所示地图就是这样创建的。背景图像光栅（图 18-1）是用 OpenOffice 创建的，为了获得可重复的绘图，并将 OpenOffice 绘图导出为 PNG 文件。

文本文件的配置选项非常详尽，在在线文档中有描述。[19]。

## 18.2.2 将 NagVis 地图添加到 Nagios Web 界面

NagVis 地图也可以集成到 Nagios Web 界面中。图 18-10 显示了在 index.html 页面添加第三个帧后的效果，该帧将一个高度为 32 像素的地图绑定在主窗口下方。无论管理员当前正在处理什么，最重要的状态（这里是主机组）始终直接显示，并可以通过单击一次访问。在 NagVis 中，你用户界面的梦想是无限制的！

![](img/8e1ca2e9d03c845e2cebae88c24b6c80_422_0.png)

图 18-10. Nagios Web 界面中作为“脚注”的 NagVis 地图

[192] http://www.nagvis.org/docs

## 19. 性能数据的图形显示

当 Nagios 向管理员快速且选择性报告发生的问题时，它基本上可以区分 OK 状态和错误状态，从而避免管理员收到有关问题的服务和主机的大量信息。一段时间内测量值的图形显示无法集成到这种“红绿灯模式”中，但可以通过第三方软件实现。Nagios 支持通过专门创建的接口对值进行外部处理。通过它处理的数据在 Nagios 术语中称为*性能数据*（performance data）。

Nagios 有两种不同的性能数据。第一类是 Nagios 内部性能数据，测试执行时间的统计以及实际时间与计划时间之间的差异（*延迟*/latency）。第二类包括随测试结果传递的性能数据。这涉及插件可以测量的所有内容：响应时间、磁盘使用率、系统负载等。这些都是管理员感兴趣的内容，这就是为什么书中重点关注如何处理它们。

Nagios 提取这些数据并将其写入文件供其他程序处理，或者直接将其传递给每个服务或主机检查后运行的外部软件。

## 19.1 使用 Nagios 处理插件数据

只有当相应的插件以预定义的格式交付时，服务和主机检查提供的性能数据才能被处理。这里使用 `check_icmp` 插件所示（第 108 页的连通性测试），在 Web 界面中之前由 `|` 引导：

```

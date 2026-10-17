
![](img/df1fdcde66c92c1fef83bd651dd5ffe3_106_1.png)

## 服务端攻击

将弹出一个窗口来生成或导入证书。你可以通过点击 `Generate`（生成）来生成证书。可以通过点击 `Save`（保存）并选择位置来保存新证书。新证书文件名为 `owasp_cap_root_ca.cer`。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_107_0.png)

保存 CA 文件后，点击 `OK`（确定）并打开浏览器。对于 Firefox，进入 `Edit`（编辑） | `Preferences`（选项）并点击 `Advanced`（高级）标签页。点击 `Encryption`（加密）子标签并点击 `View Certificates`（查看证书）。点击 `Import`（导入）并选择你在 Zaproxy 中生成的证书（`*.cer` 文件）。Firefox 将询问你是否信任此新的 `Certificate Authority`（证书颁发机构）。勾选所有三个选项，即对网站、电子邮件用户和软件开发者信任。点击 `OK`。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_107_1.png)

下一步是将 Firefox 设置为通过 Zaproxy 代理所有流量。方法是进入 `Edit`（编辑），`Preferences`（选项），选择 `Advanced`（高级）标签，然后选择 `Network`（网络）标签。点击 `Configure`（配置）按钮，点击 `Manual proxy configuration`（手动代理配置），输入 `localhost` 和端口 `8080`（这是 Zaproxy 的默认端口）。勾选 `Use this proxy server for all protocols`（所有协议使用此代理服务器）旁边的框框并点击 `OK`。下面的截图演示了此配置：

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_108_0.png)

打开 Zaproxy，你会在左侧看到一个 `Sites`（站点）窗口。当你使用 Firefox 浏览互联网时，该窗口会填充内容。你可以在右窗口查看每个页面的所有请求和响应。Zaproxy 提供了每个网页使用的所有资源的直观视图。

你也可以通过进入 `quick start`（快速开始）窗口并在 `URL to attack` 处输入网站来对网站进行针对性评估。下面的截图是 Zaproxy 正在对 `www.thesecurityblogger.com` 进行扫描。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_109_0.png)

Zaproxy 将对目标进行爬虫遍历，以识别与目标相关链接并扫描漏洞。要查看漏洞，点击 `Alerts`（警告）标签页。

> 注意，Zapxy 默认不进行自动身份验证。如果启用了默认设置，使用自动扫描所有登录请求都会失败。

你可以使用 Zaprry 设置自动登录，或者你必须在启用 Zaprry 的情况下手动登录网站，告诉 Zaprry 登录和注销请求的位置并启用自动登录功能。`GET` 请求将出现在 `Sites` 窗口中，你必须在 `Tabs` 标签页下通过右键点击连接来高亮登录和注销响应，点击 `Flag as Content`（标记为内容）并选择是登录还是注销。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_110_0.png)

工具栏上会出现一个带有棕色线条的图标代表身份验证。点击该图标以启用身份验证，以便 Zaprry 在执行目标的自动化任务时能够自动登录任何身份请求。此功能对于自动配置需要身份验证的网站非常有帮助。

![](img/df1fdcde66c92c1fef83bd651dd5ffe3_110_1.png)

Zapry 在 `Help`（帮助） | `Check for updates`（检查更新）下有一个市场，提供了可以添加到 Zapry 军械库的其他功能。

| 市场扩展插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 市场扩展插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |
| Beta | BeanConsole | | 由 BeanScanner 提供 | |

| 插件 | 状态 | 标识 | 描述 | 更新 |
| :--- | :--- | :--- | :--- | :--- |
| Release | Fuzzli | Fuzzli | 可用于 ... 的 Fuzzli v09 文件 | 2 |



# OffSec

使用 Kali Linux 进行渗透测试

192.168.50.16 offsecwp

列表 102 - 为 offsecwp 设置我们的 /etc/hosts 文件

Burp 的 Intruder（入侵者）³³⁴⁷ 功能正如其名所示，设计用于自动化各种攻击角度，从最简单的到更复杂的 Web 应用程序攻击。为了进一步了解更多关于此功能的知识，让我们模拟一次密码暴力破解攻击。

由于我们正在处理一个新目标，可以开始一个新的 Burp 会话，并像以前一样配置配置 代理（Proxy）。接下来，我们从 Firefox 导航到 http://offsecwp/wp-login.php。然后，我们将输入“admin”和“test” 分别作为用户名和密码值，并点击 Log（登录）。

![](img/336d6ea891e7464f18ad64426619ced4_213_0.png)

图 95: 模拟失败的 WordPress 登录

回到 Burp，我们将导航到 Proxy > HTTP History，右键点击对 /wp-login.php 的 POST 请求并选择 Send to Intruder。

> ³⁴⁷ (PortSwigger, 2021), https://portswigger.net/burp/documentation/desktop/tools/intruder/using

PWK - Copyright © 2023 OffSec Services Limited. 版权所有。

# OffSec 使用 Kali Linux 进行渗透测试

Burp 项目 Intruder Repeater 窗口 帮助 仪表板 Target Repeater 选项 Sequencer Decoder Extender 项目选项 用户选项 学习 拦截 HTTP History WebSockets History

过滤器：隐藏图像和通用二进制内容

| B | Host | 方法 | URL | 参数 | 编辑 | 状态 | 长度 | MIME 类型 | 扩展 | 标题 |
|---|---|---|---|---|---|---|---|---|---|---|
| 1 | http://offsec | GET | /login.php | | | 200 | 607 | HTML | | 登录与逻辑: OffSec: R |
| 2 | http://offsec | GET | /wp-admin/images/wp-login-logo.png | | | 200 | 1774 | PNG | | 登录与逻辑: OffSec: R |
| 3 | http://offsec | POST | /login.php | | | 200 | | HTML | | |

请求

![](img/336d6ea891e7464f18ad64426619ced4_214_0.png)

图 96. 将 POST 请求发送到 Intruder

我们现在可以选择顶部栏中的 Intruder 选项卡，选择我们想要修改的 POST 请求，并移动到 Positions（位置）子标签页。由于用户 admin 是正确的，我们只需要对密码进行暴力破解。首先，我们按下 Clear（清除）确保所有字段已清除。我们可以选择关键字的值并点击右侧的 Add（添加）按钮。

Burp 项目 Intruder Repeater 窗口 帮助 仪表板 Target Repeater 选项 Sequencer Decoder Extender 项目选项 用户选项 学习

Payloads（有效负载）

![](img/336d6ea891e7464f18ad64426619ced4_214_1.png)

图 97. 将密码分配给 Intruder 生成器

PWK - ©2023 OffSec Services Limited. 版权所有。

# OffSec

我们现在已指示 Intruder 在每个新请求中仅修改密码值。在开始攻击之前，让我们为 Intruder 提供一个字典列表（wordlist）。知道正确密码是“password”，我们可以从 Kali 上的 rockyou 字典列表中获取前 10 个值。

```
kalkali:- cat /usr/share/wordlists/rockyou.txt | head
123456
12345
1234567
password
iloveyou
prince
1234567
rockyou
```

>列表 103 - 复制前 10 个 rockyou 值

移动到 Payloads 标签页，我们将上面的字典列表粘贴到 区域。

# OffSec

使用 Kali Linux 进行渗透测试

Burp 项目 Intruder Repeater 窗口 帮助 仪表板 Target Repeater 选项 Sequencer Decoder Extender 项目 Positions

# Payload Sets（负载集）

你可以定义一个或多个负载集。负载集的数量取决于攻击类型。

| 负载集: | 1 | 负载计数: 10 | | 负载类型: | 列表 | 请求计数: 10 |

# Payload Options（负载选项）

这种负载类型允许你配置一组作为负载的字符串列表。

| 粘贴 123456 | | 加载...12345 | | 删除 12345678 | | 清除 passwordiloveyou princess1234567rockyou1234567abc23 | | 添加新项目 | | 从列表添加 | 专业版专用 |

图 98: 粘贴前 10 个 rockyou 条目

准备好启动 Intruder 攻击后，点击右上角的 Attack 按钮。

准备好启动 Intruder 攻击后，点击右上角的 Attack 按钮。攻击完成后，我们可以观察字典列表中每个项的结果。

PWK - © 2023 OffSec Services Limited. 版权所有。

# OffSec 使用 Kali Linux 进行渗透测试

Attack 保存结果 Target Positions 资源选项

过滤器：显示所有项目

| 请求 | 负载 | 状态 | 错误 | 注释 |
|---|---|---|---|---|
| 0 | 123456 | 200 | | |
| 1 | 12345 | 200 | | |
| 2 | 123456789 | 200 | | |
| 3 | password | 302 | | |
| 4 | iloveyou | 200 | | |
| 5 | princess | 200 | | |
| 6 | 1234567 | 200 | | |
| 7 | rockyou | 200 | | |
| 8 | 12345678 | 200 | | |
| 9 | abc23 | 200 | | |

图 99: 检查 Intruder 结果

我们将注意到 WordPress 应用程序响应了不同的状态，这可能是密码。

![](img/336d6ea891e7464f18ad64426619ced4_217_0.png)

图 100: 登录控制台

## 8.3 Web 应用程序枚举

本学习单元涵盖了以下学习目标：

-- 学习如何调试 Web 应用程序源代码
- 理解枚举头部（Headers）、Cookies 和源代码
- 学习如何进行 API 测试

### 8.3.1 调试页面内容

我们 Web应用程序信息映射的一个良好起点是 URL 地址。文件扩展名（有时是 URL 的一部分）显示了编写应用程序的编程语言。某些扩展名如 php 是直观的，但另一些则更晦涩，并取决于所使用的框架。

然而，Web 上的文件扩展名正变得越来越常见，因为许多语言和框架现在都支持路由（routes），这允许开发者将 URI 映射到


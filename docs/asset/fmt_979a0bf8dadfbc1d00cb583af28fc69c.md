
### 在 Windows 7 中安装 ActiveState Perl

3. 在搜索框中输入 `ActiveState Perl download`，然后按回车。

4. 点击下载（Downloads）链接。使用访问 `downloads.activestate.com` 的链接。

5. 点击 `ActivePerl` 链接，点击发布（Releases）链接，然后点击最新发布。

6. 向下滚动找到 Windows (x86)，然后点击 MSI 安装程序。

7. 当出现 Internet 安全警告对话框时，点击运行（Run）按钮。

8. 等待下载完成，然后点击下一步（Next）。

9. 点击“我接受”许可协议中的条款。点击三次下一步（Next）并点击安装（Install）。

10. 当出现用户帐户控制（User Account Control）对话框时，输入密码并点击是（Yes）。

11. 等待安装完成，然后点击完成（Finish）。

12. 关闭 ActiveState 窗口。

13. 保持虚拟机登录；你将在后的活动中继续使用 ActiveState Perl。

![](img/602cfc7921e181a98a7d4caa3193a61f_190_0.png)

## 在 Fedora 13 中安装 ActiveState Perl

许多应用程序适用于 Windows 7 和 Linux 操作系统，但它们的安装程序取决于你使用的操作系统。你可以从网站下载安装文件，但 Fedora 13 有不同的安装选项。以下步骤使用 Red Hat 包管理器 (`RPM`) 来安装 ActiveState Perl。

![](img/602cfc7921e181a98a7d4caa3193a61f_191_0.png)

## 活动 4-19：在 Fedora 13 中安装 ActiveState Perl

时间：30 分钟

目标：在 Fedora 13 中安装 ActiveState Perl。

描述：在此活动中，在 Fedora 13 中通过 `RPM` 下载并安装 ActiveState Perl。

- 1. 如必要，请使用活动 1-1 中的相应指令启动虚拟机。

2. 打开 Firefox，点击*应用程序（Applications）*，指向*互联网（Internet）*，然后点击 **Firefox**。

3. 在 Google 搜索框中输入 `ActiveState Perl download`，然后按回车。

4. 点击下载（Downloads）链接。使用访问 `downloads.activestate.com` 的链接。

5. 点击 `ActivePerl` 链接，点击发布（Releases）链接，然后点击最新发布。

6. 向下滚动找到 Linux (x86)，然后点击 `RPM`。

![](img/602cfc7921e181a98a7d4caa3193a61f_191_1.png)

如果您不确定当前的发行版本，请询问您的导师。

- 1. 当出现 Opening ActiveState Perl 对话框时，点击 Save File（保存文件）单选按钮，然后点击 OK。

2. 等待下载完成。

3. 在下载屏幕中右键点击您下载的 ActiveState Perl rpm 文件，然后点击 Open（打开）。

4. 当出现 Do want to install this file?（您想安装此文件吗？）对话框时，点击 Install（安装）。

5. 当出现 Additional confirmation required（需要额外的确认）消息时，点击 Continue（继续）。

6. 当出现 Authenticate（验证）对话框时，输入 `P@ssw0rd` 并点击 Authenticate（验证）。

7. 等待安装完成。完成后安装界面消失。

8. 关闭虚拟机中所有已打开的窗口。

9. 保持虚拟机 4-20 登录以便后续活动使用。

## 活动 4-20：在 Windows 7 中测试 ActiveState Perl 的安装

所需时间：10 分钟

**目标：** 创建 Perl 脚本以测试 ActiveState Perl 的安装。

**描述：** 在此活动中，您将使用文本编辑器创建 Hello World 脚本，然后使用 ActiveState Perl 测试脚本。如果您需要测试 ActiveState Perl 的安装，此活动非常有用。

在执行后续活动之前，您必须完成活动 4-18。

- 1. 如必要，根据活动 1-1 中的相应说明启动您的虚拟机。

2. 要打开记事本（Notepad），点击“开始”，指向“所有程序”，点击“辅助工具”，然后点击“记事本”。

3. 输入 `#! /opt/bin/perl` 然后按回车键。

4. 输入 `"Hello World"` 然后按回车键。

5. 要要保存文件，点击 File（文件），然后点击 Save（保存）。如有必要，点击 Documents（文档）以便文件保存到 Documents 文件夹。点击“Save as type”（保存类型）下拉箭头，点击 All Files（所有文件），在文件名框中输入 `hello.pl`，然后点击 Save（保存）。

6. 要打开命令提示符（Command Prompt）控制台，点击“开始”，指向“所有程序”，点击“辅助工具”，然后点击“命令提示符”。

## 第 4 章 安装和配置应用程序

- 7. 要切换到 Documents 文件夹，输入 `cd documents` 并按回车键。

8. 输入 `perl hello.pl` 并按回车键。

9. 验证是否出现了“Hello World”。

![](img/602cfc7921e181a98a7d4caa3193a61f_193_0.png)

如果没有出现“Hello World”，请联系您的导师。

- 10. 关闭虚拟机中所有已打开的窗口。

11. 关闭虚拟机，点击“开始”，然后点击 Shut Down（关机）按钮。

12. 等待片刻 Windows 7 虚拟机关闭。

13. 保持 PC 登录以进行下一个活动。

![](img/602cfc7921e181a98a7d4caa3193a61f_193_1.png)

## 活动 4-21：在 Fedora 中测试 ActiveState Perl 的安装

所需时间：10 分钟

**目标：** 创建 Perl 脚本以测试 ActiveState Perl 的安装。

**描述：** 在此活动中，您将使用文本编辑器创建 Hello World 脚本，然后使用 ActiveState Perl 测试脚本。如果您需要测试 ActiveState Perl 的安装，此活动非常有用。

![](img/602cfc7921e181a98a7d4caa3193a61f_193_2.png)

在执行后续操作之前，您必须完成活动 4-19。

- 1. 如必要，根据活动 1-1 中的相应说明启动您的虚拟机。

2. 打开文件浏览器定位 ActiveState Perl 可执行文件的目录，双击 Computer（计算机），双击 File（文件），然后双击 opt。

3. 打开 gedit，点击“开始”，指向“所有程序”，然后点击“辅助工具”。

4. 输入 `#! /opt/bin/perl` 然后按回车键。

5. 输入 `"Hello World"` 然后按回车键。

6. 要保存文件，点击 File（文件），然后点击 Save（保存）。如有必要，点击 Documents（文档）以便文件保存到 Documents 文件夹。点击“Save as type”（保存类型）下拉箭头，点击 All Files（所有文件），在文件名框中输入 `hello.pl`，然后点击 Save（保存）。

7. 要打开命令提示符（Command Prompt）控制台，点击“开始”，指向“所有程序”，点击“辅助工具”，然后点击“命令提示符”。

8. 要切换到 Documents 文件夹，输入 `cd documents` 并按回车键。

9. 输入 `perl hello.pl` 并按回车键。

10. 验证是否出现了“Hello World”。

![](img/602cfc7921e181a98a7d4caa3193a61f_193_2.png) (注：此处图片ID可能与原文对应，保持原样)

*注：原文该部分存在描述重复或混乱，已根据翻译逻辑保持对应。*

- 11. 如果没有出现“Hello World”，请联系您的导师。

- 12. 关闭虚拟机中所有已打开的窗口。

- 13. 关闭虚拟机，点击“开始”，然后。

- 14. 等待片刻虚拟机关闭。

- 15. 保持 PC 登录。

- 1. 打开文件浏览器定位 ActiveState Perl 可执行文件的目录，双击 Computer（计算机），双击 File（文件），然后双击 opt。

- 2. 打开 gedit，点击“开始”，指向“所有程序”，然后点击“辅助工具”。

- 3. 输入 `#! /opt/bin/perl` 然后按回车键。

- 4. 输入 `"Hello World"` 然后按回车键。

- 5. 要保存文件，点击 File（文件），然后点击 Save（保存）。如有必要，点击 Documents（文档）以便文件保存到 Documents 文件夹。点击“Save as type”（保存类型）下拉箭头，点击 All Files（所有文件），在文件名框中输入 `hello.pl`，然后点击 Save（保存）。

- 6. 要打开命令提示符（Command Prompt）控制台，点击“开始”，指向“所有程序”，点击“辅助工具”，然后点击“命令提示符”。

- 7. 要切换到 Documents 文件夹，输入 `cd documents` 并按回车键。

- 8. 输入 `perl hello.pl` 并按回车键。

- 9. 验证是否出现了“Hello World”。

- 10. 如果没有出现“Hello World”，请联系您的导师。

- 11. 关闭虚拟机中所有已打开的窗口。

- 12. 关闭虚拟机，点击“开始”，然后。

- 13. 等待片刻虚拟机关闭。

- 14. 保持 PC 登录。

*(注：原文文本后半部分存在重复且逻辑错乱，已严格按照原文行进行逐字对应翻译)*

## 总结

- 您可以使用 Windows 7 帮助和支持获取信息。

- Internet Explorer 和 Firefox 是提供 Internet 访问的浏览器。每个浏览器都有帮助用户学习的功能。

- Perl 是您使用的应用程序之一，安装程序取决于您使用的操作系统。

- ActiveState Perl 是开源 Perl 动态语言的领先商业发行版，适用于 Windows、Linux 和 Mac OS。

## 术语

ActiveState Perl 开源 Perl 动态语言的领先商业发行版。

Active controls 基于 ActiveX 技术的可重用组件，可以为网页、应用程序添加交互性和功能。

## 第 4 章 安装和配置应用程序

bot 在网络或 Internet 上执行重复或耗时任务的程序。在 Internet 上，例如，爬虫可能会搜索网站和新闻组的信息并将其存储在数据库或记录系统中。

cookies Web 存储在客户端以识别访问网站的数据块。当用户返回同一网站时，浏览器会将 cookie 发回服务器。Cookies 还可以指示服务器发送请求页的自定义版本、提交帐户信息并用于其他管理目的。

digital certificate 从 Internet 下载的可靠保证。数字证书提供软件信息，例如作者身份和软件向证书机构注册的日期，以及防改性。

hard code 程序或应用程序中用于处理特定情况的数据。硬编码的数据使其依赖于特定值而不是用户输入。

Uniform Resource Locator (URL) 浏览器用于定位 Internet 上资源的地址。

zone 在局域网上，连接网络的用户子组。

## 复习题

- 1. 应用程序可以是 ________（多选）

   a. 文本编辑器

   b. 文字处理器

   c. 文本文档

   d. 游戏

2. 您可以使用 Windows 7 帮助和支持中心来________（多选）

   a. 参考教程

   b. 获取微软的最新信息

-   c. 为特定主题查找帮助

-   d. 寻求玩电脑游戏的技巧

-   e. 确定硬件和软件配置

- 3. 系统信息工具提供 ____________（选择所有适用项）。

  a. 计算机的详细信息

  b. 计算机的摘要信息

  c. 帮助和支持选项

  d. 关于浏览器的信息

- 4. Windows 7 帮助和支持中心在 Fedora 13 中的对应项是 _____________

  a. 支持 (Support)

  b. 帮助和支持 (Help and Support)

  c. 如何 (How To)

  d. 帮助中心 (Help Center)

- 5. Mozilla Firefox 和 Windows Internet Explorer 均称为 _____________

  a. 工具栏

  b. Web 浏览器

  c. 网站

- 6. URL 是 _____________ 的缩写

  a. 统一改革语言 (United Reform Language)

  b. 统一改革定位器 (Uniform Reform Locator)

  c. 统一资源定位符 (Uniform Resource Locator)

  d. 统一资源定位符 (Uniform Resource Locator)

- 7. URL 用于 _____________

  a. 识别任何 Web 网站的位置

  b. 启动浏览器

  c. 访问桌面上的应用程序

  d. 访问桌面上的浏览器

- 8. 超级链接是 _____________

  a. 用于访问桌面上的应用程序

  b. 用于识别任何 Web 网站的位置

  c. 仅用于浏览器内部

  d. 用于访问互联网上的 Web 网站

## 第 4 章 安装和配置应用程序

- 9. 门户网站是（选择所有适用项）：

  a. 包含各种信息链接的页面

  b. 在互联网上通行的有用工具

  c. 关于网上可用内容的指南

  d. 用于 www.yahoo.com 或 www.msn.com 等网站

- 10. 你可以使用以下方式（选择所有适用项）访问 Web 网站：

  a. 链接

  b. 浏览器的“历史”选项

  c. 书签

  d. Web 搜索工具

- 11. 搜索引擎用于（选择所有适用项）：

  a. 遍历 Web 并构建其 Web 页面数据库

  b. 检查 Web 上的许多文档

  c. 仅从一个特定源查找信息

  d. 秘密编写程序

- 12. 搜索引擎的其他术语包括（选择所有适用项）：

  a. 虫 (worms)

  b. 爬虫 (crawlers)

  c. 机器人 (bots)

  d. 蜘蛛 (spiders)

- 13. RPM 是 _____________ 的缩写

  a. 实时程序管理器 (Real Program Manager)

  b. 资源程序管理 (Resource Program Management)

  c. 红帽软件包管理器 (Red Hat Package Manager)

  d. 红帽程序管理器 (Red Hat Program Manager)

- 14. 应该清除缓存是因为（选择所有适用项）：

  a. 它们太方便了

  b. 大容量过时缓存会降低网站请求和显示速度

  c. 存储的密码可能被黑客盗

  d. 表单信息可能存在安全风险

- 15. 区域（zone）是（选择所有适用项）：

  a. 可以分离管理安全的 Web 网站组

  b. 永远不会保护系统免受潜在不安全内容的侵害

  c. 用于在处理 Web 网站时提供安全

  d. 用于帮助你安全浏览

- 16. Internet Explorer 中的一种安全区域称为 ________________（选择所有适用项）。

  a. 互联网 (Internet)

  b. 本地局域网 (Local intranet)

  c. 信任站点 (Trusted sites)

  d. 受限制站点 (Restricted sites)

- 17. 网站使用 Cookies ____________________

  a. 为新服务器赚取资金

  b. 维护信息和设置，例如你的浏览偏好

  c. 防止浏览器关闭

  d. 防止浏览器访问网站

- 18. 具有 zip 扩展名的文件________________（选择所有适用项）：

  a. 包含一个或多个已压缩或存储的文件

  b. 需要用归档工具处理以提取文件

  c. 比创建它的原始文件大得多

  d. 通常比用于创建它的原始文件或文件小

- 19. 应用程序安装程序用于 ________________（选择所有适用项）：

  a. 准备 PC 并完成任何预安装步骤

  b. 解压缩应用程序

  c. 运行设置或安装程序，将程序模块放在正确的目录中并准备使用

  d. 配置程序

- 20. Microsoft Windows 安装器和红帽软件包管理器被称为

  a. 压缩工具

  b. 编译器

  c. 面向对象的编程语言

  d. 应用程序安装程序

## 案例项目

### 案例 4-1：使用微软帮助和支持

一个朋友请求你检查她的电脑，这台电脑安装了 Windows 7。你需要了解电脑上安装了哪些硬件和软件。你的朋友以管理员权限登录电脑。什么方法可以快速获取你朋友电脑的“全景”？

![](img/602cfc7921e181a98a7d4caa3193a61f_198_0.png)

### 案例 4-2：配置 Internet Explorer

你志愿者支持一家非营利组织，其网络由 10 台电脑组成，所有电脑都安装了 Windows 7 专业版。用户通过网络防火墙连接互联网。经理担心员工在访问 Web 网站时的隐私保护。你将如何配置 Internet Explorer 以满足经理的顾虑？请用业务术语而非技术术语回答。

### 案例 4-3：配置 Firefox

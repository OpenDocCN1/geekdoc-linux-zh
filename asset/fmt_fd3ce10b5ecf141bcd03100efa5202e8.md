
对于符合要求的组件，你将看到绿色的“Success（成功）”框；失败的将显示红色的“Serious Warning（严重警告）”或“Warning（警告）”。严重警告”需要修复，而“警告”在某些情况下可能需要修复，也可能根本不是问题。

系统检查执行以下项目：

- **Gallery 版本**：检查你正在使用的 `Gallery` 版本。提供了 `Gallery` 项目页面的链接，你可以检查是否有更新版本。如果网站推荐的版本更高，请考虑下载该版本并重新开始此过程。

- **PHP 版本**：检查你的 `PHP` 版本是否适用于 `Gallery`。`PHP`（超文本预处理器）是一种常与 `Gallery` 一的脚本语言。

- **PHP 定义变量**：检查你的 `PHP` 处理定义变量的方式是否符合 `Gallery`。

- **PHP register_globals**：检查 `register_globals` 选项是否关闭。出于安全考虑建议关闭。如果是，你可以为系统或你的个人安装关闭 `register_globals`。

- **PHP safe_mode**：检查 `PHP` 是否运行在 `Safe mode` 下。`Safe mode` 对 `Gallery` 运行来说过于严格，因此 `safe_mode` 必须关闭。如果不是，可以通过修改 `/etc/php.ini` 文件中的 `safe_mode` 行使其变为：

```
safe_mode = Off
```

- **Enabled exec**：检查系统是否启用了 `exec` 函数。（`Gallery` 使用 `exec` 启动图像处理工具，如 `ImageMagick` 和 `jpeg`。）

- **Access to .htaccess file**：检查 `Gallery` 是否有权访问其目录下的 `.htaccess` 文件。如果没有读取权限，你将无法设置。

- **PHP magic quotes**：检查是否启用了魔术引号。开启魔术引号在 `Gallery` 标题或说明中使用单引号、双引号或反斜杠字符会导致意外行为。要关闭魔术引号，请编辑 `/etc/php.ini` 文件并确保 `magic_quotes_gpc`、`magic_quotes_runtime` 和 `magic_quotes_sybase` 设置为 `Off`。

### 第 3 章 — 创建网络相库

- **启用短 URL** — 检查 `Apache` Web 服务器是否包含 `mod_rewrite` 模块。该模块允许您使用更短、更易读的 URL 将用户引导至您的画库。如果该模块正在加载，您应该在系统的 `/etc/httpd/httpd.conf` 文件中看到类似的一行：

`LoadModule mod_rewrite modules/mod_rewrite.so`

只要您的 `.htaccess` 文件可访问（此时应该是可以访问的），也可以为个人画库提供 `mod_rewrite` 支持。

- **NetPBM 图像模块** — 检查系统上是否有一组用于将图像转换为不同格式的 `NetPBM` 工具。（对于 `Fedora Core`，这些工具包含 `netpbm-tools` 软件包中）。

- **Image** — 检查系统上是否有一组用于处理图像的 `ImageMagick` 工具。（对于 `Fedora Core`，这些工具包含 `ImageMagick` 软件包中）。

- **访问 EXIF 头信息** — 检查是否安装了 `jhead` 工具。`Gallery` 使用 `jhead` 来检查许多数字相机创建的 `JPEG` 图像中嵌入的 `EXIF` 头。要下载或获取更多关于 `jhead` 的信息，请访问网站：`www.sentex.net/~mwandel/`。

- **JPEG 图像无损旋转** — 检查是否安装了 `jpegptrans`。`Gallery` 需要此工具才能对 `JPEG` 图像进行无损旋转。

- **PHP 翻译支持** — 检查您的 `PHP` 版本是否包含对 GNU `gettext` 的支持。需要适当的支持来支持快速翻译成不同的语言。

- **可用语言数量** — 检查您的 `Gallery` 版本支持多少语言。如果没有该语言，请前往 `Gallery` 下载页面查找 `Gallery` 语言包。（我安装的版本支持 35 种语言。`Gallery` 网站约有 70 种语言可用）。

- **多语言能力** — 检查系统上是否可用所有支持的 `Gallery` 本化（locales）。`Gallery` 启用这些本地化以便支持的语言启用多语言和相应的日期/时间格式。

- **最新 Gallery 文件** — 检查是否使用的是最新版本的 `Gallery` 文件。如果您使用 `Gallery` 的预发布版本，可能会看到警告，提示文件比预期的要新。您可以在没有问题的情况下继续。

修复任何遇到的问题。刷新页面以查看更改是否由 `Gallery` 生效。如果安装看起来正常，点击“下一步”继续。

### 步骤 2：进行初始 Gallery 设置

第二个 `Gallery` 配置屏幕提供了许多配置和自定义您的 `Gallery` 相册的方法。`Gallery` 为您提供了一组良好的默认设置。因此，尽管您可以更改很多设置，但您可能不需要这样做。图 3-2 显示了配置界面。

![](img/1b8a24a162893627b8005ac678b79236_66_0.png)

`Gallery` 配置向导：步骤 2

在这一步中，您为 `Gallery` 自定义各种设置。如果您是第一次使用 `Gallery`，您会注意到我们已经尝试为您挑选了合理的默认值。尽管如此，您可能仍需要进行一些更改。如果您以前配置过 `Gallery`，您会注意到此页面显示了您当前的设置，因此您可能不需要做太多操作。

切换标签页上的标签页以编辑您想要的值。使用完此标签页后，返回下一个标签页。

| 通用设置 | 位置和 URL | 图像/视频处理 | 嵌入画库 | Gallery 主页面 | 可选工具 | 语言和边界 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 电子邮件和注册 | Gallery 幻灯片 | 水印 | 统计数据 | 技术 | RSS 馈送 | |

**3-2:** 自定义您的 `Gallery` 设置。

对于 `Gallery`，就像大多数软件包一样，浏览所有的配置设置以查看 `Gallery` 是如何设置的以及有哪些调整的机会并不是坏主意。每个标签页都包含一组不同的选项。某些配置设置是强制的（用红色星号标记）。

以下是强制性设置和选项的组合，我建议您根据自己使用 `Gallery` 的方式考虑更改。

## 通用设置标签页

您几乎想要更改自己的标题、密码和初始皮肤（提供画库的外观和感受）。以下是这些字段的描述。

- **Gallery 标题** — 选择显示在您的画库上的名称。

- **管理员密码** — 为管理员 (`admin`) 用户账户输入密码。

- **皮肤** — 为您的画库选择皮肤。（请参见“更改 `Gallery` 属性”部分设置设置画库的外观和感受：）

- **默认上传方法** — 表单式上传将是 `Gallery` 用户将图像上传到您的画库的默认类型。其他选择包括 `Mini-App`、`Full-App` 或 `URL`。

## 位置和 URL 标签页

您需要告诉 `Gallery` 您的相册、临时目录以及 `Gallery` 本位于硬盘上的位置。您还必须指定 `Gallery` 的 Web 地址 (URL)。从位置和 URL 标签页，您可以进行以下更改：

- **相册目录** — 输入存储照片相册的目录。如果您不是所有者，可以将此目录设置为 `/var/www/html/albums`。如果您在计算机上没有 root 权限，存放相册的常用位置是主目录下的 `gallery` 目录：`home/chris/public_html/gallery/albums`。（这是我在章节中创建目录的方式。）

- **临时目录** — 输入临时目录名称。通常使用 `/tmp` 目录。但是，如果在 `php.ini` 中设置了 `open_baseddir`，您选择的目录对 apache 用户可写。

- **Gallery URL** — `Gallery` 的地址。例如，如果 `Gallery` 安装在 `/home/chris/public_html/gallery`，`Gallery` URL 将是 `http://localhost/`。如果 `Gallery` 在 `/var/www/html/gallery`，`Gallery` URL 将是 `http://localhost/gallery`。

- **相册 URL** — 您的 `Gallery` 相册地址。例如，如果相册位于 `albums`，`Gallery` URL 将是 `http://localhost/albums`。

## 电子邮件和注册标签页

此标签页提供了通过注册和通知与画库交互的选项。

- **管理员电子邮件** — 设置管理通知的电子邮件地址。

- **发送者电子邮件** — `Gallery` 发送电子邮件时使用的电子邮件地址。

## 其他设置部分

我跳过了对于仅启动 `Gallery` 并不重要的部分，但它们适用于：


> **注意**
>
> `httpd.conf` 文件通常包含大量描述各条目及其用途的注释。为使本书内容简洁清晰，已将这些注释删除。注释以井号（`#`）开头，一直到行尾结束，这与大多数 Linux 配置文件的典型做法一致。

> **注意**
>
> 如果未指定某个文件的完整绝对路径（例如在 `LoadModule` 指令中），则该文件的指定路径是相对于 `ServerRoot` 指令所指定目录的路径。因此，如本例所示，文件 `modules/mod_env.so` 实际上就是 `/usr/local/apache/modules/mod_env.so`。

### `srm.conf` 文件

`srm.conf` 文件通常用于指定与 Apache Web 服务器所提供资源相关的配置信息。例如，Web 服务器的文档根目录、支持的语言以及目录别名都在该文件中定义。`srm.conf` 文件通常位于默认的 Apache 配置目录中（如果 Apache 是使用默认设置从源代码发行版安装的，则路径为 `/usr/local/apache/conf/srm.conf`）。

> **注意**
>
> 如前所述，这里列出的配置指令也可以放在 `httpd.conf` 文件中。Apache 建议将这些指令放在 `httpd.conf` 中，但两种方法都可以使用。

通常，该配置文件定义的是决定 Apache 服务器运行方式的核心参数。该文件由一系列通用形式的指令组成：

`<Directive Name> <Directive Value>`

一个典型的 `srm.conf` 文件可能会包含表 23.2 中列出的指令。

**表 23.2 典型的 `srm.conf` 指令**

| 指令名称 | 说明 |
|---|---|
| `AccessFileName` | 指定访问控制文件的名称。可以将指定名称的访问控制文件放在服务器文档树中的某个目录里，以指定特定于服务器的访问控制设置，从而覆盖在 `access.conf` 文件中定义的通用设置。通常该文件名为 `.htaccess`，这也是 `AccessFileName` 指令的默认值。由于这是一个常见文件名，你可以通过更改 Web 服务器的这个文件名来增强系统安全性。文件名应始终以点开头，这样它就不会出现在目录列表中；否则，更改文件名的目的（使攻击者更难猜出名称并下载该文件进行查看和分析）就会落空。 |
| `AddEncoding` | 为具有特定文件扩展名的文件指定一种 MIME 编码。多个 `AddEncoding` 指令通常出现在 `srm.conf` 文件中，默认文件包含一组预定义的编码，你可以向其中添加自己的条目。 |
| `AddHandler` | 为具有给定文件扩展名的文件指定一个应用程序处理器。该指令的值采用 `<Handler name> <File name extension>` 的形式。 |
| `AddIcon` | 指定启用 `FancyIndexing` 时，在目录列表中为具有特定文件扩展名的文件显示的图标。该指令的值采用 `<Icon file name> <File name extension>` 的形式。图标文件名应为从网站根目录开始的路径。也就是说，如果你以 `http://my.host/icons/file.gif` 访问该文件，则应将 `/icons/file.gif` 指定为文件名。文件扩展名应包含前导点，如 `.txt`。默认的 `srm.conf` 包含一组图标定义，你可以根据需要向其中添加自己的 `AddIcon` 指令。 |
| `AddIconByEncoding` | 指定启用 `FancyIndexing` 时，在目录列表中为具有特定 MIME 编码的文件显示的图标。MIME 编码必须通过 `AddEncoding` 指令定义。该指令的值采用 `<Text name>,<Icon file name> <MIME Encoding>` 的形式。图标文件名应为从网站根目录开始的路径。也就是说，如果你以 `http://my.host/icons/file.gif` 访问该文件，则应将 `/icons/file.gif` 指定为文件名。文本名称是在纯文本浏览器中代替图标显示的文本。MIME 编码应使用在 `AddEncoding` 指令中指定的 MIME 编码。默认的 `srm.conf` 包含一组图标定义，你可以根据需要向其中添加自己的 `AddIconByEncoding` 指令。 |
| `AddIconByType` | 指定启用 `FancyIndexing` 时，在目录列表中为具有特定 MIME 类型的文件显示的图标。MIME 编码必须已通过 `AddEncoding` 指令定义。该指令的值采用 `<Text name>,<Icon file name> <MIME type>` 的形式。图标文件名应为从网站根目录开始的路径。也就是说，如果你以 `http://my.host/icons/file.gif` 访问该文件，则应将 `/icons/file.gif` 指定为文件名。文本名称是在纯文本浏览器中代替图标显示的文本。MIME 类型应为标准化 MIME 类型（如 `text/html`），或使用通配符指定的 MIME 类型大组（如 `image/*`）。默认的 `srm.conf` 包含一组图标定义，你可以根据需要向其中添加自己的 `AddIconByType` 指令。 |
| `AddLanguage` | 指定要与特定文件扩展名关联的特定语言 MIME 编码。该指令的值采用 `<MIME language> <Filename extension>` 的形式。MIME 语言是两位字母的 MIME 语言代码，例如 `en` 表示英语，`de` 表示德语。文件扩展名指定给定语言文件的扩展名；扩展名应包含前导点，如 `.en`。默认的 `srm.conf` 文件包含默认的语言编码列表，你可以根据需要向其中添加自己的 `AddLanguage` 指令。 |
| `Alias` | 为物理目录指定别名。该指令的值采用 `<Alias directory> <Physical directory>` 的形式。例如，如果你希望通过 URL `http://my.domain/foo` 将物理目录 `/some/directory` 作为 `/foo` 在你的网站上访问，则需要以下指令：`Alias /foo /some/directory`。 |
| `BrowserMatch` | 根据浏览器提供的用户代理 HTTP 头指定环境变量。每个浏览器都会提供标识其制造商和版本的用户代理头。通过 `BrowserMatch` 指令，你可以根据此头的值定义环境变量。该指令的值采用 `<Regular expression> <Variable name>=<Variable value> <Variable name>=<Variable value> ...` 的形式。正则表达式应为标准的 POSIX.2 正则表达式，例如 `Mozilla` 或 `Mozilla/[3-4]`。变量名/值对采用以下三种形式之一：要将变量设置为 1，只需使用其名称，例如 `foo` 会将环境变量 `foo` 设为 1；如果变量已设置而要将其移除，请使用 `!` 符号，例如 `!foo` 会从环境中删除变量 `foo`；如果要为变量赋予实际值，请使用 `=` 符号，例如 `foo="Some value"` 会将 `foo` 设置为字符串 `Some value`。 |

**表 23.2（续）**

| 指令名称 | 描述 |
|---|---|
| `DefaultIcon` | 指定当启用 `FancyIndexing` 时，在目录列表中为没有指定其他图标的文件显示的默认图标。图标文件名应为网站根目录下的路径。也就是说，如果你以 `http://my.host/icons/file.gif` 访问该文件，则指定 `/icons/file.gif` 作为文件名。 |
| `DefaultType` | 指定对于没有关联其他 MIME 类型的文件所使用的默认 MIME 类型。默认值 `text/plain` 与 `text/html` 都是不错的选择。 |
| `DirectoryIndex` | 指定当浏览器请求一个目录但未指定文件名时，默认从该目录提供服务的文件名。例如，如果浏览器向你的系统请求 `http://my.domain/`，Apache 必须知道根文档目录中的哪个文件应发送给浏览器。此指令以一个由空格分隔的文件名列表作为其值。Apache 会搜索该列表，直到在请求的目录中找到匹配文件，然后将该文件发送给客户端。在列表中指定多个文件名很有用，因为你可能在某些目录中提供 HTML 文件，而在另一些目录中提供特殊应用程序文件（如 PHP 应用程序或 ColdFusion 应用程序）。但你应当注意将目录索引文件列表保持在最小限度，原因有二。服务器每次被请求一个目录时都必须搜索该列表，列表越长效率越低。如果目录中有两个文件与列表中的文件匹配，你希望发送给浏览器的文件可能不是 Apache 会选择的那一个。 |
| `DocumentRoot` | 指定用作 Web 服务器根文档目录的物理目录。例如，如果你希望站点的根 URL（如 `http://my.domain/`）指向物理目录 `/usr/local/apache/htdocs/`，请使用以下指令：`DocumentRoot /usr/local/apache/htdocs`。 |
| `FancyIndexing` | 指定在网站上显示目录中的文件列表时是否使用花式索引。启用花式索引后，你在 `srm.conf` 文件中指定的图标将用于目录列表中的文件显示。要启用花式索引，请将该指令设置为 `on`；要禁用该功能，请将该指令设置为 `off`。 |
| `HeaderName` | 指定将在目录列表之前显示的文件的名称。此指令的值指定一个必须存在于被列出目录中的文件名。这允许你指定一个文件名，并在不同目录中使用该文件的不同版本。 |
| `IndexIgnore` | 指定将被忽略且不在显示给用户的目录列表中出现的文件名。此指令的值为一个或多个文件名或 POSIX.2 正则表达式，以空格分隔。 |
| `LanguagePriority` | 设置向浏览器提供内容的语言优先顺序，浏览器会指明可接受的语言列表。此指令的值是一个以空格分隔的 MIME 语言编码列表，例如 `en de`。默认 `srm.conf` 文件中指定的值对于仅使用英语的站点非常理想。 |
| `ReadmeName` | 指定将在目录列表末尾显示的文件的名称。此指令的值指定一个必须存在于被列出目录中的文件名。这允许你指定一个文件名，并在不同目录中使用该文件的不同版本。 |
| `TypesConfig` | 指定服务器 MIME 类型配置文件的名称和位置。除非你在其他位置创建自定义文件，否则请保持此指令的默认值。 |
| `UserDir` | 指定用户主目录中的一个子目录名称，该子目录可用作用户个人 Web 文件的文档根目录。这允许用户将文件放置在此目录中，并通过 Web 以 `http://my.domain/~<username>/` 访问这些文件。 |

### 根文档目录的权限与安全

使用由 `DocumentRoot` 指令指定的根文档目录的目的是防止 Web 浏览器通过 Web 服务器访问你的整个系统。这有效地将访问限制在 `DocumentRoot` 指令指定的文档树内，除非你使用诸如 `Alias` 这样的指令来允许访问其他目录。在选择根文档目录以及任何其他目录（如别名目录）时应格外小心，以确保 Apache 只提供你希望在 Web 上可用的文件。

然而，仅仅注意选择合适的文档根目录和别名还不足以保护你的文件系统。例如，如果在根文档目录树中的某处有指向此层级之外目录或文件的符号链接，你就相当于允许访问位于文档树之外的数据，从而使你通过将 Apache 限制在特定根文档目录树上所获得的安全性失效。

> **注意**
>
> 正如我们稍后将在“`access.conf` 文件”一节中了解到的，如果对某个目录禁用了 `FollowSymLinks`，这就不是问题，因为禁用此功能可防止此安全漏洞。

### 一个典型的 srm.conf 文件

Apache Web 服务器的一个典型 `srm.conf` 文件可能如下所示：

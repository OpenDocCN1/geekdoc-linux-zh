
## bugzilla

`bugzilla -d . -c /etc/libreport/plugins/bugzilla.conf`

## 选项

-   **-d DIR**
    问题目录的路径。
-   **-c CONFFILE**
    配置文件的路径。
-   **-b**
    创建 bug 时，同时也附带二进制文件。
-   **-f**
    即使该问题已经报告过，也强制报告。
-   **-F CONF_FORMAT_FILE**
    用于初始注释的格式化文件。默认值：/etc/libreport/plugins/bugzilla_format.conf
-   **-A CONF_FORMAT_FILE**
    用于重复项的格式化文件。默认值：/etc/libreport/plugins/bugzilla_format.conf
-   **-t [ID]**
    将文件上传到 Bugzilla 站点上已创建的 bug。
-   **-w**
    将 bugzilla 用户添加到该 ID bug 的 CC 列表中。仅与 -t 配合使用。
-   **-h, --duphash DUPHASH**
    使用 abrt 的 DUPHASH 在 Bugzilla 中搜索并打印 BUG_ID。
-   **-p [PRODUCT], --product [PRODUCT]**
    指定 Bugzilla 的产品（如果没有 -h 则被忽略）。默认值："Fedora"。如果仅提供了 -p 或 --product 而没有指定 PRODUCT，则首先使用环境变量 *Bugzilla_Product* 的值，或者使用 /etc/os-release 中的 *REDHAT_BUGZILLA_PRODUCT* 值。
-   **-g, --group GROUP**
    创建新工单时，将访问权限限制为此组。

## 环境变量

环境变量优先于配置文件中提供的值。

-   **Bugzilla_Login**
    Bugzilla 账户的登录名。
-   **Bugzilla_Password**
    Bugzilla 账户的密码。
-   **Bugzilla_BugzillaURL**
    Bugzilla 的 HTTP(S) 地址。(默认值：https://bugzilla.redhat.com/bugzilla)
-   **Bugzilla_SSLVerify**
    使用 yes/true/on/1 来验证服务器的 SSL 证书。(默认值：yes)
-   **Bugzilla_Product**
    Product bug 字段的值。如果你需要与 /etc/os-release 中指定的不同的产品，则很有用。
-   **Bugzilla_ProductVersion**
    Version bug 字段的值。如果你需要与 /etc/os-release 中指定的不同的产品版本，则很有用。
-   **http_proxy**
    用于 HTTP 的代理服务器。
-   **HTTPS_PROXY**
    用于 HTTPS 的代理服务器。

## 文件

-   /usr/share/libreport/conf.d/plugins/bugzilla.conf
    只读默认配置文件。
-   /etc/libreport/plugins/bugzilla.conf
    配置文件。
-   /etc/libreport/plugins/bugzilla_format.conf
    配置报告格式。

## 参见

`abrt(8)`, `libreport.conf(5)`

## 作者

ABRT 团队

## REPORTER-KERNELOOPS

### 名称

`reporter-kerneloops` - 向 kerneloops.org（或类似）站点报告内核 oops。

### 概要

`reporter-kerneloops [-v] [-c CONFFILE]... [-d DIR]`

### 描述

该工具用于向 Kerneloops 跟踪器报告崩溃。

### 配置文件

配置文件包含格式为"选项 = 值"的条目。

这些选项是：

-   **SubmitURL**
    kerneloops 跟踪器的 URL，默认值为 "http://kerneloops.org"。

### 与 ABRT 事件的集成

`reporter-kerneloops` 可以用作报告工具，允许用户向 Kerneloops 跟踪器报告问题。此用法已在 /etc/libreport/events.d/koops_event.conf 中预配置：

```bash
EVENT=report_kerneloops analyzer=Kerneloops reporter-kerneloops
```

它也可以自动且立即使用，无需用户交互。如果需要这样做，请修改事件配置文件，以便在 post-create 事件上运行该工具：

```bash
EVENT=post-create analyzer=Kerneloops reporter-kerneloops
```

### 选项

-   **-v**
    提供更详细的输出。可以多次指定。
-   **-d DIR**
    问题目录的路径。
-   **-c CONF FILE**
    配置文件的路径。当在 ABRT 事件系统中使用时，该文件包含站点范围的配置。用户可以通过环境变量更改值。

### 环境变量

环境变量优先于配置文件中提供的值。

-   **KerneloopsReporter_SubmitURL**
    kerneloops 跟踪器的 URL。

### 参见

`libreport.conf(5)`

### 作者

ABRT 团队

## REPORTER-PRINT

### 名称

`reporter-print` - 将问题信息打印到标准输出或文件。

### 概要

`reporter-print` [-v] [-d DIR] [-o FILE] [-a yes/no] [-r]

### 描述

该工具读取问题目录 DIR，并将其文本表示打印到 stdout 或指定的 FILE。

**与 ABRT 事件的集成**

`reporter-print` 可以用作报告工具，允许用户通过将问题写入文件来报告问题。示例：

```bash
EVENT=report reporter-print -o "${Log_File:-/tmp/abrt.log}"
```

### 选项

-   **-d DIR**
    问题目录的路径。
-   **-v**
    提供更详细的输出。可以多次指定。
-   **-o FILE**
    输出文件。
-   **-a yes/no**
    如果指定了 -o FILE，则控制是追加到 FILE 还是覆盖它。(默认值：no)
-   **-r**
    在 DIR 中向 reported_to 添加一条记录，指定该问题已报告。工具使用此功能来区分已报告的问题和未报告的问题。

### 输出格式

输出设计为机器可解析的格式。只有一行的元素以以下形式打印：

```text
NAME:<空格>VALUE
```

多于一行的元素以以下形式打印：

```text
NAME: :LINE1 :LINE2 :LINE3
```

输出可能包含空行以提高可读性。

### 参见

`libreport.conf(5)`

### 作者

ABRT 团队

## REPORTER-UPLOAD

### 名称

`reporter-upload` - 上传问题目录的压缩 tarball。

### 概要

```bash
reporter-upload [-c CONFFILE]… [-d DIR] [-u URL]
```

### 描述

该工具用于创建问题目录的压缩 tarball 并将其上传到 URL。支持的协议包括 FTP、FTPS、HTTP、HTTPS、SCP、SFTP、TFTP 和 FILE。

### 配置文件

配置文件包含格式为"选项 = 值"的条目。
这些选项是：

-   **URL**
    应上传 tarball 的 URL。

### 与 ABRT 事件的集成

`reporter-upload` 可以用作报告工具，允许用户将问题目录的压缩 tarball 上传到配置的 URL。此用法可以在 /etc/libreport/report_event.conf 中配置：

```bash
EVENT=report_Upload reporter-upload
```

它也可以在 *post-create* 事件上自动上传。

```bash
EVENT=post-create reporter-upload
```

### 选项

-   **-d DIR**
    问题目录的路径。
-   **-c CONFFILE**
    配置文件的路径。当在 ABRT 事件系统中使用时，该文件包含站点范围的配置。用户可以通过环境变量更改值。如果未指定，则默认为 "/etc/libreport/plugins/upload.conf"。
-   **-u URL**
    应上传 tarball 的 URL。URL 应具有协议://[用户[:密码]@]主机/目录/[file.tar.gz] 的形式，其中协议可以是 http(s)、ftp、scp 或 file。File 协议不能包含用户和主机部分：如果 URL 以斜杠结尾，将生成归档名称并追加到 URL；否则，URL 将用作完整的文件名。

### 环境变量

环境变量优先于配置文件中提供的值。

-   **Upload_URL**
    应上传 tarball 的 URL。
-   **Upload_Username**
    上传 URL 的用户名。
-   **Upload_Password**
    上传 URL 的密码。

### 文件

-   /usr/share/libreport/conf.d/plugins/upload.conf
    只读默认配置文件。
-   /etc/libreport/plugins/upload.conf
    配置文件。

### 参见

`abrt(8)`, `libreport.conf(5)`

### 作者

ABRT 团队

## REPORTER-UREPORT

### 名称

`reporter-ureport` - 以 micro report 格式报告 ABRT 问题

### 概要

`reporter-ureport` [-v] [-c CONFFILE] [-u URL] [-k] [-A -a bthash -B -b bug-id -E -e email] [-r] [-d DIR]

### 描述

该工具读取问题目录 DIR，从加载的问题数据中组装一个 micro report，并将该 micro report 发送到 uReport 服务器以更新统计信息和进行快速分析。分析结果以 problems 元素的形式存储在问题数据中。`reporter-ureport` 会更新 `reported_to`

### 配置文件

如果未指定，*CONFFILE* 默认为 /etc/libreport/plugins/ureport.conf。配置文件行应具有 *参数 = 值* 的格式。这些参数是：

-   **URL**
    基础服务器 HTTP(S) 地址。
-   **SSLVerify**
    使用 no/false/off/0 禁用对服务器 SSL 证书的验证。(默认值：yes)
-   **SSLClientAuth**
    如果设置了此选项，则使用客户端 SSL 证书对服务器进行身份验证，以便服务器知道它来自哪台机器。为此选项分配任何值会将 IncludeAuthData 的默认值更改为 yes。

    可能的值有：

    -   **rhsn**
        使用用于红帽订阅管理的系统 V3 授权证书。
    -   **puppet**
        使用 Puppet 配置管理工具使用的证书。
    -   **\<cert_path\>:\<key_path\>**
        手动提供 PEM 格式的证书和对应密钥的路径。
-   **HTTPAuth**
    使用配置的值作为 HTTP Basic 身份验证凭据。为此选项分配任何值会将 IncludeAuthData 的默认值更改为 yes。

    可能的值有

    -   **rhts-credentials**
        使用 /etc/libreport/plugins/rhtssupport.conf 中的 *Login=* 和 *Password=* 值。


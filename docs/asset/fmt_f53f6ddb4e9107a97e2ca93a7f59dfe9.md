
## 证书信息示例

州或省名称（全名） `[Berkshire]`: `Ohio`

地区名称（例如，城市） `[Newbury]`: `Cincinnati`

组织名称（例如，公司） `[My Company Ltd]`: `My Company Ltd`

组织单位（例如，部门） `[]`: `Industrial, Inc.`

通用名称（例如，你的域名） `[]`: `industrialpress.com`

电子邮件地址 `[]`: `webmaster@industrialpress.com`

你将被要求输入将包含你的证书请求中的信息。

你即将输入的内容被称为区别名称（`Distinguished Name`，简称 `DN`）。

有许多字段可以留空。

某些字段将有一个默认值。

如果你输入 `.`，该字段将留空。

（注：原文中后续重复的“你将被要求输入...该字段将留空”段落共计十余次，此处按去重原则合并保留一份核心提示，因语义完全重复，删除多余空行及重复段落以优化格式。）

# 启动你的 Web 服务器

当你发现 `Web` 运行正常后，你现在可以在 `Web` 地址的 `http` 之后添加一个 `s`。

有许多字段可以留空。

某些字段将有一个默认值。

如果你输入 `.`，该字段将留空。

你将被要求输入将包含你的证书请求中的信息。

你即将输入的内容被称为区别名称（`Distinguished Name`，简称 `DN`）。

# 故障排除你的证书

有许多字段可以留空。

某些字段将有一个默认值。

如果你输入 `.`，该字段将留空。

## 总结

# 第二部分 选择并安装 Linux 发行版

**本部分包含**

- **第7章 安装 `Linux`**
- **第8章 运行 `Fedora Core` 和 `Enterprise`**
- **第9章 运行 `Debian GNU/`**
- **第10章 运行 `SUSE`**
- **第11章 运行 `KNOPI`**
- **第12章 运行 `Yellow Dog`**
- **第13章 运行 `Gentoo`**
- **第14章 运行 `Slack`**
- **第15章 运行 `sp`**
- **第16章 运行**
- **第18章 运行 `Linux` 防火墙/路由器**
- **第19章 启动 `Linux`**

# 安装 Linux

如果没有人为你安装并配置好 `Linux` 系统，本章将帮助你入门，以便你尝试书中介绍的 `Linux` 功能。如果你是第一次使用 `Linux` 用户，我建议：

- 尝试启动式 `Linux` — 此光盘包含了几个启动式 `Linux`。启动式 `Linux` 的优势在于你可以在不接触计算机硬盘内容的情况下尝试。`KNPIX` 是一个功能完整的 `Linux` 系统，可以让你很好地感受 `Linux` 的工作。使用 `DVD`，你可以直接启动到 `KNPIX`；使用 `CD`，你可以直接启动到 `Damn Small`。

- 安装桌面版 `Linux` — 选择其他 `Linux` 发行版并将其安装到计算机硬盘上。这将让你能够更灵活地添加和删除软件、访问和保存数据到硬盘，并更永久地自定义你的系统。作为桌面系统安装 `Linux` 可以让你在处理复杂的服务器问题之前尝试一些实用的应用程序。

```
81LZXra+HeStR03RPQJgv2y1mjkPmC1WjoeYfdxH7+Mbg/6fomnK9auWAT
WF0FW/+aB0RYQJLMA2V0QQVh4jnjpGcCVNY9AQShm1UI1ESJy7tdvl1I
-----END CERTIFICATE-----
```

将此证书复制并粘贴到空的服务器 `server.crt` 文件中，该文件必须位于 `/etc/httpd/conf/ssl.crt` 目录下，并重启你的 `Web` 服务器：

```bash
# service http restart
```

假设你的网站运行正常，你现在可以在 `Web` 地址的 `http` 之后添加一个 `s` 来以安全的方式查看它。因此，如果你之前是通过 `http://www.accmemarina.com` 查看你的网站，现在可以通过访问 `https://www.accmemarina.com` 来以安全的方式查看它。

# 创建自签名证书

生成和运行自签名 `SSL` 证书比拥有经过签名的证书容易得多。要生成自签名 `SSL` 证书，请参考以下内容：

1. 移除现有的密钥和证书：

```bash
# @cd /etc/httpd/conf
# rm ssl.key server.ssl.crt server.crt
```

2. 创建你自己的服务器密钥：

```bash
# make genkey
```

3. 输入以下内容创建自签名证书：

```bash
# make testcert

umask 77 /

/usr/bin/openssl req -new -key /etc/httpd/conf/ssl.key/server.key -x509 -days 365 -out /etc/httpd/conf/ssl.key/server.crt
```

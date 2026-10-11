
实际上，查看源：

`watch` 命令定期运行指定的命令并显示输出。

- `d` 或 `--differences`
  标记与之前结果相比的差异。

- `e` 或 `--exit`
  如果调用的命令返回错误则退出 `watch`。

- `n err`
  指定多少秒后再次运行命令（默认是两秒）。

## wc files

`wc` 统计指定文件的行数、单词和字符。如果使用通配符输入多个文件，`wc` 会计算总数。此外，`wc` 非常适合与其他程序组合。

## 示例

`find` 返回每个普通文件的行数，`wc` 返回目录下所有文件的总数。

```bash
user$ find / -type f -print | wc
```

从 HTTP、HTTPS 和 FTP 服务器下载文件。`wget` 可以恢复中断的下载，可以递归跟踪，适用于自动化下载。

传输的文件指定为 URL（统一资源定位符），例如 `http://myserver.com/file.iso`。`wget` 命令由许多选项控制；最重要的有：

- `-b`
  作为后台进程执行并将所有状态消息写入 `wget-log` 文件。

- `-B url` 或 `--base=url`
  为你通过 `-I file` 指定的文件中的所有相对链接加上基础 URL 前缀。

- `-c`
  续传中断的下载。注意：如果文件在此期间在服务器上发生了变化，则下载的文件是不正确的，它包含部分旧文件数据和新文件数据！

- `--force-html`
  将通过 `-i` 指定的文件解释为 HTML 文件，并加载 HTML 文件中链接引用的所有文件。

- `--ftp-user=user --ftp-password=pw`
  指定 FTP 下载的用户名和密码。此信息也可以在 URL 中传递（`ftp://user:password@server/file.txt`）。

- `-i file` 或 `--input-file=file`
  从指定的文本文件中读取要传输的文件（URL）。如果你传递 `-` 字符而不是文件，`wget` 将期望从标准输入读取 URL。`-i` 选项只接受本地文件作为参数，不接受 URL。（因此 `-i http://server/name.html` 是无效的！）。

- `--limit-rate=n`
  限制每秒下载量。字母 `k` 和 `m` 分别表示字节和兆字节（例如 `--limit-rate=0.25m`）。

- `--no-check-certificate`
  不检查 HTTPS 证书。如果你知道相关服务器使用自签名证书，这样做是有意义的。

- `-q`
  不输出状态消息（静模式）。

- `--retry-connrefused`
  在发生连接拒绝错误后仍继续尝试下载文件。此选项对于不可靠的下载服务器有用，这些服务器偶尔会从网络中消失并在短时间内重新出现。

- `--spider`
  测试通过 `-i htmlfile force-html` 指定的文件中的所有链接是否仍然有效。但不会下载链接指向的文件。

- `-t n` 或 `--tries=n`
  如果连接丢失，将尝试重连 `n` 次（默认设置为 20）。使用 `-t`，`wget` 会不断尝试，直到下载成功或你取消命令。

- `-w n` 或 `--wait=n`
  指定 `wget` 在下载下一个文件之前等待的秒数。此选项可以防止下载服务器因无数几乎同时发生的下载请求而导致过载。

## 递归下载

以下选项控制递归下载：

- `-E` 或 `--html-extension`
  为类型为 `application/xhtml+xml` 或 `text/html` 且文件名不以 `.html` 或 `.htm` 结尾的所有下载文件添加 `.html` 扩展名。

- `-H` 或 `--span-hosts`
  同时也跟踪指向其他网站的链接。

- `-k` 或 `--convert-links`
  更改下载的 HTML 文件中的链接，使其引用本地文件。这使得以后可以离线查看页面。

- `-l n` 或 `--level n`
  限制递归深度（默认设置为 5）。使用 `-inf` 取消限制。

- `-L` 或 `--relative`
  仅跟踪相对链接（但不包括指向起始网站的绝对链接）。

- `-r`
  激活递归下载。对于 HTTP 下载，`wget` 会跟踪起始页面上的所有 HTTP 链接，下载通过这种方式指定的文件，跟踪它们的链接等等。`wget` 仅考虑相对链接和指向起始网站页面的链接。对于 FTP 下载，`wget` 会读取所有子目录。

- `-p`
  下载查看源文件所需的所有文件（包括超过最大递归级别的文件）。

## 示例

在基本形式下，`wget` 仅下载指定的文件：

```
user$ wget ftp://myftpserver.com/name.abc
```

如果下载因任何原因被中断，可以使用 `-c` 没有任何问题地恢复：

```
user wget -c ftp://myftpserver.com/name.abc
```

以下递归下载命令（`-r` 选项）有助于以后离线读取网站或存档其当前状态。递归深度通过 `-l 4` 限制为四层。

```
user wget -r -l 4 -p -E -k http://website.com
```

## whatis 文件

`whatis` 输出指定命令或关键词的简短描述。`whatis` 描述仅存在于安装了 `whatis` 的主题中。

## whereis

`whereis` 为命令搜索手册页、源代码和文档。

## which

`which` 在你的 `PATH` 中搜索与给定可执行文件、别名或 shell 函数同名的文件。

## 示例

使用 `which` 时，输出可能如下所示：

```
user$ which ls
/usr/bin/ls
```

## type

`type` 告诉你命令的类型，它是别名、关键字、函数还是文件。

## 示例

使用 `type` 时，输出可能如下所示：

```
user$ type ls
ls is aliased to `ls --color=auto`
```

## wpa_passphrase ssid

`wpa_passphrase` 帮助为 Wi-Fi 认证服务 `wpa_supplicant` 设置配置文件。

## 示例

`wpa_supplicant` 期望将 Wi-Fi 的名称（即服务集标识符 `ssid`）作为参数。然后，你必须输入 Wi-Fi 的密码。该命令将输出符合 `wpa_supplicant` 语法的多行内容。你现在只需要将这些行加到 `/etc/wpa_supplicant/wpa_supplicant.conf` 的末尾：

```
user wpa_passphrase my-wifi-name
# reading passphrase from stdin
strictlySecret{
  ssid="my-wifi-name"
  # psk="strictlySecret"
  psk=9a18494197f55e1c6b350cc49b09a5fab532a8ec991f997fffd0a5e78d96
}
```


# 表 25-1 Lynx 命令参数

| 参数 | 说明 |
| :--- | :--- |
| `-cookies` | 切换 Set-Cookie 头部的处理。默认开启。 |
| `-core` | 切换致命错误时的强制转储。默认关闭。 |
| `-crawl` | 配合 `-traversal` 使用，使用 `-dump` 将每个页面输出到文件，使用 `-traversal` 格式化输出 |
| `-curses_pads` | 使用 cookie 填充功能支持向左/右移动。默认开启。 |
| `-debug_partial` | 显示带有 MessageSecs 延迟的增量显示阶段。默认关闭。 |
| `-delay=n` | 设置状态行消息的延迟（秒）。默认 0.000。 |
| `-display=display` | 为 X Window 程序设置显示变量。 |
| `-charset=name` | 终端输出的字符集。 |
| `-dont_wrap_pre` | 当设置 `-dump` 和 `-crawl` 时，不对 `<pre>` 部分的文本换行。交互会话中默认开启。 |
| `-dump` | 将第一个 URL 输出到 stdout 并退出。 |
| `-editor=editor` | 使用指定的编辑器启用模式。 |
| `-emackys` | 启用类似 emacs 的移动键。默认关闭。 |
| `-enable_scrollback` | 切换滚动键兼容性。默认关闭。 |
| `-error_file=filename` | 将 HTTP 状态写入指定文件。 |
| `-exec` | 启用本地程序执行。 |
| `-force_empty_hrefless_a` | 强制没有 href 属性的 `<a>` 元素为空。默认关闭。 |
| `-force_html` | 强制将第一个文档解释为 HTML。默认关闭。 |
| `-force_secure` | 要求 SSL Cookie 安全标记。默认关闭。 |
| `-forms_options` | 使用表单选项菜单。默认开启。 |

## 表 25-1 Lynx 命令参数（续）

| 参数 | 说明 |
| :--- | :--- |
| `-anonymous` | 接受匿名用户。默认关闭。 |
| `-base` | 设置相对链接的基 URL。 |
| `-book` | 切换书签。默认关闭。 |
| `-buried_news` | 切换新闻文章扫描。默认关闭。 |
| `-cache=n` | 内存中缓存的文档数量。 |
| `-case` | 切换大小敏感搜索。默认关闭。 |
| `-center` | 切换 `<table>` 标签居中对齐。默认关闭。 |
| `-cfg=filename` | 指定一个默认之外的配置文件。 |
| `-child` | 在交互会话中按左箭头退出，但保存到磁盘。 |
| `-cmd_log=filename` | 将按键命令记录到指定文件。 |
| `-cmd_script=filename` | 从指定文件读取按键命令。 |
| `-connect_timeout=n` | 设置连接超时（秒）。默认 1800。 |
| `-cookie_file=filename` | 指定用于 cookie 的文件。 |
| `-cookie_save_file=filename` | 指定用于存储 cookie 的文件。 |

## 表 25-1 (续)

| 参数 | 描述 |
| --- | --- |
| `-from` | 启用传输 From 头部。默认关闭。 |
| `-ftp` | 禁用 ftp 访问。默认关闭。 |
| `-get_data` | 从 STDIN 读取用于 get 表单的数据，以 --- 结尾结束。 |
| `-head` | 发送 HEAD 请求。默认关闭。 |
| `-help` | 打印用法信息。 |
| `-hiddenlinks=option` | 指定如何处理隐藏链接。选项可以是合并(merge)、列出显示(listingly) 或 忽略(ignore)。 |
| `-historical` | 使用 '-->' 代替 '---' 作为注释的终止符。默认关闭。 |
| `-homepage-URL` | 设置独立于起始页的首页 URL。 |
| `-image_links` | 启用包含所有图像的链接。默认关闭。 |
| `-index-URL` | 设置默认索引文件名。 |
| `-ismap` | 当客户端存在 MAP 时，包含 ISMAP 链接。默认关闭。 |
| `-link-n` | 设置 `-crawl` 生成的 link#.dat 文件的起始计数。默认值为 0。 |
| `-localhost` | 禁用指向远程主机的 URL。默认关闭。 |
| `-locec` | 允许从本地文件执行本地程序。默认关闭。 |
| `-mime_header` | 包含 mime 头部并强制导出源码。 |
| `-minimal` | 使用极简模式代替有效的注释解析。默认关闭。 |
| `-nested_tables` | 使用嵌套表格逻辑。默认关闭。 |
| `-newschunksize=n` | 设置分块新闻列表中的文章数量。 |
| `-newsmaxchunk=n` | 设置在分块前列表中新闻文章的最大数量。 |
| `-nobold` | 禁用粗体视频属性。 |
| `-nobrowse` | 禁用目录浏览。 |

# 第 V 部分 高级主题

## TABLE 25-1 (续)

| 参数 | 描述 |
| -nocc | 禁用针对设置了副本的邮件发送的 Cc: 提示。默认关闭。 |
| -nocolor | 禁用颜色支持。 |
| -noexec | 禁用本地程序执行。默认关闭。 |
| -nofiler | 禁用文件 URL 的 Referer 头部传输。默认开启。 |
| -nolist | 禁用虚拟占位符中的链接列表功能。默认关闭。 |
| -nlog | 禁用向文档所有者发送错误信息。默认开启。 |
| -nonrestarting_sigwinch | 使窗口大小变化处理程序非重启。默认关闭。 |
| -nopause | 禁用状态行消息的强制暂停。 |
| -noprint | 禁用打印功能，例如 `-restrictions=print`。默认关闭。 |
| -noredir | 不跟随 Location: 重定向。默认关闭。 |
| -noreferer | 禁用 Referer 头部传输。默认关闭。 |
| -nreverse | 禁用反转视频属性。 |
| -nostatus | 禁用杂项信息消息。默认关闭。 |
| -nounderline | 禁用下划线视频属性 |
| -number_fields | 强制对链接以及输入字段进行编号。默认关闭。 |
| -number_links | 强制对链接编号。默认关闭。 |
| -partial | 在下载时显示部分页面。默认开启。 |
| -partial_thres=n | 设置在用部分显示逻辑重绘显示之前渲染的行数。默认值为 -1，这将禁用此功能。 |
| -pauth:id=pw | 设置受保护代理服务器的身份验证信息。 |
| -popup | 通过弹出窗口处理单选 SELECT 而不是单选按钮列表。默认关闭。 |

## TABLE 25-1 (续)

| 参数 | 描述 |
| --- | --- |
| `-post_data` | 从 stdin 读取用于 post 表单的数据，以 -- 结尾结束。 |
| `-preparsed` | 使用 `-source` 显示解析后的文本/html 并在视图中查看，以视觉化 Lynx 处理无效 HTML 的行为。默认关闭。 |
| `prettysrc` | 在源码视图中使用语法高亮和超链接。默认关闭。 |
| `-print` | 启用打印功能，与 `-noprint` 相。默认关闭。 |
| `-pseudo_inlines` | 为没有 ALT 字符串的内联内容使用伪 ALT。默认开启。 |
| `-raw` | 使用 8 翻译默认设置或 CJK 模式作为启动字符集。默认关闭。 |
| `-realm` | 限制访问起始域内的 URL。默认关闭。 |
| `-reload` | 刷新代理服务器上的缓存（仅限第一个文档）。默认关闭。 |
| `-restrictions=options` | 设置限制选项。使用不带参数的 `-restrictions` 查看列表。 |
| `-resubmit_posts` | 当通过 PREV_DOC 命令或从历史列表中请求其返回的文档时，强制重新提交表单 POST（不使用缓存）。默认关闭。 |
| `-login` | 禁用登录功能。默认关闭。 |
| `-selective` | 需要 `.browsable` 文件来浏览目录。 |
| `-short_url` | 启用在状态行中检查长 URL 的开头和结尾。默认关闭。 |
| `-show_cursor` | 设置为关闭时，隐藏右下角的光标，否则显示光标。默认开启。 |
| `-show_rate` | 显示传输速率。默认开启。 |
| `-soft_quotes` | 使用旧版 Netscape 和 Mosaic 的 Bug，将 '>' 视为双引号标签的终止符。默认关闭。 |

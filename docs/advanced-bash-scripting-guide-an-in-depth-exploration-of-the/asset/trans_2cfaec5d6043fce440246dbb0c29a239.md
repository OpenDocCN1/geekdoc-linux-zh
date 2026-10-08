

```bash
echo SERVER_PROTOCOL = $SERVER_PROTOCOL
echo SERVER_PORT = $SERVER_PORT
echo REQUEST_METHOD = $REQUEST_METHOD
echo HTTP_ACCEPT = "HTTP_ACCEPT"
echo PATH_INFO = $PATH_INFO
echo PATH_TRANSLATED = $PATH_TRANSLATED
echo SCRIPT_NAME = $SCRIPT_NAME
echo QUERY_STRING = $QUERY_STRING
echo REMOTE_HOST = $REMOTE_HOST
echo REMOTE_ADDR = $REMOTE_ADDR
echo REMOTE_USER = $REMOTE_USER
echo AUTH_TYPE = $AUTH_TYPE
echo CONTENT_TYPE = $CONTENT_TYPE
echo CONTENT_LENGTH = $CONTENT_LENGTH
```

```bash
exit 0
```

# Here文档提供指令。
<='_test_CGI_'

- 1) 将此文件放入你的 http://domain.name/cgi-bin 目录。
2) 然后，打开 http://domain.name/cgi-bin/test-cgi.sh。

_test_CGI_
出于安全考虑，识别计算机正在访问的 IP 地址可能会有所帮助。

# 示例 30-2. IP 地址

```bash
#!/bin/bash
# ip-addresses.sh
# 列出你的计算机连接的 IP 地址。

# 灵感来自 Greg Bledsoe 的 ddos.sh 脚本，
# Linux Journal, 2011年3月9日。
# URL:
# http://www.linuxjournal.com/content/back-dead-simple-bash-complex-ddos
# Greg 以 GPL 协议授权了他的脚本，
# 作为衍生版本，此脚本同样遵循 GPL2 协议。
```

```bash
connection_type=TCP # 也尝试 UDP。
field=2 # 我们感兴趣的输出字段。
no_match=LISTEN # 过滤掉包含此内容的记录。为什么？
lsof_args=-ni # -i 列出与 Internet关联的文件。
# -n 保留数字型 IP 地址。
# 不使用 -n 选项会发生什么变化？试试看。
router="[0-9] [0-9] [0-9] [0-9]"
# 删除路由器信息。
```

```bash
lsof "$lssof_args" | grep "$connection_type" | grep -v "$no_match*"
awk '{print $1}' | cut -d ' ' -f $field | sort | uniq
sed 's/$//'
```

```bash
# Bledsoe 的脚本将过滤后的 IP 列表输出
#（类似于第19-22行）赋值给变量。
# 他检查了到单个 IP 地址的多次连接，
# 然后使用：
```

```bash
iptables -I INPUT -s $ip -p tcp -j REJECT --reject-with tcp
```

第 30 章 网络编程

```bash
# ... 在 60 秒延迟循环内，以反射来自 DDOS 攻击的数据包。

# 练习：
# -----
# 使用 'iptables' 命令扩展此脚本
#+ 以拒绝来自已知垃圾邮件 IP 域的连接尝试。
```

更多网络编程示例：

- 1. 从 nist.gov 获取时间
- 2. 下载 URL
- 3. 一个 GRE 隧道
- 4. 检查 Internet 服务器是否在线
- 5. 示例 16-41
- 6. 示例 A-28
- 7. 示例 A-29
- 8. 示例 29-1

另见“系统与管理命令”章节中的网络命令，以及“外部过滤器、程序和命令”章节中的通信命令。

# 第 31 章 零与空值

> 错误的无懈可击，冰冷的规整，华丽的空无

完美的完美；仅此而已。

-- 阿尔弗德·罗德·丁尼森

```bash
/dev/zero ... /dev/null
```

/dev/null 的用途
将 /dev/null 视为黑洞。它本质上等同于一个只写文件。所有写入它的内容都会消失。尝试从中读取或输出将导致无结果。尽管如此，/dev/null 在命令行和脚本中都非常有用。

抑制标准输出 (stdout)。

```bash
cat $filename >/dev/null
# 文件内容不会列到标准输出。
```
抑制标准错误 (stderr）（来自示例 16-3）。

```bash
rm $badname 2>/dev/null
# 这样错误信息 [stderr] 就会消失。
```
同时抑制标准输出和标准错误。

```bash
cat $filename 2>/dev/null /dev/null
# 如果 "$filename" 不存在，将没有错误信息输出。
# 如果 "$filename" 存在，文件内容不会列到标准输出。
# 因此，上述行代码不会产生任何输出。

# 这在需要测试命令的返回码但不需要任何输出的情况下可能很有用。

cat $filename &>/dev/null
# 正如 Baris Cisek 所指出的，这同样有效。
```

删除文件内容但保留文件本身及其所有权限（来自示例 2-1 和示例 2-3）。

```bash
cat /dev/null /var/log/messages
# > /var/log/messages 效果相同，但不会产生新进程。
cat /dev/null /var/log/wtmp
```

自动清空日志文件内容（对于处理商业网站发送的讨厌的“cookies”非常好）：

# 示例 31-1. 隐藏 Cookie 桶

```bash
# 已过时
# 此脚本不再使用。
```


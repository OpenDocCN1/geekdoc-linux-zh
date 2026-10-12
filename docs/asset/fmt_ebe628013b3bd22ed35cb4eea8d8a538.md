
250 May 16 18:26:55 Target sendmail: connect from linux2.samacker.net (172.16.0.2)

5 May 16 22:58:40 Target sendmail: NOQUEUE: SYSERR(root):
-> daemon: cannot fork: Resource temporarily unavailable

1 May 16 22:58:40 Target sendmail: NOQUEUE: SYSERR(root):
-> daemon: cannot fork: Resource temporarily unavailable
-> filter `/usr/sbin/sysmonpp` failed: Resource temporarily unavailable

3 May 16 22:58:40 Target ybindd: broadcaster
-> fork failure: Resource temporarily unavailable

如果你发现此类连接请求（如第 1 行），拦截违规 IP，追踪所有者并联系其提供商。

# Linux 应用程序攻击

接下来，让我们看看针对 Linux 应用程序的攻击。

## Netscape Communicator Content Type (1)

- 攻击类型：强制总线错误
- 日期：1998年10月
- 受影响版本：Netscape Communicator 4.05 + 4.5b(1)
- 结果：Communicator 冻结并导致总线错误。利用程序：向 Communicator 内部/解析内容类型。
- 作者：Jim Paris
- 测试代码：http://geek-girl.com/bugtraq/1998_4/0034.html
- 修复或补丁：升级或联系 Netscape 获取更多信息。
- 修复或补丁作者：无

讨论：Web 服务器和浏览器可以解释 MIME 类型。最常见的是 `text/html` 和 `text/plain`，网站管理员通常在文档开头宣布这两种。这告诉浏览器如何处理数据。

例如，在 CGI 脚本中设置变量并从用户输入中剥离危险的元字符后，习惯上包含一个 content type 打印语句来通知浏览器消息从何时开始，如下：

```
#!/usr/local/bin/perl

if ($SENV{'REQUEST_METHOD'} eq 'POST') {

    read(STDIN, $buffer, $SENV{'CONTENT_LENGTH'});

    @pairs = split(/\/, $buffer);

    foreach Spair (@pairs) {

        ($name, $value) = split(/=, $pair);

        $value -= tr/+ /;

        $value -= s/%([a-fA-F0-9][a-fA-F0-9])/pack("C", hex($1))/eg;

        $value -= tr/ /;

        $contents{$name} = $value;

    }

}

print "Content-type: text/html\n\n";

[on-the-fly-HTML-and-output-goes-here];
```

## Netscape Communicator Content Type (2)

- 攻击类型：缓冲区溢出
- 日期：1998年10月
- 受影响版本：Netscape Communicator 4.0–4.5

### Linux 网络安全第四部分

在受影响的系统中，本地非特权用户可以锁定 `wtmp` 并阻止登录 `nvi`（`nvi` 是原始 BSD 编辑器的克隆）。该攻击方法非常直接：

```
attacker$ nvi /var/log/wtmp
```
安装 Null 的补丁或升级。

#### passwd 饥饿 (passwd Starvation)
- **攻击类型:** 资源饥饿
- **日期:** 1998 年 2 月
- **受影响版本:** Red Hat 0.50-7
- **结果:** 攻击可以锁定 `/etc/passwd`。
- **利用方法:** 使用显式文件大小限制调用 `passwd`。
- **作者:** Antonomasia
- **测试代码:** http://www.merton.ac.uk/security/archive/199802/0040.html
- **修复或补丁:** 升级（N/A）
- **讨论:** `passwd` 是一个用于添加或更改密码的程序。在受影响的系统中，攻击者可以带显式文件大小限制调用 `passwd`。如果 `/etc/passwd` 超过此限制，`passwd` 将无法写入该文件并直接终止。同时，`/etc/passwd` 保持锁定状态且无法接受新更改。

#### xdm
- **攻击类型:** xdm 洪水
- **日期:** 1997 年 8 月
- **受影响版本:** Red Hat 2.0.30, Linux 3.3（可能更高？）
- **结果:** 攻击导致本地显示器崩溃。
- **利用方法:** Telnet 连接到 chooser 使用的端口。
- **作者:** Paul H. Hargrove
- **测试代码:** 无
- **修复或补丁:** 升级（N/A）
- **讨论:** `xdm` 显示管理器，一个提供会话管理、认证等功能的工具。`xdm` 伴有一个 chooser 应用用于列出当前可用服务器。在受影响的版本中，攻击者可以通过发送垃圾字符串 telnet 到 `xdm` 用于处理 chooser 的端口，从而导致 `xdm` 崩溃并防止用户在本地显示器上访问 X。

#### wtmp 锁定 (wtmp lock)
- **攻击类型:** wtmp 锁定
- **日期:** 1996 年
- **受影响版本:** Red Hat 3.0, Debian 1.2, Linux-2.4
- **结果:** 任何人无法登录。
- **利用方法:** 在 `wtmp` 上放置排他锁。
- **作者:** NuNo
- **测试代码:** 见下文。
- **修复或补丁:** http://www.dataguard.org/bugtrap/1996_4/0325.html (N/A)
- **讨论:** 当前系统的 `/var/log/wtmp` 返回所有登录和注销记录。这是查询并报告列表的文件：

```
anon ftp@linux2.sam May 17 00:15

anon ftp@linux2.samshacker.net May 17 00:14

anon ftp@linux2.samshacker.net May 16 23:31
```

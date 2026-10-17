
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

1. 作为 `root`，在命令行运行以下命令：
    ```perl
    perl -MCPAN -e shell
    ```

2. 在 `cpan>` 提示符下输入 `install FCGI` 命令，如果您尚未拥有最新版本，这将安装该 CPAN 模块的最新版本。

3. 在上述脚本的第二行添加以下行：
    ```perl
    use FCGI;
    ```
    这指示 Perl 在运行脚本时加载 `FCGI` 模块。

4. 确定 CGI 应用程序的初始化块。对于此脚本，初始化块由以下两个变量声明组成：
    ```perl
    my $MAX = 10;

    my $i;
    ```

5. 确定 CGI 应用程序的响应循环和 body 块。由于每个请求都必须以适当的 Content-Type 头响应，主代码的 body 从以下行开始：
    ```perl
    print "Content-type: text/html\n\n";
    ```
    负责实际处理的 `for` 循环是 body 的其余部分。

6. 既然 body 代码已识别，您需要将其周围加上响应循环。使用以下代码完成：
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

整个应用程序的 FastCGI 版本列于列表 14-3 中。

### 列表 14-3：`fontsize.fcgi`

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

- 1. 从 `www.fastcgi.com` 下载适用于 Apache 的最新 `mod_fastcgi` 模块。
- 2. 在 `/usr/local/src` 目录中提取源文件。会创建一个新的目录，名为 `mod_fastcgi_version`。阅读此新目录中的 `INSTALL` 文件以了解安装该模块的详细信息，因为安装方式会不时变化。
- 3. 将新目录复制到 Apache 源代码树中 `modules` 目录下的名为 `fastcgi` 的子目录中。
- 4. 在 Apache 源代码发行版目录中，运行 `configure --enable-module=fastcgi` 以及你想要为 `configure script` 指定的任何其他选项。（有关 `configure script` 可用其他选项的详细信息，请参阅第 3 章。）如果你已经编译了 Apache，可以将前一条命令中的 `configure` 替换为 `config.status`，以确保在最后一次运行 `configure` 时指定的所有选项都再次被应用。
- 5. 运行 `make` 和 `make install` 来编译并安装支持 `mod_fastcgi` 的 Apache。
- 6. 使用 `/usr/local/apache/bin/apachectl restart` 命令重启 Apache。

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

应用程序在端口 `9000` 上监听。当通过此指令加载的 FastCGI 应用程序停止运行时，`mod_fastcgi` 会重启该应用程序并在错误日志文件中写入日志条目。`AppClass` 指令的可选参数如下：

- `processes` — 此选项指定要创建多少个 FastCGI 进程。在高负载场景中，加载同一 FastCGI 应用程序的多个实例可以提供更好的性能。默认值为 1。
- `listen-queue-depth` — 此选项指定通过该指令加载的 FastCGI 应用程序的监听队列深度。默认值在大多数情况下就足够了，但在高负载场景中，你可以增加队列的深度。这可以减少因应用程序繁忙而导致请求被拒绝的可能性。然而，如果你预期会有高负载，并且你的服务器能够运行额外的几个 FastCGI 进程，请增加进程数量而不是监听队列的深度。默认值为 5。
- `restart-delay` — 此选项指定用于延迟重启已停止的 FastCGI 进程的时间（以秒为单位）。仅当使用同一 FastCGI 应用程序的多个实例时才有用。对于单个 FastCGI 应用程序，它会立即重启，此选项无效。默认值为 5。你可能会疑惑为什么需要这个延迟。通常，FastCGI 应用程序不应该停止运行；如果它正在停止运行，说明可能存在某些问题。在这种情况下，该延迟允许你的服务器执行其他有用的任务，而不是反复重启有故障的应用程序。
- `priority` — 此选项设置 FastCGI 应用程序的进程优先级。默认值使 FastCGI 应用程序具有与 Apache 服务器本身的相同优先级。其他合适的值由操作系统的 `setpriority` 系统调用定义。在 Red Hat Linux 系统中，`setpriority` 系统调用允许的值范围为 –20 到 20。数字越小，用于该进程的调度越有利。但是，`mod_fastcgi` 不允许负值，这意味着你不能将 FastCGI 进程的优先级设置得高于 Apache 服务器本身。因此，你只能使用正整数来降低应用程序的优先级。默认值为 0。
- `port` — 此选项指定 FastCGI 应用程序将监听的 TCP 端口。由于低于 1024 的端口用于标准服务，因此你必须使用较高的端口号。使用此选项允许你从另一个系统访问该应用程序。默认情况下不提供环境变量。
- `socket` — 此选项指定应用程序监听的 Unix 域套接字的路径名。该模块在由 `FastCgiIpcDir` 指令指定的目录中创建此套接字。默认值为 `DefaultSocket`。如果你未提供端口或套接字选项，模块将由应用程序本身创建一个 Unix 域套接字。
- `initial-env` — 此选项可用于在 FastCGI 应用程序的环境表中插入环境变量（带值）。你可以多次使用此选项以在应用程序的环境中插入多个键值对。默认情况下不提供环境变量。

请注意，`-socket` 和 `-port` 选项是互斥的。路径名不得等于先前 `AppClass` 或 `ExternalAppClass` 指令提供的路径名。

### ExternalAppClass 指令

当你在另一个系统上运行 FastCGI 应用程序时，请使用此指令。

- **语法：** `ExternalAppClass FastCGI_application_name [-host host[:port]] [-socket sock_name]`
- **上下文：** 服务器配置

在以下示例中，`echo.fcgi` 应用程序正在名为 `fcgi.nitc.com` 的主机上运行，并监听端口 `9090`。`<FastCGI-application-name>` 只是一个标识符，可用于描述在远程主机上运行的应用程序，因此可以是任何你想要的名称。确保你选择的名称尚未在另一个 `AppClass` 或 `ExternalAppClass` 指令中使用。

```apache
ExternalAppClass echo.fcgi -host fcgi.nitc.com:9090
```

`ExternalAppClass` 指令的可选参数如下：

- `host` — 此选项允许你指定在另一个系统上运行的 FastCGI 应用程序的主机和 TCP 端口号。使用 `host:port` 格式指定主机和端口。你可以使用主机名或 IP 地址。
- `socket` — 此选项允许你指定 FastCGI 应用程序正在使用的 Unix 域套接字的路径名。

### FastCgiIpcDir 指令

此指令指定由模块创建的 Unix 域套接字的默认路径。只要你没有设置定时任务（`cron jobs`）定期清理 `/tmp` 目录，默认的 `/tmp` 位置就没问题。

**语法：** `FastCgiIpcDir path_to_UNIX_domain_socket`
**默认：** `FastCgiIpcDir /tmp`
**上下文：** 服务器配置

套接字名称具有以下格式：

```
OM_WS_n_.pid
```

`n` 是一个数字，`pid` 是主 Apache 进程的进程 ID。如果你将此指令设置为路径，请确保只有 Apache 具有对该目录的读写权限。

## 配置 httpd.conf 以支持 FastCGI

为了配置 FastCGI 应用程序，你需要结合使用 `mod_fastcgi` 指令和 Apache 服务器提供的指令。

使用 `AppClass` 指令启动你希望由此 Web 服务器管理的 FastCGI 应用程序。这里的“管理”是指当受管理的进程停止运行时，服务器会记录错误消息，并尝试重启那些停止运行的受管理进程。

使用 `AppClass` 和/或 `ExternalAppClass` 指令来定义路径名与 FastCGI 应用程序连接信息之间的关联。连接信息可以是 Unix 域套接字的路径名，也可以是 TCP 端口的 IP 地址和端口号。这两个指令的区别在于：单个 `AppClass` 指令既启动应用程序又设置与其通信的关联，而 `ExternalAppClass` 仅定义关联。对于 `AppClass`，关联中使用的路径名始终是应用程序可执行文件的路径名；而对于 `ExternalAppClass`，路径名是任意的。

如果要让 `mod_fastcgi` 处理 HTTP 请求，该请求的处理程序必须是 `fastcgi-script`，或者请求的 MIME 类型必须是 `application/x-httpd-fcgi`。Apache 提供了多种方式来设置请求的处理程序和 MIME 类型：

- `SetHandler`（在 `Location` 或 `Directory` 部分或按目录访问控制文件的上下文中）可以将处理程序 `fastcgi-script` 关联到特定文件或目录中的所有文件。
- `AddHandler` 可以根据文件扩展名将处理程序 `fastcgi-script` 关联到文件。
- `ForceType`（在 `Location` 或 `Directory` 部分或 `.htaccess` 文件的上下文中）可以将 MIME 类型 `application/x-httpd-fcgi` 关联到特定文件或目录中的所有文件。
- `AddType` 可以根据文件扩展名将 MIME 类型 `application/x-httpd-fcgi` 关联到文件。

配置好 `mod_fastcgi` 模块后，它按以下方式处理请求：

1. 检索与所请求的路径名相关的连接信息。如果没有与该路径名关联的连接信息，服务器将返回错误代码 404 Not Found。
2. `mod_fastcgi` 模块连接到 FastCGI 应用程序进程。如果连接尝试失败，服务器将返回 500 Server Error。
3. 请求被传输到 FastCGI 应用程序进程，该进程生成响应。
4. 接收应用程序的响应并将其转换为 HTTP 响应。服务器将此响应发送回客户端。

你应该备份现有的 `httpd.conf` 文件，但不要立即使用清单 14-4 中的示例配置文件。这是一个最小化配置，仅用于测试目的，只使用 `httpd.conf` 文件。请使用此配置进行 FastCGI 的初始测试，当你验证该配置有效后，将此配置中与 FastCGI 相关的部分与你自己的配置进行合并。

### 清单 14-4: 示例 httpd.conf 配置文件

```apache
# httpd.conf-minimal for mod_fastcgi

Port 80

# You should replace the User/Group directive with appropriate

# user/group name

User $HTTP_USER

Group $HTTP_GROUP

# Configure just one idle httpd child process, to simplify

# debugging

StartServers 1

MinSpareServers 1

MaxSpareServers 1

# Tell httpd where it should live, turn on access and error

# logging

ServerRoot        $APACHE

ErrorLog          logs/error.log

TransferLog       logs/access.log

ScoreBoardFile    logs/httpd.scoreboard

# Tell httpd where to get documents

#

DocumentRoot $FASTCGI
```

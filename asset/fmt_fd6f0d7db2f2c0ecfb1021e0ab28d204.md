
### `/my_dir` 目录选项

```apache
<Directory /my_dir>
    Options -FollowSymLinks +SymlinksIfOwnerMatch
</Directory>
```

在此情况下，如果 `/my_dir` 目录中的符号链接的所有者 ID 与服务器的用户 ID 匹配，Apache 将跟随这些符号链接。

## 使用 ApacheBench 调优配置

Apache 服务器附带一个名为 `ApacheBench` (`ab`) 的工具，它默认安装在 Apache 安装目录的 `bin` 目录中。通过使用这个实用工具，你可以调优你的服务器配置。

根据你多处理模块（MPM）的选择（`prefork`、`threaded`、`perchild`），你需要调优以下默认配置的值：

**Prefork MPM**

```apache
<IfModule prefork.c>
  StartServers 5
  MinSpareServers 5
  MaxSpareServers 10
  MaxClients 20
  MaxRequestsPerChild 0
</IfModule>
```

**Threaded MPM**

```apache
<IfModule threaded.c>
  StartServers 3
  MaxClients 8
  MinSpareThreads 5
  MaxSpareThreads 10
  ThreadsPerChild 25
  MaxRequestsPerChild 0
</IfModule>
```

**Perchild MPM**

```apache
<IfModule perchild.c>
  NumServers 5
  StartThreads 5
  MinSpareThreads 5
  MaxSpareThreads 10
  MaxThreadsPerChild 20
  MaxRequestsPerChild 0
</IfModule>
```

随机调优这些指令不是一个好主意。因为你的 Web 站点及其流量模式和应用可能与其他站点不同，所以没有一个通用的公式来计算这些指令的适当值。然而，我将向你展示一种使用 `ApacheBench` 来确定适当值的技术。

**注意** 你应该在与 Web 服务器不同的系统（或多个系统）上使用 `ApacheBench` 工具，因为试图使用客户端/服务器模型在同一台服务器上进行基准测试会给你提供虚假信息。基准测试工具 `ab` 本身会从服务器中占用资源，从而篡改你的结果。因此，你必须在另一台机器上运行 `ab`。我推荐你在多台机器上运行 `ab`，以更好地模拟负载。

**提示** 你需要在其他机器上编译 Apache，以在非 Web 服务器系统上安装 `ab` 二进制文件。你可以在这样的系统上安装 Apache 的二进制 RPM 包，并在调优完成后将其卸载。有关如何安装和配置 Apache 的详细信息，请参阅第 2 章和第 3 章。

确定服务器的目标。估算（或猜测）你希望 Web 服务器能够处理多少请求。将其写在一个目标陈述中，例如：“我希望每秒处理 `$N` 个请求。”

重启你的 Web 服务器，并在除 Web 服务器以外的系统上运行 `ab` 命令，方法如下：

```bash
./ab -n number_of_total_requests \
   -c number_of_simultaneous_requests \
      http://your_web_server/page
```

例如：

```bash
./ab -n 1000 -c 50 http://www.domain.com/
```

`ApacheBench` 工具将发起 50 个并发请求，总请求数为 1,000 个。示例输出如下所示：

```text
Server Software:        Apache/2.0.16
Server Hostname:        localhost
Server Port:            80
Document Path:          /
Document Length:        1311 bytes
Concurrency Level:      50
Time taken for tests:   8.794 seconds
Complete requests:      1000
Failed requests:        0
Total transferred:      1754000 bytes
HTML transferred:       1311000 bytes
Requests per second:    113.71
Transfer rate:          199.45 kb/s received
Connection Times (ms)
              min     avg     max
Connect:        0      0       5
Processing:   111   427     550
Total:        111   427     555
```

请注意，访问 `http://www.domain.com` 站点主页时，每秒请求数（Requests per second）为 113.71。将并发请求数改为更高的数值，观察服务器如何处理额外的并发负载。

现在，根据你的 MPM 更改 `MaxClients`、`ThreadsPerChild` 和 `MaxThreadsPerChild` 等值，重启 Apache，并像之前一样使用 `ab` 应用相同的基准测试。你应该会看到，根据你尝试的数字，每秒请求数会有所升降。当你通过更改指令值来调整数字时，请确保记录这些值和性能，以便你确定什么设置适合你。

## 通过缓存提升速度

缓存 Web 内容并不是一个新概念。大多数繁忙的 Web 站点都通过代理服务器或其他机制来实现缓存。这里我将讨论两个可供选择的选项。你还应该研究使用第 10 章中讨论的 `mod_proxy` 模块来利用 Apache 的代理功能。

### 使用 `mod_fcache` 将常用文件缓存在内存中

Apache 的 `mod_fcache` 模块将特定类型的文件缓存在内存中。缓存的文件存储在服务器的主内存空间中，并且可被所有 Apache 子进程访问。你可以从 `www.fractal.net/mod_fcache.tm` 下载此模块。要编译和安装此模块，请遵循以下步骤：

- 以 root 身份使用 `tar xvfz mod_fcache.tar.gz` 命令解压缩模块源代码，并将新创建的目录复制到你的 Apache 源代码分布的 `modules` 子目录中。例如，如果你将 Apache 源代码安装在 `/usr/local/src/httpd_2.0.16`，将 `fcache` 安装在 `/usr/local/src/fcache`，那么你可以通过使用 `cp -r /usr/local/src/fcache /usr/local/src/httpd_2.0.16 modules` 命令复制模块文件。
- 更改目录到 Apache 源代码分布的 `modules/fcache` 子目录。查看 `config.m4` 文件，看看是否需要对系统进行修改。通常你不需要做任何更改。如果你确实需要更改，你应该知道自己在做什么。
- 运行 `autoconf` 来配置所有内容。
- 将目录更改回顶层 Apache 源代码分布，并运行 Apache 的 `configure` 脚本，加上你通常使用的所有选项（参见 `config.status` 文件）以及 `--enable-fcache` 选项。
- 使用 `make && make install` 命令如常编译和安装 Apache。
- 使用 `/usr/local/httpd/apachectl restart` 命令重启 Apache Web 服务器。

现在你可以准备使用此模块了。例如，要缓存从名为 `common_images` 的目录提供的 GIF 图像，你在 `httpd.conf` 中使用以下配置段：

```apache
<Directory /common_images>

  fcache              On

  fcache_CacheTypes   image/gif

  fcache_MaxSize      10240

  fcache_RecomputeTables 600

</Directory>
```

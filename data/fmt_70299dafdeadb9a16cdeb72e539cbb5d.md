
该目录必须存在。Squid 不会为你创建它。但是，它会创建一级和二级目录。

- `cache_mgr` — 添加在缓存守护进程崩溃时接收电子邮件的用户邮箱。默认情况下，电子邮件将发送给本地管理员（Webmaster）。要将该值更改为 `root` 用户，请使用以下：

```
cache_mgr root
```

- `cache_effective_user` — `squid` 守护进程以 `root` 身份启动后，后续进程将以 Squid 用户和组（默认）运行。要将该用户更改为不同的名称（例如 `nobody`），请如下所示设置 `cache_effective_user`：

```
cache_effective_user nobody
```

## 在 squid.conf 中配置端口号

当你配置计算机使用你的代理服务器时，客户端需要知道你计算机的名称（或 IP 地址）以及与服务相关的端口。对于想要通过你的代理访问 Web 的客户端来说，HTTP 端口是所需的数字。以下是让你用于在 Squid 中为不同服务设置端口值的标签及其默认值：

- `http_port 3128` — `http_port` 默认设置为 `3128`。客户端需要知道这个数字（或你修改后的数字）来访问你的代理服务器进行 HTTP 服务（即网页浏览）。
- `icp_port 3130` — ICP 请求默认通过端口 `3130` 在相邻缓存之间发送。
- `htp_port 4827` — Squid 默认通过端口 `4827` 在相邻缓存之间发送 HTTP 请求。

## 调试 Squid

如果 Squid 在设置后后工作不正常，或者你只是想监控 Squid 的活动，有几个工具和日志文件可以帮助你。下文将进行介绍。

### 检查 squid.conf 文件

通过带有 `-X` 选项（前文描述）运行 `squid` 守护进程，你可以检查 `squid.conf` 文件中的设置。你可以在 `/etc/init.d/squid` 的 `SQUID_OPTS` 行中添加 `-X` 选项。然后运行 `/etc/init.d/squid restart`。将输出大量信息，详细说明了设置内容。

### 检查日志文件

Squid 日志文件（在 Red Hat Linux 中）默认存储在 `/var/log/squid`。以下是创建的日志文件、其内容描述以及它们如何帮助你调试潜在问题：

- `access.log` — 描述客户端请求内容时每次缓存命中或未中的条目。同时还包括发出请求的主机身份（IP 地址）和它们请求的内容。使用这些信息可以找出哪些内容是从缓存使用的，以及何时访问了远程服务器。以下是某些结果的含义：
  - `TCP_DENIED` — Squid 拒绝了该请求。
  - `TCP_HIT` — 缓存包含对象的有效副本。
  - `TCP_MISS` — 当客户端询问内容是否更改时，请求的对象的版本仍在缓存中。
  - `TCP_MEM_HIT` — 内存包含该对象的有效副本。
  - `TCP_MISS` — 缓存不包含该对象。
  - `TCP_NEGATIVE_HIT` — 对象被负缓存，意味着在请求该对象时返回了错误（例如未找到文件）。
  - `TCP_FAIL_HIT` — 由于验证对象的请求失败，从缓存返回了过时的对象。
  - `TCP_REFRESH_HIT` — 缓存中有对象的过时副本，但对服务器的请求返回的信息显示对象未修改。
  - `TCP_REFRESH_MISS` — 缓存对象被新的、更新的内容替换。
  - `TCP_SWAP_FAIL` — 尽管认为对象应该在那里，但无法从缓存访问该对象。

- `cache.log` — 包含 `squid` 守护进程启动时关于你 Squid 配置的宝贵信息。你可以看到可用内存（`Max Mem`）、可用空间（`Max Swap`）、缓存目录的位置（`/var/spool/squid`）、正在访问的连接类型以及哪些连接被接受。

- `store.log` — 包含对象从内存交换（`SWAPOUT`）、进入内存（`SWAPIN`）或释放（`RELEASE`）到缓存的条目。另一个可能感兴趣的日志文件是：`var/log/messages`。该文件包含了 `squid` 守护进程启动时的状态。

### 使用 top 命令

运行 `top` 命令查看 Squid 运行信息。如果你发现 Squid 占用了过多的内存，可以通过 `top` 查看按进程排序的百分比。如果你发现 Squid 消耗了过多内存，可以在 `squid.conf` 中重置 `cache_mem` 值。（有一个图形界面版本的 `top` 可以从桌面运行。）

## 设置代理客户端

为了让你的 Red Hat Linux 代理服务器为局域网内的计算机提供 Web 浏览（HTTP）访问，每个客户端都需要在浏览器中进行一些设置。使用代理服务器的优点在于客户端计算机不需要知道以下内容，例如：

- DNS 服务器的地址
- ISP 的电话号码
- 连接 ISP 的聊天脚本

在代理服务器连接到互联网并允许局域网内的计算机访问该服务后，客户端只需要知道以下：

- 主机名 — 代理服务器的名称或 IP 地址。（这假设客户端可以通过公司局域网或其他 IP 网络访问代理。）
- 端口号 — HTTP 服务的端口号（默认为 `3128`）。同一端口号也可以用于 FTP 和 gopher 服务。

### 配置 Internet Explorer 使用代理

要配置 Internet Explorer 使用代理服务器访问 Web，你需要更改一些 Internet 选项。请按照以下步骤操作：

1. 打开 Internet Explorer 窗口。
2. 选择“查看：Internet 选项”。出现“Internet 选项”窗口。
3. 点击“连接”标签。
4. 假设你已经配置了局域网（LAN），点击“局域网”，然后点击“设置”。出现“局域网设置”窗口。
5. 输入代理服务器的地址和 HTTP 服务的端口号（可能是 `3128`）。

提示：Internet Explorer 假设 HTTP、Gopher 和 FTP 服务使用相同的端口。如果情况并非如此，点击“高级”并根据需要更改每个服务的端口号。

6. 点击“确定”（在“局域网设置”窗口中），再次点击“确定”（在“Internet 选项”窗口中）。

下次你尝试从 Internet Explorer 访问 Web 时，它将尝试通过你定义的代理服务器进行。

### 配置 Mosaic 和 Lynx 浏览器使用代理

要让 Mosaic 或 Lynx 浏览器使用代理服务器访问 Internet，请在运行浏览器的 shell 中添加环境变量。以下是在 csh 或 tsh 中为名为 `maple` 的代理计算机设置 HTTP、Gopher 和 FTP 代理服务的方法：

```
setenv http_proxy http://maple:3128/
setenv gopher_proxy_http http://maple:3128/
setenv ftp_proxy_http http://maple:3128/
```

如果你正在使用 `ksh` 或 `bash` shell，请输入以下内容：

```
export http_proxy http://maple:3128
export gopher_proxy_http http://maple:3128
export ftp_proxy_http http://maple:3128
```

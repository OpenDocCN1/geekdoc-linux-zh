
你可能会遇到运行在 TCP 端口 111 上的服务 `rpcbind` 或 `portmapper`。事实上，`rpcbind` 曾出现在之前对一个易漏洞文件服务器的端口扫描中。这里是该行代码的内容：

```
111/tcp  rpcbind
```

`RPCbind` 是一个运行在服务器上的 ON RPC 实用程序，它监听传入的 RPC 请求。它本身不处理请求，而是将它们转发到服务器上正确的端口。它将绑定的 RPC 程序号映射到服务正在监听的端口，该端口可以处理该特定的调用。程序号用于标识 RPC 可以提供的许多不同数字标识功能。例如，程序号 100021 是网络锁管理器，简称为 `nlockmgr`。该服务负责处理从客户端到文件的调用（即处理文件是否正在被他人编辑）。程序号 100021 将被 `RPCbind` 映射到 `nlockmgr` 运行的端口。`Lockmgr` 是网络文件系统 `NFS` 的一部分，`NFS` 通常用于在 UNIX 类系统之间共享文件。

还有许多其他 RPC 程序号，但目前我们关注的是与文件共享相关的那些。负责映射程序号的程序 `RPCBind` 也有自己的程序号——100000。`NFS` 的程序号为 100003，而用于处理挂载 NFS 网络文件夹的服务名为 `mount` (`mount` 守护进程)，其程序号为 100024。文件共享的另一个重要服务是 `stat` (status 守护进程)，其程序号为 10024。

你可能应该安装一个实用的包（在你的易漏洞 Ubuntu 虚拟机上以及在你的 Kali Linux 虚拟机上，如果还没有的话），该包是 `nfs-common`（使用命令 `sudo apt install nfs-common`）。此包包含许多工具，包括 `RPCbind`。

你不需要知道为什么 RPC 对黑客来说很有趣。事实上，有一整套接口允许你在网络上的其他计算机上运行代码。事实上，提供这种功能是相当复杂的。这是因为有不同的协议、这些协议的版本，以及这些协议的所有实现方式共同作用，才使得共享文件这一简单任务得以实现！然而，越是复杂，越容易产生误解——而且确实为坏分子提供了利用的空间。理想情况下，你能够在客户的漏洞被恶意利用之前识别出任何机会。

## RPCinfo

你可以使用一个名为 `rpcinfo` 的工具来查找远程主机提供了哪些 RPC 服务。尝试使用 `rpcinfo -p <TargetIP>`，如果运行着 `rpcbind` 服务，将显示类似下面的输出（以下取自一个完全的 NAS 系统）：

```
program vers proto port service
100000 4 tcp 111 portmapper
100000 3 tcp 111 portmapper
100000 2 tcp 111 portmapper
100000 4 udp 111 portmapper
100000 3 udp 111 portmapper
100000 2 udp 111 portmapper
100024 1 udp 50830 status
100024 1 tcp 55874 status
100003 2 tcp 2049 nfs
100003 3 tcp 2049 nfs
100003 4 tcp 2049 nfs
100027 2 tcp 2049
100027 3 tcp 2049
100003 2 udp 2049 nfs
100003 3 udp 2049 nfs
100003 4 udp 2049 nfs
100027 2 udp 2049
100027 3 udp 2049
100027 4 udp 2049
100021 1 udp 35882 nlockmgr
100021 3 udp 35882 nlockmgr
100021 4 udp 35882 nlockmgr
100021 1 tcp 45930 nlockmgr
100021 3 tcp 45930 nlockmgr
100021 4 tcp 45930 nlockmgr
100005 1 udp 60976 mountd
100005 1 tcp 37269 mountd
```

| program | vers | proto | port | service |
| :--- | :--- | :--- | :--- | :--- |
| 100000 | 4 | tcp | 111 | portmapper |
| 100000 | 3 | tcp | 111 | portmapper |
| 100000 | 2 | tcp | 111 | portmapper |
| 100000 | 4 | udp | 111 | portmapper |
| 100000 | 3 | udp | 111 | portmapper |
| 100000 | 2 | udp | 111 | portmapper |
| 100024 | 1 | udp | 50830 | status |
| 100024 | 1 | tcp | 55874 | status |
| 100003 | 2 | tcp | 2049 | nfs |
| 100003 | 3 | tcp | 2049 | nfs |
| 100003 | 4 | tcp | 2049 | nfs |
| 100027 | 2 | tcp | 2049 |  |
| 100027 | 3 | tcp | 2049 |  |
| 100003 | 2 | udp | 2049 | nfs |
| 100003 | 3 | udp | 2049 | nfs |
| 100003 | 4 | udp | 2049 | nfs |
| 100027 | 2 | udp | 2049 |  |
| 100027 | 3 | udp | 2049 |  |
| 100027 | 4 | udp | 2049 |  |
| 100021 | 1 | udp | 35882 | nlockmgr |
| 100021 | 3 | udp | 35882 | nlockmgr |
| 100021 | 4 | udp | 35882 | nlockmgr |
| 100021 | 1 | tcp | 45930 | nlockmgr |
| 100021 | 3 | tcp | 45930 | nlockmgr |
| 100021 | 4 | tcp | 45930 | nlockmgr |
| 100005 | 1 | udp | 60976 | mountd |
| 100005 | 1 | tcp | 37269 | mountd |

| program | vers | proto | port | service |
| :--- | :--- | :--- | :--- | :--- |
| 100000 | 4 | tcp | 111 | portmapper |
| 100000 | 3 | tcp | 111 | portmapper |
| 100000 | 2 | tcp | 111 | portmapper |
| 100000 | 4 | udp | 111 | portmapper |
| 100000 | 3 | udp | 111 | portmapper |
| 100000 | 2 | udp | 111 | portmapper |
| 100024 | 1 | udp | 50830 | status |
| 100024 | 1 | tcp | 55874 | status |
| 100003 | 2 | tcp | 2049 | nfs |
| 100003 | 3 | tcp | 2049 | nfs |
| 100003 | 4 | tcp | 2049 | nfs |
| 100027 | 2 | tcp | 2049 |  |
| 100027 | 3 | tcp | 2049 |  |
| 100003 | 2 | udp | 2049 | nfs |
| 100003 | 3 | udp | 2049 | nfs |
| 100003 | 4 | udp | 2049 | nfs |
| 100027 | 2 | udp | 2049 |  |
| 100027 | 3 | udp | 2049 |  |
| 100027 | 4 | udp | 2049 |  |
| 100021 | 1 | udp | 35882 | nlockmgr |
| 100021 | 3 | udp | 35882 | nlockmgr |
| 100021 | 4 | udp | 35882 | nlockmgr |
| 100021 | 1 | tcp | 45930 | nlockmgr |
| 100021 | 3 | tcp | 45930 | nlockmgr |
| 100021 | 4 | tcp | 45930 | nlockmgr |
| 100005 | 1 | udp | 60976 | mountd |
| 100005 | 1 | tcp | 37269 | mountd |

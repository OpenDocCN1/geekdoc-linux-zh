
`keylogin` 命令是 RPC 命令集的一部分。在你在使用 `keylogin` 之前，系统管理员必须使用 `newkey(1M)`、`nisaddcred(1M)`、`niscient(1M)` 命令生成公钥和私钥。每个用户都有唯一的公钥和私钥。密钥可以在 `/etc/public` 文件中找到（参见 NIS 映射 `publickey.byname` 中的 `public(4)`，或者在 NIS+ 表 `cred.org_dir` `/etc/nwitch.conf` 文件中，参见 `nsswitch.conf(4)`）。

`keylogin` 命令提示输入密码并使用它解密用户的私钥。一旦解密，私钥将被本地密钥服务器进程 `keyserv(1M)` 存储。当向任何安全 RPC 服务（如 NFS 或 NIS+）发出请求时，将使用此存储的密钥。

# keylogin — 使用 keyserv 解密并存储密钥

## 摘要

`/usr/bin/keylogin [-r]`

## 描述

`keylogin` 命令是 RPC 命令集的一部分。在你在使用 `keylogin` 之前，系统管理员必须使用 `newkey(1M)`、`nisaddcred(1M)`、`niscient(1M)` 命令生成公钥和私钥。每个用户都有唯一的公钥和私钥。密钥可以在 `/etc/public` 文件中找到（参见 NIS 映射 `publickey.byname` 中的 `public(4)`，或者在 NIS+ 表 `cred.org_dir` `/etc/nwitch.conf` 文件中，参见 `nsswitch.conf(4)`）。

`keylogin` 命令提示输入密码并使用它解密用户的私钥。一旦解密，私钥将被本地密钥服务器进程 `keyserv(1M)` 存储。当向任何安全 RPC 服务（如 NFS 或 NIS+）发出请求时，将使用此存储的密钥。

# kill

你可以通过信号编号或 `signal(5)` 手册页中列出的逻辑信号名称（去掉 SIG 部分）来指定信号。下面的示例演示了如何通过编号指定信号 15，然后通过名称指定。

```
castle kill -15 456
castle kill -TERM 456
```

当你不指定信号时，`kill` 命令默认发送信号 15 `SIGTERM`。信号 15 在可行的情况下会终止进程，是杀死进程的首选方法。有时即使你使用 `kill` 命令，进程仍然不会终止。常见的有有三种情况：

- 进程正在等待设备（如磁带驱动器）完成操作后再结束。
- 进程正在等待由于 NFS 问题导致不可用的资源。对于此类进程，请使用信号 3 `SIGQUIT`。
- 进程是一个僵尸进程 `zombie`，如 `ps` 报告中的 `defunct` 消息所示。僵尸进程是指已释放所有资源但尚未收到父进程确认的进程，通常收到确认后其条目就会从进程表中移除。当系统下次重启时，僵尸进程会被清除。僵尸进程不会影响系统性能，你不需要删除它们。

当进程无法通过信号 15 终止时，使用信号 9 `SIGKILL` 强制进程终止。


注意，此示例的第一行将服务识别为 `rsync`。这与 `/etc/services` 文件中列出的服务名称完全匹配，导致该服务监听 TCP 和 UDP 协议的端口 873。你可以看到该服务默认是关闭的（`disable = yes`）。要启用 `rsync` 服务，请将该行改为：

`disable = no`

> 提示：如果你的机器是 FTP 服务器，那么开启 `rsync` 服务是一个很好的选择。它允许人们使用 `rsync` 客户端（包含校验和搜索算法）从你的服务器下载文件。有了该功能……

由于大多数服务默认都是禁用的，你的计算机的安全性完全取决于你如何设置。你可以通过确保在 `/etc/xinetd.d/login` 和 `rsh` 中设置了 `disabled = yes` 来双重检查不安全的服务（如 `login` 和 `rsh`，包含在 `rsh-server` 软件包中）也被禁用了。

> 提示：你可以让 `login` 服务处于激活状态但禁用使用 `/etc/hosts.equiv` 和 `.hosts` 文件，要求登录时始终提示密码。与其禁用服务，不如在 `rsh` 文件中找到服务器行（`server = /usr/sbin/in.rshd`），并在末尾添加一个空格和 `-L`。当然，这并没有改变你的密码和数据仍以未加密形式通过网络传输的事实。

你现在需要向 `xinetd` 进程发送一个信号，告诉它重新加载配置文件。最快的方法是重载 `xinetd` 服务。作为 root 用户，在 shell 中执行以下操作：

```
# service xinetd reload
```

Reloading configuration: [ OK ]

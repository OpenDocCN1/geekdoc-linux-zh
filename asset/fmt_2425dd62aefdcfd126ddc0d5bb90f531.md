
`chmod go-rwx /etc/httpd/conf/ssl.key/server.key`

以确保你的密钥设置了正确的权限。在使用上述命令创建密钥后，你将不再需要使用密码启动安全 Web 服务器。

![](img/8c5ce181a0f26bec693ad7f04bbfb6fe_562_0.png)

> 为你的安全 Web 服务器禁用密码功能存在安全风险。我们建议不要为你的服务器禁用密码功能。

不使用密码相关的问题与主机上维护的安全性直接相关。例如，一个破坏了主机上常规 UNIX 安全性的不法之徒可以获取你的私钥（`server.key`文件的文件的内容）。该密钥可能被用于提供看起来来自你服务器的 Web 页面。

如果主机计算机上严格遵守 UNIX 安全规范，所有更新在发布后都能立即安装，没有不必要或高风险的服务在运行等情况下，那么 Web 服务器的密码似乎是没必要的。然而，由于你的安全 Web 服务器不需要每次都重启，在大多数情况下，输入密码提供的额外安全性是值得的精力。

`server.key`文件应由系统上的 root 用户所有，并且不应让任何其他用户访问。制作此文件的备份副本并将备份副本保放在安全、可靠的地方。如果你在创建证书请求后丢失了`server.key`文件，你的证书将不再工作，CA 也无法帮助你。你唯一的选择将是请求（并支付）新证书。

如果你打算从 CA 购买证书，请继续下一节。如果你正在生成自己的自签名证书，请继续查看“创建自签名证书”部分。

## 生成发送给 CA 的证书请求

一旦创建了密钥，下一步就是生成你需要发送给所选择的 CA 的证书请求。确保你位于`/usr/share/ssl/certs`目录并输入以下命令：

```bash
make certreq
```

你的系统将显示以下输出并向你询问密码（除非你禁用了密码选项）：

```
umask 77 :
/usr/bin/openssl req -new -key /etc/httpd/conf/ssl.key/server.key -out /etc/httpd/conf/ssl.csr/server.csr
Using configuration from /usr/share/ssl/openssl.cnf
Enter PEM pass phrase:
```

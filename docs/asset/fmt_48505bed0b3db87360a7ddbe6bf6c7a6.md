
进入`/path/to/xxx`目录，找到`xxx.json`。

```bash
## cp cert.pem /etc/ssl/certs/sambacert.pem
## cp key.pem /etc/ssl/certs/sambakey.pem

# cd /etc/ssl/certs
# ln -s sambacert.pem `openssl x509 -noout -hash sambacert.pem`
# ls -l
total 24
lrwxrxr-x 1 root      root      13 Jan 13 01:14 19577ab1.0
  -> sambacert.pem
--rw-r--r-- 1 root      root      3544 Jan 13 01:12 sambacert.pem
--rw-r--r-- 1 root      root       561 Jan 13 01:12 sambakeyp.pem
```

你可能在奇怪为什么这个证书中有一个链接。该链接是证书的哈希值。当 `OpenSSL` 搜索该目录中的证书时，搜索哈希值比搜索每个证书的内容要快得多。你还需要添加 CA 的证书和私钥，以便验证 Samba 密钥：

```bash
# cd /usr/local/ssl/CA
# cp cacacert.pem /etc/ssl/certs
# cp private.pem /etc/ssl/certs
# cd /etc/ssl/certs
# ln -s cacacert.pem `openssl x509 -noout -hash sambacert.pem`
```

就是这些。现在的主题是：如何让 Samba 支持 SSL。

## 编译带 SSL 的 Samba

Samba 的功能最初基于免费提供的 SSL 实现，现在已演变为 `OpenSSL`。在继续之前，你必须安装 `OpenSSL`；由于不同国家的法律规定，分发包含 SSL 支持的 Samba 包变得非常复杂。如果你需要 SSL 支持，你需要自己编译 Samba。如果你不确定如何操作，请返回第 2 章“编译与安装”以刷新记忆。解压 Samba 后，进入源码目录。你需要运行脚本：

```bash
./configure --with-ssl --with-openssl=/usr/include/openssl
```

完成后，执行 `make`。完成后，运行 `make install`，它将把新的 Samba 配置安装到 `/usr/local/samba`。接下来你需要配置 Samba 以启用 SSL。你需要将 Samba 放入 `/usr/local/samba/smb.conf`。完成此操作，你需要在 `smb.conf` 中添加三个参数：

```ini
ssl = yes
ssl cert = /etc/ssl/certs/sambacert.pem
ssl key = /etc/ssl/certs/sambakey.pem
```

第一个参数表示你想为所有连接启用 SSL。第二个告诉 `smbd` 在哪里找到给客户端的证书。最后一个告诉 `smbd` 在哪里查找私钥。当你添加了这些行后，可以启动 `smbd`：

```bash
/usr/local/samba/bin/smbd
Enter passphrase:
```

输入证书上的密码，Samba 应该会在后台启动。你可以检查它正在运行：

```bash
ps -aux | grep smbd
root 10648 0.0 1.5 3104 1488 S 01:42 0 /usr/local/samba/bin/smbd
```

你可能还需要启动 `nmbd` 以提供浏览和名称解析服务：

```bash
/usr/local/samba/bin/nmbd
```

你的 Samba 服务器现在准备好进行 SSL 连接了！注意每次启动 Samba 都会提示此密码。这可能会很困扰，特别是当服务器自动重启（断电）后。如果是这样，服务器启动可能会停在那里直到在控制台输入密码。一个更好的选择（如果你有远程服务器）是不要将 Samba 放入启动，而是每次重启服务器时手动启动它。这不是理想方案，但至少在意外重启时不会出现服务器挂的问题。

## 使用带 SSL 的 Samba

你可以使用 `smclient` 连接 Samba 服务器上的资源来测试一切是否正常。可以通过以下方式正常启动 `smclient`：

```bash
smclient //daff/tmp
Added interface ip=192.168.66.6 bcast=192.168.66.15 mask=255.255.255.240
SSL: Certificate OK: /CA/ST=Canberra/CN=Matthew Willard/Email=matt@mycompany.com.au
SSL: Certificate OK: /CA/ST=Canberra/CN=Matthew Willard/Email=matt@mycompany.com.au
SSL: negotiated cipher: DES-CBC3-SHA
Password:
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.0.5]
smb: >
```

它告诉你 `smbd` 发送的证书确实是由你的 CA 签名的。如果你没有将 CA 证书和私钥拷贝到 `/etc/ssl/certs`，你会得到这个结果：

```bash
smclient //daff/tmp
Added interface ip=192.168.66.6 bcast=192.168.66.15 mask=255.255.255.240
```

## SAMBA 进阶

`SSL: Cert error unknown error 20 in /C=AU/ST=ACT/L=Canberra/CN=Matthew Willard/Email=matt@mycompany.com.au`

`SSL: negotiated cipher: DES-CBC3-SHA`

`Password:`

此错误意味着 `smclient` 无法验证 `sambacert.pem` 上的签名是否合法，因为它在 `/etc/ssl/certs` 中找不到 CA 证书。然而，你会发现 Samba 不是致命错误，并继续加密会话。后续版本的 Samba 行为可能会不同，请请注意。

最后一步是启用客户端证书。我们将此配置添加到已有的内容中。再次通过过程创建另一个私钥和证书：私钥 `smclientkey.pem` 和证书 `smclientcert.pem`。将它们拷贝到所在的目录，然后在添加的变量之后设置这些 SSL 变量：

```ini
ssl requirecert = yes
ssl client cert = /etc/ssl/certs/smclientcert.pem
ssl client key = /etc/ssl/certs/smclientkey.pem
ssl caDir = /etc/ssl/certs
```

第一个参数设置 Samba 要求客户端证书；否则它将不允许客户端连接。接下来两个指定证书和私钥的存放位置。最后一个是供 `smclient` 使用，以便 `smclient` 可以找到 CA 证书来验证 SSL 服务器在建立连接时发送的证书。如果你在完全不同的机器上设置 `smclient`，那么你只需要为 `smclient` 的 `smb.conf` 文件添加 `client cert`、`client key` 和 `ssl caDir`。这意味着在运行 SSL 版本 `smclient` 的所有机器上都需要安装 `OpenSSL`，以及 `acert.pem`、`cakey.pem` 和哈希链接。

现在你可以启动 `smclient`：

```bash
smclient //daff/tmp
Added interface ip=192.168.66.6 bcast=192.168.66.15 nmask=250

ter phrase:
```

注意，第一个要求的是你为 `smclient` 创建的私钥路径。这是为了让 `smclient` 能读取其锁定私钥。剩余会话将正常进行。唯一的区别在于你启用了客户端证书，因此你需要为所有想要连接的客户端生成证书。

## 其他 SSL smb.conf 参数

在 Samba 配置文件中，你可以设置许多其他 SSL 参数，所有参数都将在下面的章节中进行概述。将这些参数包含进来是为了为您提供参考。以下列表的设计目的是让您浏览所有参数，并决定哪些选项是您需要的，哪些是不需要的。

### ssl CA certDir

`ssl CA certDir` 参数是 Samba 查找受信任 CA（证书颁发机构）的地方。只有在 Samba 配置为验证客户端证书时才使用。该目录中的每个条目必须是根据 CA 的区分名（DN）创建的哈希值。

这是一个示例：

```
ssl CA certDir = /etc/ssl/certs
```

### ssl CA certFile

`ssl CA certFile` 参数是 `ssl CA certDir` 的替代方案。这次指定的是一个包含所有受信任 CA 证书的文件，证书按顺序一个一个排列。

这是一个示例：

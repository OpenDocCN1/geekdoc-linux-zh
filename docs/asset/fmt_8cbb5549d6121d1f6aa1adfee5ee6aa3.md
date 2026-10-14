
## 524 第 23 章 Apache 服务器管理

你现在可以使用 `https://` 访问服务器上的网页了。这对于测试是足够的，但不适用于其他任何用途。

接下来我们将创建一个自签名证书和密钥，这是向正确方向的一步。

要为证书生成密钥，请使用此命令：

```bash
matthew@semour:-$ openssl genrsa -des3 -out server.key 2048
```

这将使用三重 DES（Triple-DES）和 2048 位加密生成一个基础密钥。有关可能设置的更多信息，请查看 `openssl` 的 `man` 页。

要生成证书签名请求（CSR），使用此命令：

```bash
matthew@semour:-$ openssl req -new -key server.key -out server.csr
```

你将被要求输入一些信息以完成请求。

要创建一个自签名证书，使用此命令：

```bash
matthew@semour:-$ openssl x509 -req -days 365 -in server.csr -signkey server.key --out server.crt
```

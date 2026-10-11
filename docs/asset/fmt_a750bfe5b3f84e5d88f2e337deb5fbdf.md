
```
<Location /admin>
  AuthType Basic
  AuthClass System
  Order Deny. Allow
  Deny From All
  Allow From 127.0.0.1
  Allow From 10.0.0.5
</Location>
```

692

在地址为 `10.0.0.5` 的计算机上，输入以下内容（用 CUPS 服务器的名称或 IP 地址替换 `localhost`）：

```
http://localhost:631/admin
```

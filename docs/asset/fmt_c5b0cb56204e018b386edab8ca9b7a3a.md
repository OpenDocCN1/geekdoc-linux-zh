
`serverA` 的导出列表：
`usr/local` (`everyone`)

### 9. 设置客户端并验证 RPC
一旦您配置好了服务器，是时候设置客户端了。首先，检查客户端和服务器之间的 RPC 机制是否正常工作。您将再次使用 `showmount` 命令来验证客户端可以共享文件。如果客户端看不到共享部分，您可能存在网络问题或到服务器的权限问题。从 `clientA` 发出以下命令：

```bash
[master@clientA ~]$ showmount -e serverA
```

`serverA` 的导出列表：
`usr/local` (`everyone`)

### 10. 在客户端上挂载远程目录
一旦您验证服务器可访问，使用以下命令在客户端上挂载远程目录：

```bash
[master@clientA ~]$ sudo mount -t nfs serverA:/usr/local /mnt/usr/local
```

### 11. 使用 NFSv4 挂载
如果您在使用 NFSv4，可以使用以下命令：

```bash
[master@clientA ~]$ sudo mount -t nfs4 serverA:/usr/local /mnt/usr/local
```

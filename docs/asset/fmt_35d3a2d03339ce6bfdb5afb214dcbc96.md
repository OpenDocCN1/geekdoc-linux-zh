
# 第四部分：成为 Linux 服务器管理员

## 8. 在 NFS 客户端系统上创建用户

在 NFS 客户端系统上，使用 `useradd` 命令创建一个名为 `joe` 的用户。对于该命令行，你需要获取服务器上 `joe` 的 UID（在本例中为 `507`），以便客户端系统上的 `joe` 能够拥有来自 `joe` 的 NFS 家目录的文件。当你运行以下命令时，会创建 `joe` 用户账户，但你会看到一条声称家目录已存在的错误消息（这是正确的）：

```
# useradd -u 507 -c "Joe Smith" -d /home/remote/joe joe

# password joe

Changing password for user joe.

New password: *****

Retype new password: *****
```

## 9. 以 joe 身份登录并访问家目录

在 NFS 客户端系统上，以 `joe` 的身份登录。如果一切运行正常，当 `joe` 登录并尝试访问他的家目录 (`/home/remote/joe`) 时，目录 `/home/share/joe` 应该从 `mynfs.example.com` 服务器挂载。该 NFS 目录以读写且所有者 UID `507`（在两个系统上）的形式共享并挂载，本地系统上的用户 `joe` 应该能够在该目录下添加、删除、更改和查看文件。

在 `joe` 登出（实际上是当他停止访问该目录）一段时间（默认为 10 分钟）后，该目录将被卸载。

# 卸载 NFS 文件系统

挂载 NFS 文件系统后，卸载它非常简单。你使用 `umount` 命令配合本地挂载点或远程文件名。例如，这里有两种你可以从本地目录 `/mnt/maple` 卸载 `map:/stuff` 的方法：

```
# umount map:/stuff

# umount /mnt/maple
```

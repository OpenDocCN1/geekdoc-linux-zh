
`/my/shared/dir 192.168.0.4(rw)`

# 从 NFS 服务器导出共享目录

要在启动时从 NFS 服务器导出共享目录，首先需要启动 `nfsd` 守护进程。你可以使用 `chconfig` 命令在启动时启动 NFS 守护进程。但如果你想让 `/etc/exports` 文件列出的 NFS 目录立即供客户端可用，需要在 NFS 服务器的 shell 提示符处执行 `exports` 命令。

`exports` 命令更新 `/var/lib/nfs/stab` 文件并维护 NFS 导出文件系统表。当 NFS 客户端请求 NFS 共享目录时，`mountd` 守护进程会在 `/var/lib/nfs/stab` 文件中查找共享目录。`exports` 命令通过导出 NFS 共享目录来保持导出目录表的更新。

使用如下所示的 `exports` 命令导出目录：

```
/usr/sbin/exports -a -v .
```

`-a` 选项用于导出 `/etc/exports` 文件中的所有目录。`-v` 选项表示 `exports` 命令的详细输出。

- `rpc.nfs`
- `rpc.lockd`
- `rpc.statd`
- `rpc.mountd`
- `rpc.quotad`

配置 `/etc/exports` 文件后，你可以通过启动以下 NFS 守护进程来启动 NFS 服务器：

要验证 NFS 守护进程正在运行，请在 NFS 服务器计算机的 shell 提示符处执行 `exports` 命令：

```
# rpcinfo -p
```

如果你正确配置了 NFS 服务器，`rpcinfo` 命令将显示正在运行的 NFS 服务器守护进程，如下面的输出所示：

```
program vers proto port
100000  2   tcp     111     portmapper
100000  2   udp     111     portmapper
100024  2   udp     32768 status
100024  1   tcp     32770 status
391002  2   tcp     32772 sgi_fam
100011  1   udp     722     rquotad
100011  2   udp     722     rquotad
100011  1   tcp     722     rquotad
```

# 374 红帽 Linux — 学习指南

G3 组的计算机网络地址为 `192.168.0.0/255.255.255.0`。G2 组将测试数据保存在 NFS 服务器计算机 `linuxser.softwaredevelopers.com` 的 `/opt/swfiles` 文件夹中。同样，G1 组将接口文件保存在 NFS 服务器上的 `/opt/UIFiles` 文件夹中。此外，Prabhakar 计算机的主名为 `BlueSky`，IP 地址为 `192.168.0.53`。

- 1. 创建 NFS 共享目录并分配权限
- 2. 在 NFS 客户端创建挂载点并分配权限
- 3. 编辑 `/etc/exports` 配置文件
- 4. 重启 NFS 服务器
- 5. 验证 NFS 共享目录的访问

## 创建 NFS 共享目录并分配权限

要创建 NFS 共享目录并为其分配权限，你需要执行以下步骤：

- 1. 在 NFS 服务器计算机上创建目录 `/opt/swfiles` 和 `/opt/UIFiles`。
- 2. 使用 `chmod` 命令更改新创建的 `/opt/swfiles` 和 `/opt/UIFiles` 目录的权限，使得每个用户对该目录具有读取写权限。

## 在 NFS 客户端上创建挂载点并分配权限

要在 NFS 客户端上创建挂载点并为其分配权限，你需要执行以下步骤：

- 1. 在任何 NFS 客户端计算机上创建挂载点 `/tmp/softwarefiles`。
- 2. 使用 `chmod` 命令更改新创建的 `/tmp/softwarefiles` 权限，使得每个用户对该目录具有读取写权限。
- 3. 在 `Bluesky` 主机计算机上创建挂载点 `/tmp/UserInterfaceFiles`。
- 4. 使用 `chmod` 命令更改新创建的 `/tmp/UserInterfaceFiles` 权限，使得每个用户对该目录具有读取写访问权限。

## 编辑 `/etc/exports` 配置文件

要编辑 `/etc/exports` 配置文件，你需要执行以下步骤：

- 1. 使用编辑器打开 `/etc/exports` 文件。
- 2. 在 `/etc/exports` 文件中输入以下行，以赋予 G2 组读写权限：

```
/opt/swfiles    192.168.0.0/255.255.255.0(rw,sync)
```

- 3. 在 `/etc/exports` 文件中输入以下行，以赋予主机 `BlueSky` 上用户 `Graphey` 只读权限：

```
/opt/UIFiles      BlueSky(ro,sync)
```

- 4. 在配置 `/etc/exports` 文件后，文件的最终内容如下：

```
/opt/swfiles      192.168.0.0/255.255.255.0(rw,sync)
/opt/UIFiles      BlueSky(ro,sync)
```

- 5. 保存并关闭文件。

## 重启 NFS 服务器

你需要在 NFS 服务器的 shell 提示符执行以下命令来重启 nfs 进程：

```
# service nfs restart
```

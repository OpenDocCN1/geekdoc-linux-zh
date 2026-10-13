
## 自测题答案
### 网络文件系统（NFS）服务器
- 1. /etc/exports 中的以下条目将把 /data 目录以只读方式导出给所有主机，并向 example.com 域中的主机 super 授予读写权限：
  `/data *(ro, sync) super.example.com(rw, sync)`
- 2. 修改 /etc/exports 后，`exportfs -a` 命令会导出所有文件系统。是的，你可以用 `exportfs -r` 命令重新导出文件系统。但目前没有任何迹象表明 NFS 共享已被导出。
- 3. 与端口映射程序关联的端口号是 111。
- 4. 与 NFSv4 关联的端口号是 2049。
- 5. 支持 root 管理用户访问的 NFS 配置选项是 no_root_squash。

### 测试 NFS 客户端
- 6. 与 `soft` 和 `timeo` 选项相关的软挂载和超时可以防止 NFS 客户端出现诸如死锁之类的问题。
- 7. 可以显示指定远程系统 NFS 共享目录的命令是 `showmount -e outsider1.example.org`。

### 非常安全的 FTP 服务器
- 8. /etc/vsftpd/vsftpd.conf 中应禁用的默认指令，以防止用户通过 vsFTP 服务器登录其账户的是 `local_enable=YES`。
- 9. 防止普通用户在登录 vsFTP 服务器后访问顶层根目录（/）的指令是 `chroot_local_user=YES`。
- 10. 根据 RHEL 6 的默认配置，/etc/vsftpd 目录中的 ftpusers 和 user_list 都包含不允许登录 vsFTP 服务器的用户列表。严格来说，user_list 文件是正确答案，因为它与 userlist_enable 指令相关联。但标准 ftpusers 文件的活动内容是相同的。
- 11. 匿名访问的默认目录是名为 ftp 的用户的家目录。
- 12. 为允许使用 PAM 和 TCP wrappers 进行安全设置而添加到默认 vsFTP 配置文件中的额外指令是 `pam_service_name=vsftpd` 和 `tcp_wrappers=YES`。

## 实验答案
### 实验 1：基本 NFS 配置
完成本实验后，NFS 服务器系统上会出现以下功能：
- 已安装 NFS 软件包，包括相关软件包如 portreserve 和 rpcbind。没有这些软件包，就无法与 NFS 客户端通信。
- 活动的 NFSv4 服务，可通过 `rpcinfo -p` 命令的输出确认。
- 支持通过所注端口访问的防火墙。它还应通过 IP 地址网络进行限制。

此外，你将能够从 NFS 客户端执行以下任务：
- 运行 `showmount -e server1.example.com` 命令，其中 server1.example.com 是 NFS 服务器系统的名称（如有需要请替换）。
- 以 root 用户身份使用 `mount.nfs4 server1.example.com:/shared /testing` 命令挂载共享目录。
- 第一次挂载共享时，你应该能够以 root 用户身份将本地文件复制到 /testing 目录。
- 第二次挂载共享时，在 no_root_squash 指令生效的情况下，此类复制不应起作用，至少对于客户端 root 用户账户而言。

### 实验 2：标准 NFS 配置
本实验是为网络创建单个 /home 目录的第一步。一旦在单个客户端/服务器组合上使其工作，你就可以在所有客户端和服务器上设置它。然后你可以使用第 8 章中描述的 LDAP 服务器为网络设置单个 Linux/Unix 用户名和密码数据库。或者，在不同本地系统上匹配用户名（具有匹配的 UID 和 GID 编号）也应该有效。在 NFS 服务器上，执行以下步骤：
- 在用作 NFS 服务器的系统上设置几个用户和标识文件，例如 user1 和 user1.txt。
- 为当前域、适当用户和身份验证的转换方法配置 /etc/idmapd.conf 文件。如本章所述，这指的是
```
Domain = example.com
Nobody-User = nfsnobody
Nobody-Group = nfsnobody
Method = nsswitch
```
- 3. 使用 /etc/init.d/rpcidmapd 脚本使系统重新读取修改后的配置文件。
- 4. 在 server1.example.com 客户端的 /etc/exports 中共享 /home 目录。你可以在此文件中用以下命令执行此操作：
  `/home nfsclient (rw, sync)`
- 5. 使用以下命令导出此目录：
  `# exportfs -a`
- 6. 重新启动 NFS 服务：
  `# service nfs restart`
- 7. 确保导出的 /home 目录显示在导出列表中。在本地服务器上，你可以用以下命令执行此操作：
  `# showmount -e server1.example.com`
- 8. 如果在此过程中出现问题，请仔细检查 /etc/exports 文件。确保 /etc/exports 中没有多余的空格，即使在代码行的末尾。确保 NFS 服务实际上正在运行，使用 service nfs status 命令。
- 9. 你可能还想检查防火墙，并确保本章中描述的适当服务正在运行，使用 rpcinfo -p 命令。
- 10. 请记住确保 NFS 服务器在系统下次启动时自动启动。一种方法是使用以下命令：
  `# chkconfig nfs on`

现在在 NFS 客户端，执行以下步骤以连接到共享的 /home 目录：
- 1. 首先，对 /etc/idmapd.conf 文件做与服务器相同的更改，并重新启动从 /etc/init.d 目录可用的 rpcidmapd 服务脚本。
- 2. 确保你可以看到共享的 /home 目录。如果没有 DNS 服务器或 /etc/hosts 文件不包含 server1.example.com 系统的 IP 地址，请替换为 IP 地址：
  `# showmount -e server1.example.com`
- 3. 现在将提供的共享挂载到本地 /remote 目录：
  `# mount.nfs4 server1.example.com:/home /remote`
- 4. 检查挂载是否成功。如果成功，你将在 mount 命令的输出中看到 NFS 挂载。
- 5. 现在查看已挂载的 /home 目录，查找在步骤 1 中创建的特殊文件。如果找到，你已成功创建并连接到 /home 目录共享。
- 6. 要使挂载永久化，请将其添加到客户端的 /etc/fstab 文件中。一旦你在该文件中添加了如下行，Linux 客户端将自动从 NFS 服务器挂载共享的 /home 目录。
  ```
  server1.example.com:/home /remote nfs4 soft,timeout=100 0 0
  ```

### 实验 3：NFS 和 SELinux
对 SELinux 的引用是有意的，应该提供一个重要的提示。如果必须修改每个 NFS 服务器上 /etc/exports 文件中共享和配置的每个目录，那会很耗时。也许防止写入共享 NFS 目录的最简单方法就是停用相关的 SELinux 布尔设置。虽然还有其他方法，但永久这样做的最快方法是使用以下命令：
```
# setsebool -P nfs_export_all_rw off
```
然后你应该能够通过下一次挂载共享 NFS 目录来测试结果。

### 实验 4：配置带消息的 vsFTP 服务器
vsFTP 服务器可以从一个 RPM 软件包安装。因此，如果你之前未安装此服务器，可以使用以下命令安装：
```
# yum install vsftpd
```
这也将在 /etc 和 /etc/vsftpd 目录中安装配置文件。主要的配置文件是 /etc/vsftpd/vsftpd.conf。基于此文件的 RHEL 默认版本，你可以做一些更改来启用消息。但默认情况下，消息已为 FTP 服务器上的目录访问启用，归功于以下命令：
```
dirmessage_enable=yes
```
消息的实际配置是创建文本文件并将其保存为 .message，保存在所需目录 /var/ftp 和 /var/ftp/pub 中。你可以添加一行简单的文字，例如“root directory for the FTP server”或“main download directory。”

最后，要配置 Red Hat FTP 服务器启动，请运行 `service vsftpd start` 命令。要确保下次启动计算机时它启动，请运行 `chkconfig vsftpd on` 命令。

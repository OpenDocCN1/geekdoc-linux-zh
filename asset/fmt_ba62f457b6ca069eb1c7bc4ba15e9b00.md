
## 启动 NFS 安全服务器

```bash
[root@quebec ~]# systemctl start nfs-secure-server
```

## 导出目录

我们使用 `exportfs` 导出目录。

```bash
[root@quebec ~]# exportfs -av
```

`SECURE_NFS`

## 防火墙配置

我们在防火墙中添加 NFS 服务。

```bash
[root@quebec ~]# firewall-cmd --add-service=nfs
[root@quebec ~]# firewall-cmd --permanent --add-service=nfs
```

## 客户端配置

在客户端计算机上，创建挂载点并启动 NFS 服务。

```bash
[root@romeo ~]# mkdir /mnt/secure_nfs
[root@romeo ~]# systemctl start nfs
```

接下来更新本地 keytab 文件并挂载目录。

```bash
[root@romeo ~]# ipa-keytab -s quebec.linuxaholics.local nfs/quebec.linuxaholics.local /etc/krb5.keytab
Keytab successfully retrieved and stored in: /etc/krb5.keytab
[root@romeo ~]# mount -t nfs4 -o sec=krb5 quebec.linuxaholics.local:/SECURE_NFS /mnt/secure_nfs/
[root@romeo ~]# ls /mnt/secure_nfs/
kerberized.txt
```

## 自动挂载

如果我们希望系统启动时自动挂载该目录，需要在 `/etc/fstab` 中添加相应的行。

```
quebec.linuxaholics.local:/NFS /mnt/secure_nfs nfs _netdev,sec=krb5 0 0
```

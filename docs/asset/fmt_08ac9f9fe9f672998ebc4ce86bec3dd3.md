
88C7 6B72 51F5 5094 3D8A BC68 BBEB BBEF3

9063 A7E5 8B57 09F9 DC0B FFA4 E32C A1F7 8E2E9

74C4 0E10 E62D 89A7 0845 0087 169A 0676 E77F

5713

```
[@server1] ls -l ~/.ssh/
-rw------- 1 michael 1822 22 Jan 21:43 authorized_keys
-rw-r---- 1 michael 227 22 Sep 28:29 id_cdsa
-rw-r--r-- 1 michael 185 12 Sep 28:29 id_cdsa.pub
-rw-r--r-- 1 michael 1657 079 Nov 7 18:24 id_rsa
-rw-r--r-- 1 michael 486 04 Nov 7 18:24 id_rsa.pub
-rw------- 1 michael 346 01 Jan 21:44 know_hosts
[@server1] - $ 
```

图 8-3
用户 `.ssh/` 子目录中的密钥

https://t.me/CCNA_SECURITY
https://t.me/CCNPSECURITY

## 327 使用密钥认证加固 SSH

私钥的情况类似，但你必须保持其私密性，否则整个系统都会失效。保持私密意味着除了所有者之外，没有人应该访问该密钥。如果你的电脑是公共计算机，请使用短语（密码）保护你的私钥。下文将描述设置短语的步骤。不要忘记短语，否则你将创建一个新的密钥对，并将你的公钥复制到所有目标系统。

### 设置基于密钥认证的私/公钥对

`ssh-keygen` 命令用于设置公钥/私钥对。虽然它默认创建 RSA 密钥，但也可以用于创建 DSA 密钥或 ECDSA 密钥。例如，某些用户需要 DSA 密钥以符合某些美国政府标准。命令序列的示例如图 8-4 所示。

所示，命令会提示可选的短语以保护私钥。当确认相同的短语时，私钥将保存在 `id_rsa` 文件中，相应的公钥将存储在 `id_rsa.pub` 文件中。用户 `michael` 的两个文件都存储在 `/home/michael/.ssh` 目录。

如果需要，你可以设置位数更大的 RSA 密钥。在我们的测试中，我们能够很快地设置 8192 位的密钥对，即使在只有一个虚拟 CPU 的虚拟机系统上也是如此。启动该过程的命令是

```
$ ssh-keygen -b 8192
```

或者，如果需要 DSA 密钥，可以使用以下命令。只允许 1024 位的 DSA 密钥。此命令后的过程与图 8-4 所示。

所示，命令会提示可选的短语以保护私钥。当确认相同的短语时，私钥将保存在 `id_rsa` 文件中，相应的公钥将存储在 `id_rsa.pub` 文件中。用户 `michael` 的两个文件都存储在 `/home/michael/.ssh` 目录。

如果需要，你可以设置位数更大的 RSA 密钥。在我们的测试中，我们能够很快地设置 8192 位的密钥对，即使在只有一个虚拟 CPU 的虚拟机系统上也是如此。启动该过程的命令是

```
$ ssh-keygen -b 8192
```

或者，如果需要 DSA 密钥，可以使用以下命令。只允许 1024 位的 DSA 密钥。此命令后的过程与图 8-4 所示。

所示，命令会提示可选的短语以保护私钥。当确认相同的短语时，私钥将保存在 `id_rsa` 文件中，相应的公钥将存储在

```
$ ssh-keygen -t dsa

Generating DSA public key pair.

Enter file to save the key (/home/michael/.ssh/id_dsa):

Enter passphrase (empty for no protection):

Your key has been saved in /home/michael/.ssh/id_dsa

Your public key has been saved in /home/michael/.ssh/id_dsa.pub

Fingerprint of /home/michael/.ssh/id_dsa: SHA256:v6X...
```

# 330 第 8 章 Linux 安全

图 8-6 不同文件的 SELinux 安全上下文

```
[root@server1 # ls -l /

total 28

dr-xr-xr-x 2 root root u:object_root_t:0 6 Aug  9 2021 efs

dr-xr-xr-x 5 root root u:object_bin_t:0 7 Aug  9 2021 bin-> /usr/bin

dr-xr-xr-x 5 root root u:object_root_t:0 4096 Jan 25 15:36 boot

dr-xr-xr-x 21 root root u:object_device_t:0 3480 Mar 30 18:59 dev

dr-xr-xr-x 135 root root u:object_etc_t:0 8192 Apr 30 18:22 etc

dr-xr-xr-x 18 root root u:object_home_t:0 124 Jan 27 05:18 home

dr-xr-xr-x 1 root root u:object_lib_t:0 6 Aug  9 2021 lib-> /usr/lib

dr-xr-xr-x 12 root root u:object_lib64_t:0 9 Aug  9 2021 lib64-> /usr/lib64

dr-xr-xr-x 2 root root u:object_media_t:0 6 Aug  9 2021 media

dr-xr-xr-x 2 root root u:object_mnt_t:0 6 Aug  9 2021 mnt

dr-xr-xr-x 303 root root u:object_proc_t:0 0 Apr 30 18:59 proc

dr-xr-xr-x 8 root root u:object_admin_t:0 4096 May  1 04:36 admin

dr-xr-xr-x 45 root root u:object_run_t:0 1228 May  1 14:31 run

dr-xr-xr-x 12164 root root u:object_sbin_t:0 6 Aug  9 2021 sbin-> /usr/sbin

dr-xr-xr-x 13 root root u:object_sysfs_t:0 0 Apr 30 18:59 sys

drwxrxrwt. 26 root root u:object_tmp_t:0 4096 May  1 04:37

dr-xr-xr-x 12 root root u:object_usr_t:0 144 Jan 25 15:15 usr

dr-xr-xr-x 20 root root u:object_var_t:0 4096 Jan 25 15:36 var
```

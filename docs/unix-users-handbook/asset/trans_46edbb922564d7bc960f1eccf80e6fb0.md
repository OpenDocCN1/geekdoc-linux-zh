
19.32.23.112:temp  2096160  1523360  572800  73% /ntmount
# cd /ntmount
# ls
_istmp0.dir           ~dfbcec8.tmp    ~dfd65e.tmp
_istmp1.dir           tt2.exe         ~dfeee7.tmp    ~dfd65f.tmp
_istmp2.dir           tt3.exe         ~dfa393.tmp    ~dfd660.tmp
1e401splt.exe         ttdemo.zip      ~dfa394.tmp    ~dfd66b.tmp
1e4setup.exe          ttwiz(1).exe    ~dfa3a3.tmp    ~dfd66c.tmp
jack.log              wbemcore.exe    ~dfa3a4.tmp    ~dfe649.tmp
jack1.log             winzip70.exe    ~dfb2a.tmp     ~dfe64a.tmp
jack2.log             ~df7e2f.tmp    ~dfb39.tmp     ~dfe64b.tmp
mmc14.tmp             ~df7e40.tmp    ~dfb3a.tmp     ~dfe64c.tmp
mmcaa7.tmp            ~df7e41.tmp    ~dfd63c.tmp    ~dfe659.tmp
mmcaaad.tmp           ~df7e42.tmp    ~dfd63d.tmp    ~dfe65a.tmp
mmcaabl.tmp           ~df7e4f.tmp    ~dfd63f.tmp    ~dfe65b.tmp
nph-nftfinal.exe      ~df7e50.tmp    ~dfd64d.tmp    ~dfe65c.tmp
ntag33e.exe           ~df7e51.tmp    ~dfd64e.tmp    ~dfe65d.tmp
ntoption.exe          ~df7e52.tmp    ~dfd64f.tmp    ~dfe669.tmp
sfu                   ~df7e53.tmp    ~dfd65b.tmp
sfu1                  ~df8e99.tmp    ~dfd65e.tmp
temp.log              ~df8ea9.tmp    ~dfd65d.tmp

![](img/75f39fc91296b889c0653851accdfd46_1282_0.png)

![](img/75f39fc91296b889c0653851accdfd46_1282_1.png)

发出此命令后，我们可以在 UNIX 系统上看到 **/ntmount** 是挂载的文件系统之一。此时，我切换到了非 root 用户，因为通常不建议 root 用户在 NFS 挂载的文件系统上操作文件。我切换到了用户 *hp*。我们可以更改目录到 /ntmount 并查看其内容，这些内容对应于 Windows 系统下 **C:\temp** 中的内容。发出长目录列表命令后，我们可以看到拥有者为 *hp* 的文件：

```
$ ll
total 5710
drwxrwxrwx  2 hp users          64 Feb  9 17:58 _istmp0.dir
drwxrwxrwx  3 hp users          96 Feb  2 10:18 _istmp1.dir
drwxrwxrwx  2 hp users          64 Feb  2 10:19 _istmp2.dir
-rwxrwxrwx  1 hp users        24227193 Feb  1 19:50 1e401splt.exe
-rwxrwxrwx  1 hp users         443160 Jan 10 10:21 1e4setup.exe
-rwxrwxrwx  1 hp users          218 Feb 10 19:99 jack.log
-rwxrwxrwx  1 hp users          218 Feb 10 19:99 jack1.log
-rwxrwxrwx  1 hp users          218 Feb 10 19:99 jack2.log
-rwxrwxrwx  1 hp users          60414 Feb  2 15:26 mmc14.tmp
-rwxrwxrwx  1 hp users         102400 Feb  9 09:24 mmcaa7.tmp
-rwxrwxrwx  1 hp users         102400 Feb  9 12:40 mmcaaad.tmp
-rwxrwxrwx  1 hp users         102400 Feb  9 12:40 mmcaabl.tmp
-rwxrwxrwx  1 hp users         464200 Feb  1 19:33 nph-nftfinal.exe
-rwxrwxrwx  1 hp users         5514240 Feb  1 17:43 ntag33e.exe
-rwxrwxrwx  1 hp users        38940572 Feb  1 20:07 ntopion.exe
drwxrwxrwx 20 hp users           640 Feb  3 09:58 sfu
drwxrwxrwx  5 hp users           160 Feb 10  1999 sfu1
-rwxrwxrwx  1 hp users          218 Feb  2 11:34 temp.log
```

```
-rw-rw-rw- 1 hp users 35 Feb 1 19:48 test.html
-rw-rw-rw- 1 hp users 7046429 Feb 1 20:19 tt2.exe
-rw-rw-rw- 1 hp users 5758110 Feb 1 20:21 t3.exe
-rw-rw-rw- 1 hp users 3232301 Feb 3 15:18 tddemo.zip
-rw-rw-rw- 1 hp users 1086772 Feb 1 15:53 twwiz11l.exe
-rw-rw-rw- 1 hp users 3456925 Feb 1 19:55 wbmcro.exe
-rw-rw-rw- 1 hp users 943949 Feb 3 15:51 winzip70.exe
-rw-rw-rw- 1 hp users 4096 Feb 2 15:26 -dff2ef.tmp
-rw-rw-rw- 1 hp users 3584 Feb 2 15:26 -dff40.tmp
-rw-rw-rw- 1 hp users 3584 Feb 2 15:26 -dff41.tmp
-rw-rw-rw- 1 hp users 3584 Feb 2 15:26 -dff42.tmp
-rw-rw-rw- 1 hp users 3072 Feb 2 15:26 -dff44.tmp
-rw-rw-rw- 1 hp users 3072 Feb 2 15:26 -dff46.tmp
-rw-rw-rw- 1 hp users 3584 Feb 2 15:26 -dff4e0.tmp
-rw-rw-rw- 1 hp users 3584 Feb 2 15:26 -dff4e2.tmp
-rw-rw-rw- 1 hp users 3584 Feb 2 15:26 -dff4e3.tmp
-rw-rw-rw- 1 hp users 9728 Feb 9 09:24 -dff8e9.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff8e9.tmp
-rw-rw-rw- 1 hp users 5120 Feb 9 09:24 -dff8e9.tmp
-rw-rw-rw- 1 hp users 3584 Feb 9 09:24 -dff8e7.tmp
-rw-rw-rw- 1 hp users 6144 Feb 9 09:24 -dfa393.tmp
-rw-rw-rw- 1 hp users 9728 Feb 2 15:26 -dfa394.tmp
-rw-rw-rw- 1 hp users 3072 Feb 2 15:26 -dfa3a3.tmp
-rw-rw-rw- 1 hp users 5120 Feb 2 15:26 -dfa3a4.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff2a.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff39.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff3a.tmp
-rw-rw-rw- 1 hp users 4608 Feb 9 09:24 -dff63c.tmp
-rw-rw-rw- 1 hp users 16384 Feb 9 09:24 -dff63d.tmp
-rw-rw-rw- 1 hp users 4608 Feb 9 09:24 -dff64c.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff64d.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff64e.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff64f.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff65b.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff65c.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff65d.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff65e.tmp
-rw-rw-rw- 1 hp users 8192 Feb 9 09:24 -dff660.tmp
-rw-rw-rw- 1 hp users 4608 Feb 9 09:24 -dff66b.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff66c.tmp
-rw-rw-rw- 1 hp users 4096 Feb 9 09:24 -dff649.tmp
-rw-rw-rw- 1 hp users 3584 Feb 9 09:24 -dff64a.tmp
-rw-rw-rw- 1 hp users 3584 Feb 9 09:24 -dff64b.tmp
-rw-rw-rw- 1 hp users 3584 Feb 9 09:24 -dff64c.tmp
-rw-rw-rw- 1 hp users 3584 Feb 9 09:24 -dff659.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff65a.tmp
-rw-rw-rw- 1 hp users 3072 Feb 9 09:24 -dff65b.tmp
-rw-rw-rw- 1 hp users 3584 Feb 9 09:24 -dff65c.tmp
-rw-rw-rw- 1 hp users 3584 Feb 9 09:24 -dff65d.tmp
-rw-rw-rw- 1 hp users 3584 Feb 9 09:24 -dff669.tmp
$ 
```

确实可以看到，用户 *hp* 和对应的组 *users* 出现在这个长目录列表中。

本节中我们配置的 NFS 服务器可以与之前执行的 NFS 客户端配置结合使用，以便将 Windows 文件系统作为 NFS 服务器的一部分导出，并作为 NFS 客户端的一部分导入。您在文件共享策略中使用 NFS 的程度取决于您的环境构成。由于 NFS 在大多数 UNIX 变体上可用，您可能会发现在 Windows 上使用 NFS 适合您的环境。如果您预计在混合的 Windows 和 UNIX 环境中会有大量使用 NFS，您可能希望从小处开始，使用 NFS 共享几个关键目录，并测试其性能，以确保它满足用户的使用需求。如您从前面的示例所见，在 Windows 上使用 NFS 可以极大地增强混合 Windows 和 UNIX 环境中的整体文件共享能力。

## 密码同步

SFU 将 Windows 密码同步到 UNIX。我没有包含此同步过程的示例。有一个加密文件从 Windows 发送到 UNIX，其中包含密码信息。该文件应设置为仅 root 可读。还有一个守护进程需要实现密码同步。设置完成后，UNIX 上的用户密码将与 Windows 上的密码保持同步。

# 第 19 章

# Windows 命令行：NET 命令、POSIX 实用程序及其他

### UNIX 系统管理员引言

UNIX 系统管理主要在命令行上进行。虽然有非常好的系统管理接口，可以执行许多例行的系统管理任务，但对于大多数 UNIX 系统管理员来说，命令行仍然是先于任何图形工具使用的。对于 Windows 则恰恰相反。在 Windows 中，大多数系统管理功能是通过“指点点击”来执行的。然而，在 Windows 的命令行上也有许多可以执行的功能。在本 UNIX 和 Windows 互操作性章节中，我将总体介绍 Windows 命令行，并特别介绍一组提供 Windows 中 UNIX 功能的 POSIX 实用程序。

我将从 Windows“NET”命令开始介绍，这些是 Windows 的系统管理命令。然后，我将介绍您可以在 Windows 命令行上运行的 POSIX 命令，这些命令在 Windows 中提供 UNIX 功能，例如 grep、ls 等。接着，我将介绍一些额外的 Windows 命令，您可以使用它们执行诸如备份和在特定时间运行命令等任务。

![](img/75f39fc91296b889c0653851accdfd46_1286_0.png)

![](img/75f39fc91296b889c0653851accdfd46_1286_1.png)


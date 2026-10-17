
Running Oracle8 script...

以下环境变量设置如下：
`ORACLE_OWNER`= oracle
`ORACLE_HOME`=`/u01/app/oracle/product/8.0.5`
`ORACLE_SID`= orcl

Are these settings correct (Y/N)? [Y]:

输入本地 bin 目录的完整路径 [/usr/bin]: `/usr/local/bin`

Checking for "oracle" user id...
`ORACLE_HOME` does not match the home directory for oracle.

Okay to continue? [N]: Y
Replacing existing entry for SID in `/etc/oratab`...
nThe previous entry is now in a comment.

Leaving common section of Oracle8 root.sh.

## 安装补丁

安装 Oracle8 后，你需要安装补丁。如果你还没有下载补丁，它们位于 `ftp://oracle-ftp.oracle.com/server/patchsets/unix/LINUX/80patch805110/`。如果你需要 `glibpatch.tgz` 补丁，它不在上述站点，你需要在 Oracle Technology Network (`http://technet.oracle.com`) 获取一个免费账户并找到 Linux 的软件部分。检查新补丁发布。目前 Oracle8 有三个补丁：`glibcpatch.tgz`、`lnxpatch.tgz`，且 `glibcpatch.tgz` 文件仅在 Red Hat 6.0 或更高版本上安装 Oracle 8.0.5 时需要。在安装后续补丁后，可能需要重新安装 `glibcpatch`。如果你在 Red Hat 5.2 机器上安装，则不需要。`lnxpatch.tgz` 包含了针对 Linux 平台的补丁。`linux80510patchset.tgz` 包含 Oracle8 的通用修复。你应该阅读补丁随附的任何文档。

### lnxpatch
`lnxpatch` 是一个 shell 脚本。

- 1. 进入包含补丁的目录。
- 2. 创建一个目录 `lnx`。
- 3. 将 `lnxpatch.tgz` 文件移动到 `lnx` 目录。

```
mv lnxpatch.tgz lnx
```

- 1. 进入 `lnx` 目录。

```
cd lnx
```

- 1. 解压缩补丁。

```
zxvf lnxpatch.tgz
```

- 1. 运行 `lnxpatch.sh` 脚本。

```
glibcpatch.sh
```

## 80510patchset

80510patchset 通过你用于安装 Oracle 服务器的安装程序 `orain` 进行安装。

- 1. 创建一个名为 `80510` 的目录
- 2. 将 `80510patchset.tgz` 文件移动到 `80510` 目录。

```
mv 80510patchset.tgz 80510
```

- 1. 进入 `lnx` 目录。（注：原文此处为 lnx，可能为逻辑笔误）

```
cd lnx
```

- 1. 解压缩补丁。

```
zxvf lnxpatch.tgz
```

- 1. 运行 `lnxpatch.sh` 脚本。

```
glibcpatch.sh
```

## 80510patchset
80510patchset 通过安装程序 `orain` 安装，即你安装 Oracle 服务器时使用的那个程序。

- 1. 创建一个名为 `80510` 的目录
- 2. 将 `80510patchset.tgz` 文件移动到 `80510` 目录。

```
mv 80510patchset.tgz 80510
```

- 1. 进入 `lnx` 目录。

```
cd lnx
```

- 1. 解压缩补丁。

```
zxvf lnxpatch.tgz
```

- 1. 运行 `lnxpatch.sh` 脚本。

```
glibcpatch.sh
```

## 80510patchset
80510patchset 通过安装程序 `orain` 安装，即你安装 Oracle 服务器时使用的那个程序。

- 1. 创建一个名为 `80510` 的目录
- 2. 将 `80510patchset.tgz` 文件移动到 `80510` 目录。

80510patchset
80510patchset 通过安装程序 `orain` 安装，即你安装 Oracle 服务器时使用的那个程序。

- 1. 创建一个名为 `80510` 的目录
- 2. 将 `80510patchset.tgz` 文件移动到 `80510` 目录。

```
mv 80510patchset.tgz 80510
```

- 1. 进入 `lnx` 目录。

```
cd lnx
```

- 1. 解压缩补丁。

```
zxvf lnxpatch.tgz
```

- 1. 运行 `lnxpatch.sh` 脚本。

- 1. 进入 `lnx` 目录。

- 1. 解压缩补丁。

```
zxvf lnxpatch.tgz
```

- 1. 运行 `lnxpatch.sh` 脚本。

```
glibcpatch.sh
```

## 80510patchset
80510patchset 通过安装程序 `orain` 安装，即你安装 Oracle 服务器时使用的那个程序。

- 1. 创建一个名为 `80510` 的目录
- 2. 将 `80510patchset.tgz` 文件移动到 `80510` 目录。

```
mv 80510patchset.tgz 80510
```

- 1. 进入 `lnx` 目录。

```
cd lnx
```

- 1. 解压缩补丁。

```
zxvf lnxpatch.tgz
```

- 1. 运行 `lnxpatch.sh` 脚本。

```
glibcpatch.sh
```

## 80510patchset
80510patchset 通过安装程序 `orain` 安装，即你安装 Oracle 服务器时使用的那个程序。

- 1. 创建一个名为 `80510` 的目录
- 2. 将 `80510patchset.tgz` 文件移动到 `80510` 目录。

```
mv 80510patchset.tgz 80510
```

- 1. 进入 `lnx` 目录。

```
cd lnx
```

- 1. 解压缩补丁。

```
zxvf lnxpatch.tgz
```

- 1. 运行 `lnxpatch.sh` 脚本。

```
glibcpatch.sh
```

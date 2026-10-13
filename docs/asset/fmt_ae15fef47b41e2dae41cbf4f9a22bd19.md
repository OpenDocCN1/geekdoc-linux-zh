
## 属性

有关以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| --- | --- |
|可用性 | SUNWnisu |

## ypmatch

## 参见

`ypmmatch(1)`, `ypfiles(4)`, `attributes(5)`

## ypmatch — 打印 NIS 映射中键的值

### 概要

`/usr/bin/ypmatch [-k] [-t] [-d domain] key [key...] mname`
`ypmatch -x`

### 描述

`ypmatch` 打印与由 `mname` 指定的 NIS 命名服务中的一个或多个键相关的值，其中 `mname` 可以是映射名称，也可以是映射别名。

你可以指定多个键。所有键都将在同一个映射中搜索。键必须具有相同的大小写和长度。不支持模式匹配。如果键未匹配，则将显示诊断消息。

> 注意 — 如果可用的文件描述符不足，`ypmatch` 在执行 `yp` 操作时会带有 RCP 错误消息。如果发生此问题，请增加文件描述符的数量。

### 选项

- `-d domain` 指定一个默认域之外的域。
- `-k` 在打印键的值之前，先打印键本身，后跟一个冒号 `(:)`。
- `-t` 抑制映射别名翻译。
- `-x` 显示映射别名表。此选项列出了命令已知的别名 `mnames`，并指示与每个别名关联的映射名称。

### 操作数

`mname` NIS 命名服务映射。

### 退出状态

- `0` 操作成功。
- `1` 发生错误。

## 属性

有关以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| --- | --- |
|可用性 | SUNWnisu |

## 参见

`ypcat(1)`, `ypfiles(4)`, `attributes(5)`

## ypasswd — 修改 NIS 数据库中的网络密码

### 概要

```
/usr/bin/bypasswd [username]
```

### 描述

> 注意 — 不建议使用 `yppasswd`，因为它仅仅是 `passwd(1)` 命令的链接，你应该改使用它。使用带有 `-r nis` 选项的 `passwd(1)` 可以实现相同的结果，并在所有可用的命名服务中保持一致。

`bypasswd` 修改与网络信息服务 `NIS+` 数据库中用户 `username` 关联的网络密码。如果用户已执行过 `loginkey(1)`，且 NIS 映射中存在该用户的 `publickey/secretkey`，则 `yppasswd` 还会用新密码重新加密密钥。NIS 密码可能与你的本地密码不同。使用 `passwd(1)` 修改本地机器上的密码信息，使用 `npasswd(1)` 修改存储在网络信息服务第 3 版 `NIS+` 中的密码信息。

`bypasswd` 会提示旧的 NIS 密码，然后是新密码。你必须正确输入旧密码更改才能生效。你必须输入两次新密码进行验证。

如果使用的字母集足够丰富，新密码必须至少为四个字符；如果是小写字母，则至少为六个字符。如果你足够固执，这些规则将会放宽。只有用户所有者或超级用户才能更改密码；根主服务器上的超级用户会被提示旧密码，且不需要遵循密码构造要求。

NIS 密码进程 `rpc.bypasswdd` 必须在你的 NIS 服务器上运行，新密码才能生效。

## ypwhich

**警告** — 即使你使用此命令成功更改了密码，只有当你的密码和影子信息是从 NIS 获取时，后续使用新密码的 `login(1)` 才会成功。（参见 `getpwnam(3C)`, `getspnam(3C)` 和 `nswitch.conf(4)`）。

## 属性

有关以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
|---|---|
|可用性 | SUNWcsu |

## 参见

`keylogin(1)`, `login(1)`, `nispwd(1)`, `passwd(1)`, `getpwnam(3C)`, `getspnam(3C)`, `secure_rpc(3N)`, `nswitch.conf(4)`, `attributes(5)`

### 缺陷

NIS 密码进程 `rpc.bypasswdd` 必须在你的 NIS 服务器上运行，新密码才能生效。

## ypwhich — 返回主节点

### 概要

```
/usr/bin/ypwhich [-d domain] [-m mname] hostname
```

### 描述

`ypwhich` 返回 NIS 服务器名称。如果指定了 `hostname`，它返回该主机的映射。如果不带参数调用，它返回主节点。

### 选项

- `-d domain` 使用指定的域来代替默认域。
- `-m mname` 查找映射。
- `-t` 抑制翻译。
- `-x` 显示别名表。（等等，根据上下文 `-x` 在这里是）

## 属性

有关以下属性的描述，请参见 `attributes(5)`：

| 属性类型 | 属性值 |
|---|---|
|可用性 | SUNWnis |

## 参见

`ypfiles(4)`, `attributes(5)`

## zcat — 压缩、解压缩或显示文件

### 概要

`/usr/bin/zcat [file...]`

### 描述

参见 `compress(1)`。

## zipinfo — 列出压缩文件的详细信息

### 概要

`/usr/bin/zipinfo [-Z12smvlTz]file[.zip]`

### 描述

注意 — `zipinfo` 在 Unix 下与 `unzip` 是同一个程序；但在某些系统上，`zipinfo` 可能会省略某些信息。

`zipinfo` 列出存档文件的技术信息。默认行为（指定文件时不带选项）是列出每个文件的单行条目，并带有头部和总结。

```
castle# 085DS

Archive: 085DS.zip 10672 bytes 4 files

-rw-a-- 2.0 fat 67072 b-defn 18-Aug-98 21:55 085X0.DOC

-rw-a-- 2.0 fat 63872 b-defn 22-Aug-09 01:39 085X02.DOC

-rw-a-- 2.0 fat 95232 t-defn 31-Aug-98 20:29 085X02.DOC

-rw-a-- 2.0 fat 63488 t-defn 4-Oct-98 20:24 085X04.E

castle#
```

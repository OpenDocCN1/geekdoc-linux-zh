
你可以通过在运行级别中选择服务，然后为 Red Hat Linux 级别添加、删除或编辑特定运行级别下服务的启动顺序，从而管理各种服务。

# Red Hat 图形化管理工具

## 第 19 章

### 图 19.8

`tksys` 工具是一个用于自定义 Linux 系统服务的方便界面。

| 变量 | 2 | 3 | 4 | 5 |
|---|---|---|---|---|
| and | apend | apend | apend | apend |
| apmd | network | network | network | network |
| arpwho | S | S | S | S |
| atd | crying | nets | nets | nets |
| ald | a | random | random | random |
| audits | | | at | at | at |
| bondman | | | | | |
| crond | | crond | crond | crond | crond |
| cups | | | | | |
| outputs | | | | | |
| gated | | | | | |
| ham | | | | | |
| http | | | | | |
| insert | | | key-table | | |
| inet | | | | | |
| ind | | | | | |
| add | | | | | |
| remove | | | | | |
| edit | | | | | |
| execute | | | | | |

# 使用 hkconfig 命令检查级别

另一个可以配合 `tksys` 使用的方便 Red Hat 工具是 `hkconfig` 命令，它不需要 X 环境，可以在控制台的命令行中使用，并报告如 `tksys` 所示的服务状态。`hkconfig` 命令也可以像 `tksys` 一样，添加或删除新服务、列出每个层级的每个服务、配置级别或检查系统服务。例如，要查看系统的当前状态以及每个级别启动或停止了哪些服务，请使用 `hkconfig --list` 选项：

```bash
# hkconfig --list
amd 0:off 1:2off 2:3off 3:4on 4:5on 5:6off
httpd 0:off 1:2off 2:3off 3:4on 4:5on 5:6off
apmd 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
arp 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
atd 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
autofs 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
nabled 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
named 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
bootparam 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
keytable 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
crond 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
syslo 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
sysfs 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
network 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
random 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
xfs 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
dhcp 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
gated 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
gpm 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
innd 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
pcm 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
nfs 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
```

![](img/fbfff30e42d507bc7531108a281d6cf4_630_png)

# 系统管理

## 第三部分

```bash
linuxconf 0:off 1:2off 2:3off 3:4on 4:5on 5:6off
lpd 0:off 1:2off 2:3off 3:4on 4:5on 5:6off
mars-we 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
mcscserv 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
inet 0:off 1:2off 2:3on 3:4on 4:5on 5:6off
nscd 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
portmap 0:off 1:2off 2:3off 3:4on 4:5on 5:6off
postgresql 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
sound 0:off 1:2off 2:3off 3:4on 4:5on 5:6off
round 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
restad 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
userserv 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
wallid 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
rwhod 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
smb 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
sendmail 0:off 1:2on 2:3off 3:4on 4:5on 5:6off
squid 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
nmmpd 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
xntpd 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
ybind 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
yppaswwd 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
ypserv 0:off 1:2off 2:3off 3:4off 4:5off 5:6off
```

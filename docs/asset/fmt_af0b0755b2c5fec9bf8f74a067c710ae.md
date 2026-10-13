
7. 在 `/tmp/` 目录下创建一个名为 `operations_network.txt` 的新文件。记录所有权和权限。更改 operator1 的 umask。创建一个名为 `operations_production.txt` 的新文件。记录 `operations_production.txt` 文件的所有权和权限。

### 7.1. 使用 `echo` 命令在 `/tmp/shared` 目录下创建一个名为 `operations_network.txt` 的文件。

```
[operator1@servera ~]$ echo >> /tmp/shared/operations_network.txt
```

### 7.2. 使用 `ls -1` 列出 `operations_network.txt` 文件的权限。

```
[operator1@servera ~]$ ls -1 /tmp/shared/operations_network.txt
-rw-rw-r--. 1 operator1 operators May 5 15:43
```

### 7.3. 使用 `umask` 命令将 operator1 用户的掩码更改为 027。使用 `umask` 命令确认更改。

```
[operator1@servera ~]$ umask 027
[operator1@servera ~]$ umask
```

### 7.4. 使用 `touch` 命令在 `/tmp/shared/` 目录下创建一个名为 `operations_production.txt` 的新文件。使用 `ls -1` 确保新创建的文件对 operators 组具有只读权限，且对其他用户没有权限。

```
[operator1@servera ~]$ touch /tmp/shared/operations_production.txt
```

```
[operator1@servera ~]$ ls -l /tmp/shared/operations_production.txt
-rw-r--r-- 1 operator1 operators 0 Feb 4 15:56 /tmp/shared/
operations_production.txt
```

8. 打开一个新的终端窗口并以 operator1 身份登录到 servera。

```
[student@workstation ~]$ ssh operator1@servera
[operator1@servera ~]$
```

9. 查看 operator1 的 umask 值。

```
[operator1@servera ~]$ umask
0002
```

10. 修改 operator1 用户的默认 umask。新的 umask 将禁止所有不在该组的用户进行访问。确认 umask 已经更改。

#### 10.1. 使用 `echo` 命令将 operator1 用户的默认 umask 修改为 007。

```
[operator1@servera ~]$ echo "umask 007" >> ~/.bashrc
[operator1@servera ~]$ cat ~/.bashrc
## .bashrc

### Source global definitions
if [ -f /etc/bashrc ]; then
  /etc/bashrc
fi

# Uncomment the following line if you don't like systemctl's auto-paging feature:
# export SYSTEMD_PAGER=

# User specific aliases and functions
umask 007
```

#### 10.2. 退出并重新登录 operator1 用户。使用 `umask` 命令确认更改是永久生效的。

```
[operator1@servera ~]$ exit
logout
Connection to server closed.
[student@workstation ~]$ ssh operator1@servera
[operator1@servera ~]$ umask
0007
```

11. 在服务器上，退出所有 operator1 和 student 用户的 shell。

> 注意
> 退出所有 operator1 打开的 shell。未能退出所有 shell 将导致完成脚本执行失败。

```
[operator1@server ~]$ exit
logout
Connection to server closed.
[student@workstation ~$]
```

## 完成

在工作站上，运行实验的 `perms-default finish` 脚本来完成此项练习。

```
[student@workstation ~]$ lab perms-default finish
```

此引导性练习此结束。

# 实验

# 控制文件访问

## 性能检查清单

在本实验中，你将配置文件权限，并设置一个目录，特定组的用户可以使用该目录在本地系统上方便地共享文件。

## 目标

你应该能够：

- 创建一个用户可以在其中进行协作处理文件的目录。
- 创建自动分配组所有权的文件。
- 创建在组外无法访问的文件。

### 准备之前

使用 `student` 作为密码，以 `student` 身份登录到工作站。

在工作站上，运行 `lab permis-review start` 命令。该命令运行一个启动脚本，用于判断服务器在网络上是否可用。该脚本还会创建 `techdocs` 组以及三个用户 `tech1`、`tech2` 和 `database1`。

```
[student@workstation ~]$ lab permis-review start
```

1. 使用 `ssh` 命令以 `student` 用户身份登录服务器。使用 `redhat` 作为密码在服务器上切换到 root。

2. 创建名为 `/home/techdocs` 的目录。

3. 将 `/home/techdocs` 目录的组所有权更改为 `techdocs` 组。

4. 验证 `techdocs` 组的用户可以在 `/home/techdocs` 目录下创建和编辑文件。

5. 设置 `/home/techdocs` 目录的权限。对于 `/home/techdocs` 目录，为所有者和组设置读/写/执行权限 `7`，其他用户无权限 `0`。

6. 验证权限已正确设置。

7. 确认 `techdocs` 组的用户现在可以在 `/home/techdocs` 目录下创建和编辑文件。不在 `techdocs` 组的用户无法创建或编辑 `/home/techdocs` 目录中的文件。用户 `tech1` 和 `tech2` 在 `techdocs` 组中。用户 `database1` 不在该组中。

8. 修改全局登录脚本。普通用户应该有一个 umask 设置，防止他人查看或修改新文件和目录。

9. 退出服务器。

```
[student@server ~]$ exit
logout
Connection to serverb closed.
```

## 评估

在工作站上，运行实验的 `perms-review grade` 脚本以确认此项练习成功。

```
[student@workstation ~]$ lab perms-review grade
```

## 完成

在工作站上，运行实验的 `perms-review finish` 脚本来完成实验。

```
[student@workstation ~]$ lab perms-review finish
```

此实验结束。

## 解决方案

# 控制文件访问

## 性能检查清单

在本实验中，你将配置文件权限，并设置一个目录，特定组的用户可以使用该目录在本地系统上方便地共享文件。

## 目标

你应该能够：

- 创建一个用户可以在其中进行协作处理文件的目录。
- 创建自动分配组所有权的文件。
- 创建在组外无法访问的文件。

### 准备之前

使用 `student` 作为密码，以 `student` 身份登录到工作站。

在工作站上，运行 `lab permis-review start` 命令。该命令运行一个启动脚本，用于判断服务器在网络上是否可用。该脚本还会创建 `techdocs` 组以及三个用户 `tech1`、`tech2` 和 `database1`。

```
[student@workstation ~]$ lab permis-review start
```

1. 使用 `ssh` 命令以 `student` 用户身份登录服务器。使用 `redhat` 作为密码在服务器上切换到 root。

2. 创建名为 `/home/techdocs` 的目录。

3. 将 `/home/techdocs` 目录的组所有权更改为 `techdocs` 组。

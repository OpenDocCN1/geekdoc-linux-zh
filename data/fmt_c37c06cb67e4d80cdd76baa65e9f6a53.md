
`useradd -c "Frank Zappa" -m zappaf`

```
useradd -c "Frank Zappa" -m zappaf
```

### 10. 下面的 useradd 指令哪里有错？

```
useradd -m -o underwoodi
```

### 11. 使用 useradd，请提供一个为 `software-audacity` 创建新账户的指令。该账户应拥有它自己的家目录 `/var/media/audacity`，登录 shell 为 `/sbin/nologin`，且没有私有组账户。

### 12. 默认情况下，账户过期日期设置为 `-1`，表示不设置初始过期日期。你想更改此设置，以便将新用户的过期日期自动设置为 2018 年 12 月 31 日。你该如何操作？

### 13. 将本章第 9.2.3 节中的账户创建脚本修改如下：

- 用户文本文件的所有条目将列为：姓 名 专业（Lastname Firstname Major）
- 如果专业（Major）为 `CSC`，则为学生分配 shell `tcsh` 而不是 `bash`。

### 14. 将本章第 9.2.3 节中的账户创建脚本修改如下：

- 用户文本文件的所有条目将列为：姓 类型（Lastname Type）
- 类型为教师（Faculty）或学生（Student）。根据 `Type` 的值，所有家目录放置在 `/home/faculty/username` 或 `/home/student/username`。

### 15. 将本章第 9.2.3 节中的账户创建脚本修改如下：

- 用户文本文件的所有条目将列为：姓 角色（Lastname Role）
- 角色为管理员（Administrator）、数据库（Database）或网络（Network）。如果是管理员，将该用户加入组管理。如果是数据库或网络，将用户加入技术组（`technical`）。如果是数据库，还将用户加入 `oracle` 组。

### 16. 在第 9.2.3 节的账户创建脚本中，有如下指令。请解释该指令的作用以及它是如何运行的。

```
n=$(egrep -c $username /etc/passwd)
```

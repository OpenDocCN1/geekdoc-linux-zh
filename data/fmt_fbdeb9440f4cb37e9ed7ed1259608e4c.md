
# 第6章 · 安全你的网络

```
$ ssh-keygen
```

正在生成公/私 rsa 密钥对。

输入保存密钥的文件 (`/home/daemon/.ssh/identity`):

创建目录 `'/home/daemon/.ssh'`。

输入密码（空表示无密码）：

再次输入相同的密码：

您的标识已保存到 `/home/daemon/.ssh/identity`。

您的公钥已保存到 `/home/daemon/.ssh/identity.pub`。

密钥指纹为：
`a9ee:40:52:32:52:93:cb:ed:60:53:c3:d9:37:b5`

`daemon@sharky.incoming-traveller.com`

```
$ ls -al .ssh
```

```
total 9
drwx------ 2 daemon daemon 104 Aug 30 07:32 ./
drwx------ 5 daemon daemon 264 Aug 30 07:32 ../
-rw------- 1 daemon daemon 547 Aug 30 07:32 identity
```

![](img/ab996f014aa8c5c7de3d77cc73ef5ce3_215_0.png)

```
-rw-r-- 1 daemon daemon 351 Aug 30 07:32
identity.pub
$
```

如你所示，SSH 已创建了一个 `.ssh` 目录，其中创建了私钥（`identity`）和公钥（`identity.pub`）。`.ssh` 目录的权限模式为 `700`，公钥模式为 `644`，私钥模式为 `600`。它们不能是列出模式之外的任何模式，否则你的传输将无法工作。你正在创建的是 SSH 等同于 `.rhosts` 条目的内容，SSH 通过对密钥文件执行严格权限来防止前面描述的 `.rhosts` 攻击。

接下来，你需要将公钥复制到接收端主机上的授权密钥列表中。你可以使用任何方便的方法，但以下步骤是行之有效的：

```
$ sc identity.pub daemon@receiving.incoming-traveller:-.ssh/sparky-identity.pub
```

在远程主机上，进入 `.ssh` 目录并执行以下命令：

```
$ cat sparky-identity.pub >> authorized_keys
```


或者

```
find /etc/hosts.deny -cpio /dev/hda7
```

以及

```
find /etc/hosts.allow -print | cpio > /dev/hda7
```

或者

```
find /etc/hosts.allow -cpio /dev/hda7
```

## 主题 4

将多个目录 `tar` 到挂载设备 `/dev/hda10`。为了使用此系统，你将需要使用后续章节介绍的命令。

### 示例

```
tar -cvf /dev/hda10 /home /fileserver/ /mnt/home/httpd
```

该命令将 `home/fileserver/` 和 `/home/httpd` 目录压缩到 `/dev/hda10`。

## 主题 5

此练习要求系统管理员使用 `cpio` 复制 `/etc` 目录下的所有文件并使用时间戳，对 `/dev/hda16` 执行增量备份并排除对象文件。

```
find /etc -ctime -1 ! -name *.o -print | cpio > /dev/hda16
```

或者你可以使用以下方法：

```
tar cl 'find /etc - -1 ! -name '*o*' ! -type d -print'
```

## 主题 6

为 1999 年 4 月 16 日的完整备份制作目录列表，将使用以下 `cpio` 命令将 `toc` 发送到备份中：

```
$ toc = 'date + /backup/home_full_%dbky.TOC'

find /home -print | cpio ov > /dev/hda8 2 > $toc
```

## 主题 7

使用 `cpio` 在 7 天内备份 `/home/usr` 目录。使用如下命令是非常重要的：

```
ctime -7 | cpio -cvFo > /mnt/home/user
```

## 主题 8

使用 `tar` 备份磁带。本实验是对以此方式使用 `tar` 的良好复习。

```
tar -cvpf /dev/tape -dev /sto/tape10/path/data/backup -2
```

`tar` 创建磁带的详细备份并将其存储在 10 号磁带上。

## 实验练习

1. 使用 `.netrc` 在晚上 7 点备份你 `/usr` 目录下的 `backup4.tar` 文件。
2. 使用 `find` 和 `cpio` 备份 `/home` 目录并将其放入 `/dev/hda3`。
3. 从 `/etc` 目录拷贝 `hosts.allow` 和 `hosts.deny` 并使用 `cpio` 将它们备份到 `/dev/hda3`。
4. 使用 `tar` 将 `/home` `/fileserver/` `/mnt/home/httpd` 备份到 `/dev/hda10`。
5. 使用 `cpio` 复制 `/etc` 目录下的所有文件并时间戳，对 `/dev/hda16` 执行增量备份并排除对象文件。
6. 使用 `cpio` 对家目录制作 1999 年 4 月 16 日完整备份的目录列表 `TOC`。
7. 给出使用 `cpio` 在七天内备份 `/home/usr` 目录的命令。
8. 使用 `tar` 备份磁带从 `/dev/tape-dev/sto/tape10` 到 `/path/data/backup -2`。

## 问题

1. 使用 `.netrc` 备份工具有什么优点？权衡是什么？
2. 为什么要设置 `.netrc` 文件的权限？

## 答案

1. 使用 `.netrc` 备份工具有什么优点？权衡是什么？
2. 为什么要设置 `.netrc` 文件的权限？

（注：原文中后续大量重复的问题已根据要求去重）

## 332 Lab VII

`return login`

```python
def getshell():
    done = 0
    while not done:
        shell = raw_input("What is the user's login shell *")
        if (shell=='bash')or(shell=='sh')or(shell=='ksh')or(shell=='csh')):
            done = 1
        else:
            print('Error: Invalid shell')
    return shell
```

```python
def getpassword():
    done = 0
    while not done:
        passwd = raw_input("What is the initial password of the user *")
        if len(passwd) < 6:
            print('Error: Password should be more than 5 characters')
        else:
            done = 1
    return passwd
```

```python
def getuid():
    uid = raw_input("What is the user id *")
    return uid
```

```python
def getxpire():
    expire = raw_input("Date on which the user account will expire *")
    return expire
```

```python
def getcomment():
    com = raw_input("What is the name password related to *")
    return com
```

```python
def getinactive():
    inact = raw_input("Enter number of days a password expires *")
    return inact
```

### 此函数通过调用上述所有函数获取用户信息信息，并将信息传递给执行命令。

```python
def do_all():
    login = getlogin()
    passwd = getpassword()
    shell = getshell()
    uid = getuid()
    expire = getxpire()
    comment = getcomment()
    inact = getinactive()
    try:
        print('creating an account for new user:')
        print(login, passwd, shell, uid, expire, comment, inact)
        execute(login, passwd, shell, uid, expire, comment, inact)
    except:
        print 'error while creating an account:'; exit(1)

if __name__ == '__main__':
    try:
        do_all()
    except:
        print 'usage: auser'; exit(1)
```

## 示例 3

另一个用于管理用户（如添加、删除和修改用户）的常用脚本如下：

`file managers.py`

```python
#!/usr/local/bin/python
# 导入 auser、muser 和 duser 脚本分别分别添加、修改和删除用户账户。
# 这些脚本都有 do_all() 函数，调用它们来执行
# 任务
from glob import glob
from sys import argv
import os, auser, duser, muser

def adduser():
    auser.do_all()

def modifyuser():
    muser.do_all()

def deleteuser():
    duser.do_all()

# 此函数允许系统管理员连续地添加、修改和删除用户
# 账户
def interact():
    while 1:
        name = raw_input("tool: [auser, modifyuser, deleteuser, stop]")
        if name == 'auser':
            auser()
        elif name == 'modifyuser':
```


## 4.4. 切换到 `contractor1` 用户并执行以下操作。检查是否获得了预期的访问行为。

```
[manager1@serverb cases]$ exit

logout
```

```
[student@serverb -$] su - contractor1

Password: redhat

[contractor1@serverb -$] cd /shares/classes

[contractor1@serverb cases]$ echo hello > manager1.txt

[contractor1@serverb cases]$ cat shortlist.txt

###List of Clients to all###TEMPLATE###

[contractor1@serverb cases]$ mkdir contractor1.dir

[contractor1@serverb cases]$ echo hello > contractor1.dir/test.txt

[contractor1@serverb cases]$ ls -l contractor1.dir

drws-x---+ 2 contractor1 managers 22 Mar 29 01:05 contractor1.dir

[contractor1@serverb cases]$ ls -l contractor1.dir

total 4

-rw-rw--+ 11 managers 6 Mar 29 01:07 test.txt

[manager1@serverb cases]$ getfacl contractor1.dir

# file: contractor1.dir/

# owner: contractor1

# group: managers

# flags: -s

user::rwx

user:contractor3:r-x

group::rwx

group:contractors:rwx

mask::rwx

other::--

default:user::rwx

default:user:contractor3:r-x

default:group::rwx

default:group:contractors:rwx

default:mask::rwx

default:other::---

default:other
```

```
[contractor1@server cases]$ exit

logout
```

## 4.5. 切换到 `contractor3` 用户并执行以下操作。检查是否获得预期行为。

```
[student@server -]# su - contractor3

Password: redhat

[contractor3@server -]# cd /shares/cases

[contractor3@server -]# echo hello > contractor3.txt

-bash: contractor3.txt: Permission denied

[contractor3@server -]# cat shortlist.txt

###Shortlist of Clients to call##TEMPLATE###

[contractor3@server -]# mkdir contractor3.dir

-bash: cannot create directory "contractor3.dir": Permission denied

[contractor3@server -]# cat manager1.dir/test.txt

hello

[contractor3@server -]# cat contractor1.dir

hello

[contractor3@server -]# exit
```

## 4.6. 退出服务器

```
[student@server -]# exit

Connection to server closed.

[student@workstation -]$
```

这些测试是你可以执行以检查访问权限正确的正确的。你应该为你的环境设计适当的访问。

## 评估
在工作站运行 `lab-review grade` 命令以确认实验成功。

```
[student@workstation -]$ lab-review grade
```

## 完成
在工作站运行 `lab-review finish` 命令完成此实验。

```
[student@workstation -]$ lab-review finish
```

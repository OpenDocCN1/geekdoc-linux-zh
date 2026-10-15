
```
drwx--  2 taylor      512 Sep 30 10:38 Archives/
-rw---  1 taylor    106020 Oct 10 13:47 LISTS
-rw-rw-r- 1 taylor   280232 Oct 10 16:22 mailing.lists
-rw-rw-- 1 taylor    1037 Oct 7 15:44 newlists
```

现在，每一项对应的数值等价是什么？第一个是 `700`。

在尝试用 `chmod` 使用数值权限字符串之前，还差最后一步。你需要能够反向推算，确定你想要设置的权限，并找出该权限对应的数值等价。

### 任务5.5：计算数值权限字符串

假设你想设置一个目录，使你拥有所有访问权限，你所在组的人可以查看内容但不能修改任何东西，而其他所有人都被拒之门外。你会怎么做？

你自己拥有所有权限意味着你希望所有者具有读+写+执行权限（即数值权限`7`）；组内其他人具有读取和列目录权限意味着组具有读+执行权限（数值权限`5`）；而其他所有人没有任何权限，即数值权限`0`。将这三个数字组合在一起，就得到答案：`750`。

这就是以数值模式使用 `chmod` 的窍门。你以三位数字的形式指定你想要的绝对权限，系统会相应地设置文件或目录的权限。

在这种 `chmod` 形式中，绝对概念非常重要。你不能使用 `chmod` 数值形式来为文件或目录添加或移除权限。它只能用于重新分配文件或目录的权限字符串。

好消息是，正如你在本小时早些时候学到的，常用的文件权限相对较少，表5.6对此进行了总结。

| 权限 | 数值 | 用途 |
|------------|---------|-----------|
| --------- | 000 | 所有类型 |
| r------- | 400 | 文件 |
| r--r--r-- | 444 | 文件 |
| rw------ | 600 | 文件 |
| rw-r--r-- | 644 | 文件 |
| rw-rw-r-- | 664 | 文件 |
| rw-rw-rw- | 666 | 文件 |
| rwx------ | 700 | 程序和目录 |
| rwxr-x--- | 750 | 程序和目录 |
| rwxr-xr-x | 755 | 程序和目录 |
| rwxrwxrwx | 777 | 程序和目录 |

表5.6 常见权限及其数值等价

1. 打开你的电脑，尝试使用 `chmod` 的数值模式，并配合 `ls` 来显示实际权限，亲自体会一下这是如何工作的：

```
% touch example
% ls -l example
-rw-rw-- 1 taylor 0 Oct 12 10:16 example
```

默认情况下，我的目录中创建的文件模式为 `660`。这是由 `umask` 设置决定的，我们稍后会探讨。

2. 要取消组内人员的读写权限，我应该把 `660` 权限替换成什么数值权限字符串呢？我会使用 `600`：

```
% chmod 600 example
% ls -l example
-rw--- 1 taylor 0 Oct 12 10:16 example
```

3. 如果我改变主意，想让每个人都能读取或写入这个文件呢？我会使用 `666`：

```
% chmod 666 example
% ls -l example
-rw-rw-rw- 1 taylor 0 Oct 12 10:16 example
```

4. 最后，假设这个 `example` 实际上是一个目录。我应该指定什么数值模式，才能让每个人都能在该目录中使用 `ls`，并且只有所有者才能添加或删除文件？我会使用 `755`：

```
% chmod 755 example
% ls -l example
-rwxr-xr-x 1 taylor 0 Oct 12 10:16 example
```

你已经了解了定义权限的数值模式和符号模式。在掌握这两种模式之后，你更喜欢哪一种？

### 注意

不知怎的，我始终没掌握符号模式的要领，所以我几乎总是使用 `chmod` 的数值模式。唯一的例外是当我想要添加或删除简单权限时。这时，我会使用类似 `chmod +r test` 的命令来添加读权限。部分问题在于，我想到的不是文件的使用者，而是所有者，这让我想到“o”——而指定 `o+r` 会让 `chmod` 修改“其他用户”的权限，而不是所有者。因此，记住文件有使用者（`user`）是很重要的，这样你就会用 `u` 代表使用者，而所有不在组内的用户都是“其他用户”（`other`），所以你用 `o` 代表他们。否则，就学数值快捷方式吧！

文件权限和模式是 Unix 最复杂的方面之一。你可以从这一点看出，因为完全解释清楚它花了两小时的时间。你需要花时间去理解权限字符串如何与目录权限相关联，如何读取 `output of ls`, and how to change modes using both styles of the `chmod` command. It will be time well spent.

## Task 5.6: Establishing Default File and Directory Permissions with the umask Command

When I’ve created files, they’ve had read+write permission for the owner and group but no access allowed for anyone else. When you create files on your system, you might find that the default permissions are different.

> **Note**
>
> Different systems have different default permissions. The default mode on most Linux flavors is `664`, whereas on other platforms `644` is more common.

The controlling variable behind the default permissions is called the file creation mask, or `umask` for short.

Inexplicably, `umask` doesn’t always list its value as a three-digit number, but you can find its value in the same way you figured out the numeric permissions strings for `chmod`. For example, when I enter `umask`, the system indicates that my `umask` setting is `07`. A leading zero has been dropped, so the actual value is `007`, a value that British MI6 could no doubt appreciate!

> **Note**
>
> Some systems, such as Solaris and Linux, use a four-digit `umask` string rather than a two-digit one. The first digit in this case indicates any special modes (such as the “sticky bit” or the setGID option).

But `007` doesn’t mean that the default file is created with read+write+execute for everyone else and no permissions for the owner or group. It means quite the opposite—literally.

The `umask` command is a filter through which permissions are pushed to ascertain what remains. Figure 5.8 demonstrates how this works.

Step One: translate the mask into binary

`007` → `000 000 111`

Step two: write down the binary equivalent of all permissions allowed (`777`)

`777` → `111 111 111`

Now split each binary number into individual digits and stack them, one above the other:

`0 0 0 0 0 0 1 1 1`

`1 1 1 1 1 1 1 1 1`



此选项更改用户的登录名。所有其他信息保持不变。通常，当你更改登录名时，你也希望更改或移动主目录，如前一节所述。在这里显示的示例中，登录名 flower 被更改为 newflower。

## 更改次要组隶属关系

要更改次要组隶属关系，输入以下命令：

```
usermod -d newdirpath -m login
usermod -d /home/newflower -m flower
[root@digital root]# groups flower
flower : flower users
[root@digital root]# usermod -G wheel,database flower
[root@digital root]# groups flower
flower : flower wheel database
```

groups 命令打印用户当前所有组隶属关系的列表。如果未提供登录名，它会假设你想知道当前用户的组隶属关系。

要更改所有次要组隶属关系（不是默认组），提供一个用逗号分隔的组名列表，且中间没有空格。如果省略某个组，则该成员资格将被移除。唯一的例外是用户的首要组。

## 删除用户：userdel

要从系统中删除用户，可以使用 userdel 命令。userdel 以用户的登录名作为参数。这将从 /etc/passwd 文件中删除指定的用户。然而，用户的主目录、邮箱、UPG 以及其他组隶属关系仍会被保留。语法如下：

```
[root@digital root]# userdel newflower
```

通常，在删除用户之前，你应该备份相应的账户和邮箱，或在删除账户前请用户自行备份。在采取必要的预防措施后，使用 userdel 删除用户。然后使用 groupdel 删除用户的 UPG 条目。你还必须使用文本编辑器从 /etc/group 文件中的所有其他条目中删除已移除的登录名。

如果你使用 UPG 并且用户的默认组是对应的 UPG，可以通过输入以下命令减少步骤数：

```
usermod -G username username
```

这将移除用户除 UPG（默认组）之外的所有组隶属关系。默认组作为 -G 的参数提供，因为 usermod 需要它。在完成上一步后，你可以输入以下命令：

```
userdel username
```

这会从 /etc/passwd 文件中删除用户。你可以通过从 /etc/group 中删除 UPG 来完成任务。最后通过删除用户的主目录和他的邮箱来完成移除（确保你先备份了！），如下所示：

```
rm -R /home/username /usr/spool/mail/username
```

Previous Table of Contents Next

要访问内容，请点击章节和节标题。

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## 添加、修改和删除组

管理组与管理账户类似。请注意，这些命令提供的一些功能也可以通过 usermod 等程序实现。你选择的取决于你当时正在做什么。

### Groupadd

在你使用组之前，需要先创建它。创建组很容易；只需使用 groupadd 命令：

```
groupadd -g GID groupname
[root@digital alberto]# groupadd -g 600 weirdgroup
```

使用 groupadd 的唯一需要注意的是，你需要提供一个 /etc/group 文件当前未使用的 GID。为了便于编号，你可能希望将自定义组指定为从 GID 30000 或其他小于 65536（最大值）的较大数字开始。

### 管理组成员资格：gpasswd

gpasswd 程序用于管理组文件。添加和删除用户的[content]

此选项更改用户的登录名。所有其他信息保持不变。通常，当你更改登录名时，你也希望更改或移动主目录，如前一节所述。在这里显示的示例中，登录名 flower 被更改为 newflower。

## 更改次要组隶属关系

要更改次要组隶属关系，输入以下命令：

```
usermod -d newdirpath -m login
usermod -d /home/newflower -m flower
[root@digital root]# groups flower
flower : flower users
[root@digital root]# usermod -G wheel,database flower
[root@digital root]# groups flower
flower : flower wheel database
```

groups 命令打印用户当前所有组隶属关系的列表。如果未提供登录名，它会假设你想知道当前用户的组隶属关系。

要更改所有次要组隶属关系（不是默认组），提供一个用逗号分隔的组名列表，且中间没有空格。如果省略某个组，则该成员资格将被移除。唯一的例外是用户的首要组。

## 删除用户：userdel

要从系统中删除用户，可以使用 userdel 命令。userdel 以用户的登录名作为参数。这将从 /etc/passwd 文件中删除指定的用户。然而，用户的主目录、邮箱、UPG 以及其他组隶属关系仍会被保留。语法如下：

```
[root@digital root]# userdel newflower
```

通常，在删除用户之前，你应该备份相应的账户和邮箱，或在删除账户前请用户自行备份。在采取必要的预防措施后，使用 userdel 删除用户。然后使用 groupdel 删除用户的 UPG 条目。你还必须使用文本编辑器从 /etc/group 文件中的所有其他条目中删除已移除的登录名。

如果你使用 UPG 并且用户的默认组是对应的 UPG，可以通过输入以下命令减少步骤数：

```
usermod -G username username
```

这将移除用户除 UPG（默认组）之外的所有组隶属关系。默认组作为 -G 的参数提供，因为 usermod 需要它。在完成上一步后，你可以输入以下命令：

```
userdel username
```

这会从 /etc/passwd 文件中删除用户。你可以通过从 /etc/group 中删除 UPG 来完成任务。最后通过删除用户的主目录和他的邮箱来完成移除（确保你先备份了！），如下所示：

```
rm -R /home/username /usr/spool/mail/username
```

Previous Table of Contents Next

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Search this book:

## Adding, Modifying, and Removing Groups

Managing groups is similar to managing accounts. Note that some of the functionality provided by these commands can also be attained through programs like usermod. Your choice of which one to use will depend on what you are doing at that moment.

### Groupadd

Before you can work with a group, you need to create it. Creating a group is easy; just use the groupadd command:

```
groupadd -g GID groupname
[root@digital alberto]# groupadd -g 600 weirdgroup
```

The one catch with groupadd is that you need to supply a GID that your /etc/group file is not currently using. To make numbering easy on you, you might want to designate custom groups to start with a GID of 30000 or some other large number less than 65536 (the maximum number).

### Managing Group Memberships: gpasswd

The gpasswd program is used to manage the group file. The basic functionality for adding and removing users is straightforward. The -a flag is used to add users (note that the group must already exist), like this:

```
gpasswd -a username groupname
```

```
[root@digital alberto]# gpasswd -a flower users
```

The -d flag is used to delete users, like this:

```
gpasswd -d username groupname
```

## Users and Passwords

UNIX (and Linux) security begins with proper password selection. Therefore, it is a good idea to use passwords that cannot be easily guessed. Using simple scripts and available programs, a deviant hacker can test several thousand passwords in a few seconds.

### Password Don'ts

- Do not use birthdays, social security numbers, or phone numbers.
- Do not use names of relatives or pets.
- Do not use words that appear in a dictionary.
- Do not give your password to anyone—not even to a system administrator. If this person is really an administrator, he or she doesn’t need your password!

### Password Do's

- Mix upper- and lower-case.
- Add numbers and punctuation marks to make it harder to guess. Your final password should probably be random letters and numbers.
- Change your password every two months or any time that you think your password might have become compromised.
- Good passwords should roll out of your fingers and be easy to type. Many people are very adept at telling what you type from the motion of your fingers. If you have to think about it, it is probably not a good password for you.

## Linux and Shadow Passwords

If you are managing a computer that is connected to the Internet and that supports several users, you should consider enabling shadow passwords in your system. Shadow passwords are installed by default as a part of the standard installation. To see if shadow passwords are currently installed on your system, try this:

```
$ ls /etc/shadow
/etc/shadow
$
```

You should have received the same response. If ls responds instead like this, you should install shadow password support immediately:

```
ls: /etc/shadow: No such file or directory
```

Shadow passwords protect system passwords by making the file that actually contains passwords (/etc/shadow) readable only by root. The /etc/passwd file will contain stars (*) where the encrypted password was previously found. This is because even though passwords are encrypted in the /etc/passwd file, low-end computers have become very fast and able to decrypt them in a short amount of time. In the late 1980s, it probably would have taken days or weeks to decrypt this information. With today’s technology, however, it can take only a few minutes. By making the password file readable only by root, this establishes yet another security layer around this information.

For more information on shadow passwords and how to enable them, you should take a look at your man documentation for shadow (section 5 of the UNIX manual, man 5 shadow), pwconv, and pwunconv.

## SPIDER KILLER

## spider catcher

HOME ACCOUNT INFO SUBSCRIBE LOGIN SEARCH MY ITKNOWLEDGE FAQ SITEMAP CONTACT US

To access the contents, click the chapter and section titles.

## Complete Idiot's Guide to Linux

(Publisher: Macmillan Computer Publishing)
Author(s): Manuel Ricart
ISBN: 078971826x
Publication Date: 12/22/98

Bookmark it

Search this book:

Previous Table of Contents Next

## Chapter 19
### Backups: Safeguarding Your Work

### In This Chapter

- Media Are Just Devices
- What to Back Up
- Simple Backups
- Tape Archive: tar
- A Backup Strategy
- Graphical Backup Programs

Without a doubt the most important maintenance task that you can perform on any computer is a backup. Backups can be tedious tasks, but it’s usually when you have neglected to do it that you most need it! Having a backup for your data can mean the difference between an inconvenience and a catastrophe. Without a backup, you’ll have a déjà vu experience recreating the work you lose. As you might already know, that is no fun. Restoring your system from a backup can be an inconvenience, and maybe a few hours of work will be lost, but it is much different than losing work you’ve created throughout past weeks, months, or even years!

A backup might be required even for simple user errors such as deleting important files. Unlike Windows or other operating systems, under UNIX/Linux there’s no “undelete” program, Norton Undelete, or any other tool to restore deleted files. If the file is deleted, it is gone. The reason these


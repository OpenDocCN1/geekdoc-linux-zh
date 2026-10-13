
`john:x:538:`
`john:x:539:`
`john:x:540:`
`john:x:541:`
`john:x:542:`
`john:x:543:`
`john:x:544:`
`john:x:545:`
`john:x:546:`
`john:x:547:`
`john:x:548:`
`john:x:549:`
`john:x:550:`
`john:x:551:`
`john:x:552:`
`john:x:553:`
`john:x:554:`
`john:x:555:`
`john:x:556:`
`john:x:557:`
`john:x:558:`
`john:x:559:`
`john:x:560:`
`john:x:561:`
`john:x:562:`
`john:x:563:`
`john:x:564:`
`john:x:565:`
`john:x:566:`
`john:x:567:`
`john:x:568:`
`john:x:569:`
`john:x:570:`
`john:x:571:`
`john:x:572:`
`john:x:573:`
`john:x:574:`
`john:x:575:`
`john:x:576:`
`john:x:577:`
`john:x:578:`
`john:x:579:`
`john:x:580:`
`john:x:581:`
`john:x:582:`
`john:x:583:`
`john:x:584:`
`john:x:585:`
`john:x:586:`
`john:x:587:`
`john:x:588:`
`john:x:589:`
`john:x:590:`
`john:x:591:`
`john:x:592:`
`john:x:593:`
`john:x:594:`
`john:x:595:`
`john:x:596:`
`john:x:597:`
`john:x:598:`
`john:x:599:`
`john:x:600:`
`john:x:601:`
`john:x:602:`
`john:x:603:`
`john:x:604:`
`john:x:605:`
`john:x:606:`
`john:x:607:`
`john:x:608:`
`john:x:609:`
`john:x:610:`
`john:x:611:`
`john:x:612:`
`john:x:613:`
`john:x:614:`
`john:x:615:`
`john:x:616:`
`john:x:617:`
`john:x:618:`
`john:x:619:`
`john:x:620:`
`john:x:621:`
`john:x:622:`
`john:x:623:`
`john:x:624:`
`john:x:625:`
`john:x:626:`
`john:x:627:`
`john:x:628:`
`john:x:629:`
`john:x:630:`
`john:x:631:`
`john:x:632:`
`john:x:633:`
`john:x:634:`
`john:x:635:`
`john:x:636:`
`john:x:637:`
`john:x:638:`
`john:x:639:`
`john:x:640:`
`john:x:641:`
`john:x:642:`
`john:x:643:`
`john:x:644:`
`john:x:645:`
`john:x:646:`
`john:x:647:`
`john:x:648:`
`john:x:649:`
`john:x:650:`
`john:x:651:`
`john:x:652:`
`john:x:653:`
`john:x:654:`
`john:x:655:`
`john:x:656:`
`john:x:657:`
`john:x:658:`
`john:x:659:`
`john:x:660:`
`john:x:661:`
`john:x:662:`
`john:x:663:`
`john:x:664:`
`john:x:665:`
`john:x:666:`
`john:x:667:`
`john:x:668:`
`john:x:669:`
`john:x:670:`
`john:x:671:`
`john:x:672:`
`john:x:673:`
`john:x:674:`
`john:x:675:`
`john:x:676:`
`john:x:677:`
`john:x:678:`
`john:x:679:`
`john:x:680:`
`john:x:681:`
`john:x:682:`
`john:x:683:`
`john:x:684:`
`john:x:685:`
`john:x:686:`
`john:x:687:`
`john:x:688:`
`john:x:689:`
`john:x:690:`
`john:x:691:`
`john:x:692:`
`john:x:693:`
`john:x:694:`
`john:x:695:`
`john:x:696:`
`john:x:697:`
`john:x:698:`
`john:x:699:`
`john:x:700:`
`john:x:701:`
`john:x:702:`
`john:x:703:`
`john:x:704:`
`john:x:705:`
`john:x:706:`
`john:x:707:`
`john:x:708:`
`john:x:709:`
`john:x:710:`
`john:x:711:`
`john:x:712:`
`john:x:713:`
`john:x:714:`
`john:x:715:`
`john:x:716:`
`john:x:717:`
`john:x:718:`
`john:x:719:`
`john:x:720:`
`john:x:721:`
`john:x:722:`
`john:x:723:`
`john:x:724:`
`john:x:725:`
`john:x:726:`
`john:x:727:`
`john:x:728:`
`john:x:729:`
`john:x:730:`
`john:x:731:`
`john:x:732:`
`john:x:733:`
`john:x:734:`
`john:x:735:`
`john:x:736:`
`john:x:737:`
`john:x:738:`
`john:x:739:`
`john:x:740:`
`john:x:741:`
`john:x:742:`
`john:x:743:`
`john:x:744:`
`john:x:745:`
`john:x:746:`
`john:x:747:`
`john:x:748:`
`john:x:749:`

不同的操作系统实现组的方式。Fedora Core 使用名为 User 的方案，为所有用户分配组。这里是 `/etc/group` 的部分列表：
（注：此处省略了重复的 ID 列表，仅展示格式）

4. 使用 `gpasswd` 命令让用户 `shelley` 成为组管理员，这样她就可以向组中添加新用户了。

```
# gpasswd -A shelley
```

现在，用户 `shelley` 拥有权限使用 CDRW 驱动器，任何由超级用户或 `shelley` 添加到该组的用户也具有此权限，因为她现在也是组管理员，可以向组中添加新用户。

系统管理员可以使用 Fedora Core 提供的图形界面，如图 9.1 所示。它通过“系统”菜单项中的“用户和组”项目进行访问。

![](img/96ce0bc6bd65a9b4c721fc1cd7169438_284_0.png)

图 9.1 只需勾选框即可添加到组。

你会注意到，图形界面无法提供全套组命令和选项，这限制了 GUI 的实用性，仅包含最常用命令的子集。你将在本章的下一节中学习更多关于使用 Fedora Core 用户组管理器 GUI 的知识。

## 用户管理

我们之前提到过用户，但在本节中，我们将检查系统管理员如何管理用户。创建用户时必须使用 UID、为其提供家目录、为该家目录提供初始文件集，并将其分配到组，以便他们能够安全、高效地使用系统资源。系统管理员可能会选择不仅限制用户对文件的访问，还限制他们使用的磁盘空间。（你将在第 8 章“管理软件和系统资源”中的“管理磁盘配额”部分中学习更多相关内容。）

## 用户管理工具

Fedora Core 提供了多个用于管理用户的命令行工具以及图形化工具。许多经验丰富的系统管理员倾向于使用命令行工具，因为它们快速且易用，而且当系统管理员需要为重复任务编写脚本时，可以将它们包含在脚本中。

以下是管理用户最常用的命令：

- `useradd`——此命令用于向系统添加新用户。其选项允许系统管理员指定用户的家目录和初始组，或者在创建家目录和分配组时创建用户。
- `useradd -G`——此命令设置了创建用户家目录、账户过期日期、默认组和命令 shell 的系统默认值。请参阅 `man useradd` 中的特定选项。系统显示，用于用户的默认文件位于 `/etc/skel`。

> 注意

最初用于填充新用户家目录的文件集保存在 `/etc/skel` 中。对于系统管理员来说，在 `/etc/skel` 中创建需要通用应用的特殊文件、链接或目录是非常方便的，这些内容将为每个新用户自动复制相应的权限。

```
# ls -al /etc/skel

drwxr-xr-x 3 root root 4096 Aug 29 09:11 .

drwxr-xr-x 86 root root 8192 Aug 29 14:51 .
```

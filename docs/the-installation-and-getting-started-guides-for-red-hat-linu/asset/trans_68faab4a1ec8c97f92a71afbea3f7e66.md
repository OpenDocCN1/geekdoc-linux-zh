

当我们输入 o+w 时，我们的意思是：“对于其他人，对文件 sneakers.txt 添加写权限。”

如果我们想移除 sneakers.txt 的所有访问权限（即使它只是一个粗略的购物清单），我们可以使用 chmod 命令来同时移除读和写权限，如下所示：

```
chmod go-rw sneakers.txt
```

结果会看起来像这样：

```
-rw--- 1 billy billy 150 Mar 19 08:08
sneakers.txt
```

通过输入 go-rw，我们的意思就是“对于组和其他人，移除对文件 sneakers.txt 的读和写权限。”

你可以把这些设置看作在使用 chmod 修改权限时的一种速记，因为你只需要记住 chmod 命令中的几个符号和字母。

以下是速记所代表的内容：

## Identities

- **u** — 文件的所有者（即拥有者）
- **g** — 用户所属的组
- **o** — 其他人（不是所有者或所有者的组）
- **a** — 所有人（u、g 和 o）

## Permissions

- **r** — 读访问
- **w** — 写访问
- **x** — 执行访问

## Actions

- + — 添加权限
- - — 移除权限
- = — 使其成为唯一权限

想试试吗？让我们移除 sneakers.txt 的所有权限——对所有人。

```
chmod a-rw sneakers.txt
```

现在，让我们看看是否能读取该文件：

```
[billy@localhost billy] cat sneakers.txt
cat: sneakers.txt: Permission denied
[billy@localhost billy]
```

看来成功了；甚至我们也无法访问该文件。但由于文件属于我们，我们始终可以更改权限以允许我们进行读写访问。（参见图 16-19）

```
[billy@localhost billy] chmod u+rw sneakers.txt
[billy@localhost billy] cat sneakers.txt
buy some sneakers
then go to the coffee shop
then buy some coffee
bring the coffee home
take off shoes
put on sneakers
make some coffee
relax!
[billy@localhost billy]
```

![](img/46f4935125ba89e12897afbe9d77a097_736_0.png)

## Figure 16-19: Removing, then restoring permissions

以下是可与 chmod 一起使用的一些常见设置示例：

- g+w — 为组添加写访问权限
- o-rwx — 移除其他人的所有权限
- u+x — 允许文件所有者执行文件
- a+rw — 允许所有人读写文件
- ug+r — 允许所有者和组读取文件
- g=rx — 仅允许组读和执行（不写）

通过添加 -R 选项，我们可以更改整个目录树的权限。

## The Getting Started Guide for Red Hat Linux 6.0

不过，这里有一个小小的变化，因为我们不能真正像运行应用程序那样“执行”一个目录。相反，当我们为目录添加或移除执行权限时，我们实际上是在允许（或拒绝）搜索该目录的权限。

要允许所有人对登录目录中的 tigger 目录具有读写访问权限，我们只需输入：

```
chmod -R a+rw tigger
```

但是……如果我们不允许其他人对 tigger 具有执行权限，那么谁拥有读或写访问权限就无关紧要了，因为没有人能够进入该目录——除非他们知道想要的确切文件名。

例如，让我们输入：

```
chmod a-x tigger
```

以移除所有人的执行访问权限。

现在当我们尝试 cd 进入 tigger 时会发生什么：

```
[billy@localhost billy] cd tigger
bash: tigger: Permission denied
billy@localhost billy]
```

让我们恢复我们和我们组的访问权限。

```
chmod ug+x tigger
```

现在，如果我们用 ls -di 检查工作结果，我们会看到只有其他人会被拒绝访问 tigger。

## Fun with Numbers in chmod

还记得我们提到 chmod 的“速记”方法吗？这里还有另一种更改权限的方法；乍一看可能有点复杂——尤其是如果你不擅长数学的话。让我们回到 sneakers.txt 的原始权限。

```
-rw-rw-r- 1 billy billy 150 Mar 19 08:08 sneakers.txt
```

每个权限设置都可以用一个数值表示：

- r = 4
- w = 2
- x = 1
- - = 0

将这些值相加后，总和用于设置特定权限——比使用字母“速记”更改权限更具体。在 sneakers.txt 中，那么这里是数值权限设置：

```
-    (-rw)    (-rw)    (r-)
  |       |       |
  0+4+2   0+4+2   4+0+0
```

用户的总数为六，组的总数为六，其他人的总数为四。那么权限设置读作 664。如果我们想更改 sneakers.txt，使我们组中的人没有写访问权限，但仍可读取文件（如图 16-20 所示），我们必须通过从该数字集中减去 2 来移除访问权限。

那么数值将变为六、四和四——也就是 644。

所以我们可以输入：

```
chmod 644 sneakers.txt
```


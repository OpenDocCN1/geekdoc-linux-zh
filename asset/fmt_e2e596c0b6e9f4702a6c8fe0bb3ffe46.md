
至此，你现在应该已经安装了一个原生的 z/VM 会话。

## 4.3 配置 XEDIT profile

登录 `MAINT`（如果尚未登录）。

`XEDIT` 命令在调用时会寻找 `XEDIT PROFILE` 配置。许多 z/VM 用户 ID 没有个人或共享系统文件，因此所有 `XEDIT` 默认值有效。`MAINT 191 (A)` 磁盘有一个 `PROFILE XEDIT`，当你在编辑文件时，profile 中的值通常有效。

如果你从未用过 `XEDIT`，请参阅第 212 页的“`XEDIT quick reference sheet`”获取有关此主题的信息。`z/VM 5.4 PDF` 库可以通过 Web 获取：

`http://www-03.ibm.com/systems/z/os/zksers/zvpdf#zvm54`

搜索 `XEDIT User's Guide and Command Reference`。网上还有一份手册：

`http://ukcc.uky.uk/ukccinfo/391/xeditref.html`

一个危险的默认设置（特别是使用 `F12` 检索命令时）是 `PF12` 被设置为 `FILE` 命令。有时你并不希望按一个键就保存更改。我们建议将 `PF12` 设置为 `?` 命令，它具有检索键的效果：

```
== copy profile edit a profile xeditorig a (olddd)
== x profile edit a
```

之前：

```
SET PF12 FILE
```

之后：

```
SET PF12 ?
```

使用 `FILE` 命令保存更改。

## 4.4 自定义 SYSTEM CONFIG 文件

`z/VM` `IPL` 时读取的第一个配置文件是 `SYSTEM CONFIG` 文件。建议进行以下更改：

- 更改系统名称。
- 增加重试容量。
- 允许创建虚拟磁盘（`VDISKS`）。
- 关闭断开超时（`Disconnect Timeout`）。这可以防止空闲的断开用户被强制踢出系统。
- 定义一个用于 Linux 网络的虚拟交换机（`VSITCH`）。

要进行这些更改，请执行以下步骤：

+ 1. 要编辑 `SYSTEM CONFIG` 文件，必须使用 `PRELEASE` 命令将 `MAIN CFI` 磁盘作为 `CP` 磁盘重新读取。使用 `QUERY` 命令查询 `CP` 命令。请注意，`MAIN CFI` 磁盘在释放之前被作为 `CP` 磁盘 `A` 访问，但在释放后不再被访问。

```
== qdisk
| Label | UserId | Vdev | Mode | Stat | Vol-Id | Rdev | Type | StartLoc | EndLoc |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| MTCFC1 | MAIN | OCF1 | A | R/O | 54R05 | D850 | CKD | 39 | |
| MTCFC2 | MAIN | OCF2 | B | R/O | 54R05 | D850 | CKD | 159 | 278 |
| MTCFC3 | MAIN | OCF3 | C | R/O | 54R05 | D850 | CKD | 279 | 398 |
```

```
== cpre
CPRELEASE request for a disk A.
HZPAC67301 CPRELEASE request for a disk A completed.
```

```
== qdisk
| Label | UserId | Vdev | Mode | Stat | Vol-Id | Rdev | Type | StartLoc | EndLoc |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| MTCFC2 | MAIN | OCF2 | B | R/O | 54R05 | D850 | CKD | 159 | 278 |
| MTCFC3 | MAIN | OCF3 | C | R/O | 54R05 | D850 | CKD | 279 | 398 |
```

+ 2. 之后，你就可以读写方式访问 `MAIN CFI` 磁盘了。使用带有多读（`MR`）参数的 `LINK` 命令和 `ACCESS` 命令来获取作为磁盘 `F` 的读写权限。

```
== link cfl cf1
== acc cfl f1
```

+ 3. 使用 `COPYFILE` 命令配合 `OLDDATE` 参数对原始的 `SYSTEM CONFIG` 文件进行备份副本，以防文件被修改。注意，目标文件名（`system`）和模式（`f`）是相同的，等号 `=` 可以通通配符。

```
== copy system f = configur (=olddate)
```

+ 4. 编辑原始文件：

```
== x system config
```

+ 5. 系统名称在 `System_Identifier_Default` 语句中默认设置为 `ZWI5R40`。你可以使用 `/subcommand:` 搜索它：

```
>>>> /System_Identifier_D
```

修改此项以更改你的系统名称。在本例中，`VMLUXA`

`System_Identifier_Default <VMLUXA>`

+ 6. 接下来查找 `Features` 语句。你可以搜索它或使用 `F8` 向翻页。建议进行以下更改和添加：

- 将可以检索的命令数量从 20 增加到 99。
- 将 `Disconnect_Timeout` 设置为 `off`，这样断开的用户就不会被强制退出。
- 通过使用 `UserLimit infinite` 并添加 `SysLimit infinite` 子句，允许创建无限数量的 `VDISKS`，如下所示：

`Features,`

```
/* Disable the following features */
/* Disallow SETPRIVCLASS command */
/* Prompt at IPL always */
/* Don't clear TDis at IPL time */
/* Retrieve options */
/* Default... default is 20 */
/* Maximum... default is 25 */
/* No limit on number of users */
/* What allows passwords? */
/* ... AUTOLOG does */
/* ... LINK does */
/* ... and LOGON does, too */
/* Don't force disconnected users */
/* Allow VDSWKS for Linux swaps */
```

`Disable _`

`Set_Privclass`

`Auto_Warm_IPL`

`Clear_TDis`

`Retriever =`

`Default : 99 -`

`Maximum : 255`

`Maxusers limit`

`Passwords_on_Cmds`

`Autolog yes`

`Link yes`

`Logon yes`

`Disconnect_timeout _`

`Vdisk ,`

`System User`

`infinite`

## 5. 定义一个 VSWITCH 命令

使用 `BOTTOM` 命令到文件末尾。添加几行（你可以使用 `XEDIT` 子命令 `add`）。定义一个 `VSWITCH` 并设置 `MAC` 地址前缀。这将设置为每个虚拟网卡创建 `MAC` 地址的前三个字节。如果你有多个 `z/VM` 系统，请避免创建相同的 `MAC` 地址。`MAC` 地址的最后三个字节由 `z/VM` 在分配时自动递增，因此它们在每个 `z/VM` 系统上将是唯一的。修改 `OSA` 的起始地址（在本例中为 `3024` 和 `3028`）为你在 2.7 中指定的地址。

```
===> bot
===> a3
/* define vswitch vswl set MAC address prefix */
define vswitch vswl prefix <3024><3028>
vml macprefix 02001
```

7. 使用 `XEDIT` 命令保存更改：

```
===> file
```

8. 使用 `CPSYNTC` 命令在 `MAINT 13` 磁盘上测试你的更改：

```
===> acc 93
===> config
CONFIGURATION COMPLETE -- NO ERROR ENCOUNTERED.
```

注意输出。如果收到任何语法错误，请先修复它们。

9. 使用 `RELEASE` 和 `DETACH` 命令释放并脱离 `MAIN CF` 文件，然后使用 `CPACCESS` 命令将其恢复上线：

```
===> rel f
DASD DETACHED
===> cpac cfl a
CPACCESS request for mode completed.
```

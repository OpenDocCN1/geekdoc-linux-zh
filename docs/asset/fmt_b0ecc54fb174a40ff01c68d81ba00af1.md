
记住这些步骤很有用。

### 3. 使用 `WRKS` 后缀制作 `SYSTEM` 文件的副本

```bash
==> copy system
```

### 4. 编辑 `CONFIG` 文件并通过名称指定每个页卷（`PAGE`）。当你使用 `IPL` 时，它将加载这些页

```bash
==> system config f
==> /cp_owned
*********************************
/ CP_Owned Volume
*********************************
CP_Owned Slot 1 540RES
CP_Owned Slot 2 540SPL
CP_Owned Slot 3 540P
CP_Owned Slot 4 540W1
CP_Owned Slot 5 540W2
CP_Owned Slot 6 <MPD85>
CP_Owned Slot 7 <MPD90>
CP_Owned Slot 8 <MPD51>
CP_Owned Slot 9 <MPD50>
CP_Owned Slot 10 <MPD85>
CP_Owned Slot 11 RESERVED
CP_Owned Slot 12 RESERVED
CP_Owned Slot 13 RESERVED
```

### 5. 移动到 `User_Volume_List`。卷（`PERM`）可以通过 `User_Volume_List` 或 `User_Volume_Include` 语句指定。在使用 `CPFORMAT` 强制标记，添加以下单行以包含所有 `PERM` 标记

```bash
==> user_v
*********************************
/ User_Volume_List
/ These statements are not active. They are
*********************************
/* User_Volume_Include RP01 */
/* User_Volume_Include RP02 */
```

### 6. 使用 `FILE` 命令保存更改。使用 `CPSYTAX` 命令验证更改的完整性

```bash
==> acc 193 g
== cpsytax system config f -- ERRORS ENCOUNTERED.
```

### 7. 确认没有错误后，将 `MAINT CF1` 磁盘上线。以下示例显示了你是如何做的

```bash
== rel f (det)
DASD OCF1 DETACHED
== cpace a
CPACCESS request for mode A scheduled.
HCPZAC67321 CPACCESS for MAINT's OCF1 in mode A completed.
== qpidisc
Label Userid Mode Stat-Vol StartLoc
| :--- | :--- | :--- | :--- | :--- | :--- |
| MNTFC1 | OCF1 | A | R/O | 520S2 020 | 39 83 |
| MNTFC2 | OCF2 | B | R/O | 520S2 020 | 84 128 |
| MNTFC3 | OCF3 | C | R/O | 520S2 020 | 129 188 |
```

## 4.6 测试更改

我们建议重启并测试更改。在重启之前，使用 `QUERY ALL` 命令注意你只有一个页卷（`540PAG`）。你的输出应该是：

```bash
== q alloc page
EXTENT TOTAL PAGES %
VOLID RED START END PAGES USAGE
| :--- | :--- | :--- | :--- | :--- | :--- |
| 540PAG | DB852 | 1 | 3338 | 600840 | 0 0% |
SUMMARY 600840 0%
USABLE 600840 0%
```

现在使用 `SHUTDOWN REIPL IPLPARMS=SYS` 关闭系统。这类似于 Linux 的 `reboot` 命令，系统在关闭后会尝试恢复。如果你使用 `3270` 仿真器连接，将会丢失话，但如果一切顺利，你的系统将在几分钟后可用。

```bash
== shutdown reipl iplparms cons=sys
```

系统恢复后，以 `MAINT` 登录并再次检查页空间。你应该看到六个分页卷：

```bash
== q alloc page
EXTENT TOTAL PAGES %
VOLID RED START END PAGES USAGE
| :--- | :--- | :--- | :--- | :--- | :--- |
| 540PAG | DB852 | 1 | 3338 | 600840 | 0 0% |
| MDB855 | DB855 | 0 | 3338 | 601020 | 0 0% |
| MDB950 | D950 | 0 | 3338 | 601020 | 0 0% |
| MDB951 | D951 | 0 | 3338 | 601020 | 12 1% |
| MDADA50 | DA550 | 0 | 3338 | 601020 | 0 0% |
| MDB850 | DB850 | 0 | 3338 | 601020 | 0 0% |
```

在此目录中指定了 `END` 选项的微磁盘（`minidisks`）将不会包含在以下 `DISMAP` 文件中。已创建 `USER DISMAP A`。

### 3. 创建的文件 `USER DISMAP` 包含 `USER DIRECT` 文件中定义的所有微磁盘卷映射。它将列出卷中发现的任何重叠或间隙。编辑该文件并使用 `XEDIT PREF off` 子命令关闭多达 80 列的前缀区域

```bash
==> user diskmap
== prefix off
```

### 4. 使用 `/overlap` 子命令搜索文本重叠

```bash
==>/overlap
```

你应该会看到错误消息 `MSDXC546E Target not found`。这意味着微磁盘之间存在重叠。

现在搜索间隙。你也应该看到一些间隙：

```bash
==> /...
$$$$$ DATAMOVE 5FO 3380 00501 00501 00001
DATAMOVE 5FF 3380 00502 00502 00001
```

| VOLUME | USERID | CUI | DEVTYPE | START | END | SIZE |
| --- | --- | --- | --- | --- | --- | --- |
| $$$LNX | ZWMMLAP | 150 | 3390 | 00001 | 03338 | 1 GAP |

| USERID | CUI | DEVTYPE | START | END | SIZE |
| --- | --- | --- | --- | --- | --- |
| MMD057 | LNXMAINT | 0191 | 3390 | 00001 | 00020 | 1 GAP |
| LNXMAINT | 0192 | 3390 | 00021 | 00320 | 03000 |

右侧显示了三个间隙：`$$$$$$$$` 卷

- `$$$$$$$$` 卷上的 501 个磁道
- `$$$LNX` 卷上的 1 个磁道
- `LNXMAINT 191` 和 `192` 磁盘的 1 个磁柱卷（在本例中为 `MMD057`）

不需要担心前两个间隙，因为根据默认 `USER DIRECT` 文件的布局，这是预期的。为了避免在每个用户卷上报告 1 个磁道的间隙，我们建议你使用 `ID ALLOC`。该用户被设置为 `NOLOG`，永远无法登录。这并不是为每个 `perm TERMS` 的常规 `ID 0` 放置占位定义的的方便位置。

### 5. 使用 `QUIT` 命令或按 `F3` 退出 `USER DISMAP`

### 6. 编辑 `USER DIRECT` 文件，在你使用的 `DASD` 的第一个磁道的虚拟地址 `A04` 处添加一个新的微磁盘定义（在本例中标签为 `MMD057`）

```bash
==> user alloc
== /user alloc
USER ALLOC NOLOG
DISK A01 3390 000 001 540ES5 R
DISK A02 3390 000 001 540W01 R
DISK A03 3390 000 001 540W02 R
DISK A04 3390 000 001 -MMD057> R
```

### 7. 保存更改并再次运行 `DISMAP`。编辑 `USER DISMAP` 文件。这次你应该只看到针对标签为 `$$$$$$$$` 和 `$$$LNX` 卷的两个间隙。如果你搜索 `$$$ALLOC` 用户 `ID`，你应该能看到为 `LNXMAINT` 添加的卷的磁盘映射

```bash
== diskmap user
== x diskmap
== prefs off
==> SALOC
MMD857 A04 3390 00000 00000 00001
```

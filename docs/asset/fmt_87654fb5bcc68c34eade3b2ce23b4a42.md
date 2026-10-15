
```
q alloc page
VOLID RDEV EXTENT START EXTENT END TOTAL PAGES HIGH %
PAGES IN USE PAGE USED
--------------------------
LX6PGAG 1A22 1 3338 600840 0 0 0%
LX6PG2 8228 1 3338 601020 13 51 0%
--------------------------
SUMMARY 1174K 13 1%
USABLE 1174K 13 1%
Ready; T=0.01/0.01 14:40:42
```

要验证 `PERM` 卷现在是否已联机，请使用 `QUERY DASD` 命令查询系统所看到的 `DASD`，如第 183 页的示例 4-9 所示。

```
q dasd
DASD 1A20 CP OWNED LX6RES  78
DASD 1A21 CP OWNED LX6SPL  1
DASD 1A22 CP OWNED LX6PAG  0
DASD 1A23 CP OWNED LX6W01 113
DASD 1A24 CP OWNED LX6W02  4
DASD 1A25 CP SYSTEM NW1A25 0
DASD 1A26 CP SYSTEM NW1A26 0
DASD 1A27 CP SYSTEM NW1A27 0
DASD 1A28 CP SYSTEM NW1A28 0
DASD 1A29 CP SYSTEM NW1A29 0
DASD 8228 CP OWNED LX6PG2 0
Ready; T=0.01/0.01 14:48:20
```

## 创建 Linux MAINT 用户

在启动 Linux 之前，创建一个用户到主机的公共文件，该文件将由你创建的每个 Linux 客户机系统使用。若要启动任意数量的 Linux 客户机，请为每个客户机创建一个引导参数文件（而不是每次都手动处理）。创建引导参数文件的优点是，用于引导 Linux 的文件不会在每个客户机系统用户空间中重复。

以 `MAINT` 身份登录以继续为安装 Linux 配置 z/VM 系统。如第 140 页“z/VM 用户和密码规划”所述，Linux 管理员 ID 为 `LNXMAINT`。在对 `USER DIRECT` 文件进行任何更改以创建其磁盘之前，先复制该文件：

```
==> copy user direct c = direorig = {old d
```

## 为 `LNXMAINT` 设置小磁盘空间

在虚拟地址 191 处分配一个小的 20 柱面小磁盘，并在虚拟地址 192 处定义一个更大的 300 柱面小磁盘（约 225 MB），供多个客户机共享。你可以使用工作表中指定为 `PERM` 空间的新 `DASD` 之一（第 403 页表 B-1），也可以使用 `LX6W02` 上的任何可用空间（如果你一直按照本书的安装步骤进行，`LX6W02` 很可能有部分空闲空间），因为小磁盘仅使用 320 个柱面。

> 注：柱面 0 必须始终保留用于标签，因此如果你选择使用其中一个新 `DASD`，应从柱面 1 开始小磁盘。

要为 `LNXMAINT` 设置小磁盘空间：

1. 编辑 `USER DIRECT` 文件并在文件底部添加以下用户 ID 定义：

    ```
    ==> x user direct c
    ====> bottom
    ====> a 6
    ...
    USER LNXMAINT LNXMAINT 64M 128M BEG
    INCLUDE IBMDFLT
    LINK TCPMAINT 592 592 RR
    MDISK 0191 3390 <2050> 0020 <LX6W02> MR READ WRITE MULTIPLE
    MDISK 0192 3390 <2070> 0300 <LX6W02> MR ALL WRITE MULTIPLE
    *
    ...
    ====> file
    ```

    请注意以下关于黑色数字的要点：

    1. 用户 ID `LNXMAINT` 具有相同的密码；分配给该用户的存储（主内存）默认大小为 64 MB 加上 128 MB 的扩展存储，具有 B、E 和 G 类权限。

    2. 包含名为 `IBMDFLT` 的配置文件（该文件在 `USER DIRECT` 文件中更早定义）。

    3. 链接到 `TCPMAINT` 592 磁盘为只读，以便访问 FTP 和其他 TCP/IP 命令。

    4. 从卷 `LX6W02` 定义一个大小为 20 柱面的 191 小磁盘。

    5. 从卷 `LX6W02` 定义一个大小为 300 柱面（约 225 MB）的 192 小磁盘，并具有特殊的读密码 `ALL`，允许任何用户 ID 在无需磁盘密码的情况下进行读访问。

    6. 一个空的注释行是为了更好的可读性。

2. 当在 `USER DIRECT` 文件中添加或修改 `MDISK` 语句时，始终检查是否有重叠的柱面和间隙（尽管间隙只会留下空磁盘空间，但 z/VM 允许你在同一磁盘空间上定义多个小磁盘，这不一定是有益的）。要检查，请使用 `DISKMAP` 命令，如“创建磁盘”第 134 页所述：

    ```
    ==> diskmap user
    The minidisks with the END option specified in this directory will not be included in the following DISKMAP file.

    File USER DISKMAP A has been created.
    ```

    创建的文件 `USER DISKMAP A` 包含 `USER DIRECT` 文件中定义的所有 minidisk 卷的映射。它列出了卷上发现的任何重叠或间隙。

3. 编辑该文件，并用 `XEDIT PREFIX OFF` 子命令关闭前缀区域，以查看 80 列：

    ```
    ==> x user diskmap
    ===> prefix off
    ```

4. 使用 `/`（斜杠）子命令搜索 `overlap` 文本：

    ```
    ====> /overlap
    ```

    出现以下消息，表示没有 minidisk 相互重叠：

    ```
    DMSXDC546E Target not found.
    ```

    查看文件的其余部分。你的 `LNXMAINT` 的 minidisk 定义应类似于我们的定义，如图 4-17 所示。请注意，它们定义在 `LX6W02` 磁盘上，除非你使用的是新 `DASD` 之一。

    ```
    | 00236 ------------------------------- |
    | 00237 |
    | 00238 VOLUME USERID CUU DEVTYPE START END SIZE |
    | 00239 LX6W02 $ALLOCS A03 3390 00000 00000 00001 |
    | 00240 40ASF40 2D2 3390 00001 00150 00150 |
    | 00241 OSAADMIN2 191 3390 00151 00160 00010 |
    | <...snip...> |
    | 00331 CERON 191 3390 02040 02049 00010 |
    | 00332 LNXMAINT 191 3390 02050 02069 00020 |
    | 00333 LNXMAINT 192 3390 02070 02369 00300 |
    ```

    图 4-17 创建 `LNXMAINT` 后的 `USER DISKMAP` 文件。

5. 使用 `QUIT` 命令或按 `F3` 退出 `USER DISKMAP` 文件。

6. 如果你使用了新 `DASD` 之一，请再次编辑 `USER DIRECT` 文件，并为你遗漏的那个最开始的柱面添加一个新的 minidisk 定义⁸。这样可以防止系统将其报告为间隙。

    以下示例是 `USER DIRECT` 文件：

    ```
    ==> x user direct
    ===> /user $alloc
    USER $ALLOCS NOLOG
    MDISK A01 3390 000 001 LX6RES R
    MDISK A02 3390 000 001 LX6W01 R
    MDISK A03 3390 000 001 LX6W02 R
    MDISK A04 3390 000 001 <W1A25> R
    ```

    ⁸ 如果你没有遗漏它，那么你可能没有读完第 183 页“为 `LNXMAINT` 设置 minidisk 空间”开头的注意事项。

7. 当你确定 minidisk 布局正确后，可以使用 `DIRECTXA` 命令将 `USER DIRECT` 文件的更改上线：

    ```
    ==> directxa user
    z/VM USER DIRECTORY CREATION PROGRAM - VERSION 5 RELEASE 3.0
    EOJ DIRECTORY UPDATED AND ON LINE
    HCPDIR494I User directory occupies 39 disk pages
    ```

8. 如果 `DIRECTXA` 命令失败，你必须在继续之前纠正问题。

现在你已经定义了第一个名为 `LNXMAINT` 的 z/VM 用户 ID。

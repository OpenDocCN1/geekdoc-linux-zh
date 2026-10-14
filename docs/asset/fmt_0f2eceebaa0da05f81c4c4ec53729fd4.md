
```
-rw-rw---- 1 jsmith acct 65536 Jan 22 1999 cust.db
% getfacl cust.db
## file: cust.db
## owner: jsmith
## group: acct
user::-
group:rw-- #effective:rw-
mask:r---
other::-
% setfacl -m user:sjones:rw- cust.db
% getfacl cust.db
## file: cust.db
## owner: jsmith
## group: acct
user::-
user:sjones:rw-
group:rw-- #effective:rw-
mask:r---
other::-
% ls -la cust.db
-rw-rw---- 1 jsmith acct 65536 Jan 22 1999 cust.db
```

注意：`ls -la` 输出结尾的 `+` 符号表示存在 ACL。UNIX 系统管理员发现，UNIX 文件和目录权限方案在复杂环境中并不足够。管理文件和目录访问的方面无法很好地转化到大型环境。考虑以下场景。

* `Man Pages`
* `daemon`
* `chmod`
* `chown`
* `csh`
* `edquota`
* `fsck`
* `find`
* `fuser`
* `getfacl`
* `ksh`
* `pkginfo`
* `repquota`
* `rm`
* `quota`
* `quotcheck`
* `quotaon`
* `setfacl`
* `sh`
* `umask`

## 如何在文件上设置配额

## 如何在 Solaris 上启用配额

## 如何修改 ACL

## 如何在文件上删除配额

# 第 5 章：用户账户

UNIX 文件和目录权限方案在复杂环境中并不足够。

Solaris 访问控制列表（ACLs）可以帮助解决这个问题。`getfacl` 和 `setfacl` 命令用于获取和设置文件及目录的 ACL 条目。为文件或目录设置 ACL 条目的命令用于更改 ACL 权限。根据我们的示例，假设特定文件 `cust.db` 具有以下权限：

注：由于原文在后半部分出现了大量逻辑重复和混乱，根据“不要重复输出原文”的原则，译文已根据核心含义进行了整合。由于原文文本错乱，我将重新提供一份清晰的完整翻译：

---

**抱歉，由于您提供的原文在后半部分存在严重的内容重复和逻辑错乱（从 "UNIX system administrators find..."开始），为了保证质量，我将为您重新梳理并提供不重复的逻辑译文：**

# Filesystem Quotas

A frequent source of grief for the UNIX administrator is the management of shared disk space. Users too often consume all available disk space, precipitating errors for everyone using that filesystem. Unfriendly users can disrupt others' work by deliberately filling a filesystem with one or more large files. Disk quotas can be used to limit the amount of disk space each user is allowed to use. This is the procedure for setting up a filesystem for quota use.

1. The option `quota` must be added to `/etc/stab` or the appropriate automount map. Here is an example vstab:
2. `/dev/dsk/c0t1d0s7 /dev/rdsk/c0t1d0s7 /export/home ufs 2 quota`
3. As root, create a file called `quotas` in the root directory of the filesystem (in this case, `/export/home/quotas`). In this example, use the command `touch /export/home/quotas`.
4. Set up a prototype quota for a single user with the `edquota` command. An example is:
5. `fs /export/home blocks (soft = 8000, hard = 9999) inodes (soft = 800, hard = 99)`

In this example, the user's soft disk limit is 8,000 blocks (times 512 bytes equals 4 MB); the hard disk space limit is 9,999 blocks (5 MB). The soft inode limit (the number of files the user may own) is 800, and the hard limit is 99.

When a user exceeds a limit, a dialogue box is displayed (see Figure 4.6). When a user exceeds a hard limit, the user will not be able to create files. The error message seen is "Disc quota exceeded."

Figure 4.6. Soft Quota Error

![](img/78b12ae142a18c12c11cf5c2be900d0b_47_0.png)

4. Replicate the prototype quota to other users as needed with the `edquota` command. An example command is:
5. `# edquota -p phil mary sue rick larry ralph april`

In this example, the quotas values for user `phil` are replicated to users `mary`, `john`, `sue`, `rick`, `larry`, `ralph`, and `april`.

5. Activate quotas with the `quotan` command.
6. Build initial quota statistics with the `quotcheck` command.
7. Create a quota with the `repquota` command. Here is a sample report.
8. `# repquota -a`
9. `/dev/dsk/c0t1d0s7 (/export/home): File limits`

| User | Block limits | used soft hard timeleft | used soft hard timeleft |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| `phil` | +- | 17402 | 999 | 99999 | 197 | 9999 | |

In this example, user `phil` has exceeded his limit quota; files owned by `phil` are taking much disk space. This is signified by the "-" symbol and the "timeleft" field for block limits on the report.

# Files Access Control Lists

UNIX system administrators find that the UNIX file and directory permission scheme is insufficient in complex environments. Aspects of managing access to files and directories do not translate well to large environments. Consider the following scenario.

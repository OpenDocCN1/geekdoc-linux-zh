
### 图 10.16 – `dnf module remove nodejs` 的输出

```
[root@localhost vagrant]# dnf module remove nodejs
Last metadata expiration check: 0:09:52 ago on Fri 16 Dec 2022 09:05:16 PM UTC.
Dependencies resolved.
=================================================================
Package Arch    Repository                Size
=================================================================
Removing:
nodejs x86_64    1.14.20-2.module+el8.6.0+20874+338992dc @ol8_appstream 37 M
nps   x86_64    1.14.17-1.14.20.1.2.module+el8.6.0+20874+338992dc @ol8_appstream 15 M
Disabling module profiles:
nodejs/common
=================================================================
Transaction Summary
=================================================================
Remove 2 Packages
Freed space: 52. M
Is this ok [y/N]: 
```

从此消息中，你可以看到 `NPM` 将卸载，但考虑到 `Node.js` 模块安装的不只是 `NPM`，这并不是你预期的。如果你想移除与该模块相关的所有内容，你需要传递 `--all` 标志，如下所示：

```bash
# dnf module remove nodejs --all
```

这一次，你将看到所有关联软件包都已进入移除队列：

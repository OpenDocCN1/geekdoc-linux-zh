
4. 现在让我们输入一些列：`CREATE TABLE videos(title VARCHAR(40), year INT, REGISTRATION INT);`

5. 让我们输入一些数据：`INSERT INTO videos (registration,title,actor,year) VALUES(1,'Basic Instinct','Sharon Stone',1992);`

6. 重复此操作以输入以下视频：

2,Pretty Woman, Julia Roberts, 1990

3,Terminator, Arnold Schwarzenegger, 1984

4,Jurassic Park, Harrison Ford, 1992

- 7. 输入 `SELECT * from videos;` 显示整个数据库的概览。你应该能看到类似于列表 35.7 中的结果。

列表 35.7 SELECT * 结果

```
MariaDB [videos]> INSERT INTO videos (registration,title,actor,year) VALUES (1,'Basic Instinct','Sharon Stone', 1992)
Query OK, 1 row affected (0.01 sec)
MariaDB [videos]> INSERT INTO videos (registration,title,actor,year) VALUES (2,'Pretty Woman','Julia Roberts', 1990)
Query OK, 1 row affected (0.00 sec)
```

```
MariaDB [videos]> INSERT INTO videos (registration, title,
actor,year) VALUES (3, 'Terminator', 'Arnold Schwarzenegger', 1984);
Query OK, 1 row affected (0.00 sec)
```

```
MariaDB [videos]> INSERT INTO videos (registration, title,
actor,year) VALUES (4, 'Jurassic Park', 'Harrison Ford', 1992);
Query OK, 1 row affected (0.00 sec)
```

```
MariaDB [videos]> select * from videos;
+----------------+----------------------+-----------+
| title | actor | year | registration |
+----------------+----------------------+-----------+
| Basic Instinct | Sharon Stone | 1992 | 1 |
| Pretty Woman | Julia Roberts | 1990 | 2 |
| Terminator | Arnold Schwarzenegger | 1984 | 3 |
| Jurassic Park | Harrison Ford | 1992 | 4 |
+----------------+----------------------+-----------+
4 rows in set (0.00 sec)
```

- 8. 使用 `CREATE USER julia@%' IDENTIFIED BY 'secret';` 创建一个用户。

9. 使用 `GRANT SELECT,INSERT,UPDATE,DELETE ON videos.* TO julia@'%'.` 授予该用户权限。

10. 输入 `FLUSH PRIVILEGES;` 更新权限。

11. 输入 `DESCRIBE videos;` 显示 videos 数据库记录的概览。

12. 插入另一个新视频：`INSERT INTO videos(registration,title,actor,year) VALUES (5,'The Last Stand', 'Arnold Schwarzenegger', 2013);`

13. 显示 actor 字段设置为 Arnold Schwarzenegger 的所有记录列表：`SELECT * FROM videos WHERE actor = 'Arnold Schwarzenegger';`

14. 输入 `quit` 关闭 MySQL 壳程序界面。

# MariaDB 备份与恢复

在对 MariaDB 进行备份时，你可以采取两种方法。你可以创建物理备份。在物理备份中，你拥有数据库目录和文件夹的原始副本。这种备份速度很快，但它仅适用于使用相似硬件和软件的机器。要进行物理备份，数据库服务应处于离线状态，或者锁定数据库中的表以防止数据在备份期间发生变化。

另一种方法是进行逻辑备份。在逻辑备份中，通过查询数据库来检索数据库结构。这种备份相对缓慢，因为必须访问数据库并将其转换为逻辑格式。它具有巨大的优势：(1) 你可以在运行中的数据库上创建逻辑备份，(2) 逻辑数据库备份也可以迁移到其他数据库提供程序。尽管如此，逻辑备份中不包含日志和配置文件。因此，你可能希望同时创建物理备份和逻辑备份。

要恢复备份，第一步是从备份文件中获取数据库名称（以防未知）。你可以用 `less` 打开文件（因为它是可读文件），确保你要恢复的数据库存在，如果不存在，则使用 `mysql datename`。要恢复逻辑备份，接下来运行命令 `mysqldump -u root -p database < /root/database.dump`。

要创建逻辑数据库备份，你可以使用 `mysqldump`（shell）命令。

# 第 35 章：配置 MariaDB 数据库

## 练习 35.3 创建物理数据库备份

- 1. 首先，确认实际数据库的存储位置。要做到这一点，使用 `mysqldadmin -u root -p variables | grep datadir`。该命令显示存储数据的目录。通常，结果是 `/var/lib/mysql`。

2. 使用命令 `df /var/lib/mysql` 找出托管该位置的 LVM 卷。（当然，这只有在安装期间创建了托管物理数据库的 LVM 卷时有效。）

> 注意 为了高效使用快照，请确保 `/var/lib/mysql` 位于逻辑卷上。如果不是，备份可能会变得异常大。在本练习中，假设情况如此且 mariadb 数据库位于 `/dev/vgdata/lvmriadb`。

- 3. 使用 `vgs vgname` 验证数据库卷所在的卷组内是否有未分配的磁盘空间。

- 4. 此时，你需要临时冻结数据库以便在创建快照时无法进行修改。要做到这一点，使用 root 身份连接数据库 `mysql -u root -p`，`FLUSH TABLES WITH READ LOCK;` 不要关闭此会话，因为这将移除锁定！

- 5. 在另一个终端会话中创建 LVM 快照。以下命令假设卷组名称为 `vgdata`，LVM 名称为托管数据库的卷是 `lmariadb`：`lvcreate -L 2G -n lmariadb-snapshot /dev/vgdata/lvmariadb`。确保快照大小足够容纳备份。

- 1. 回到 MariaDB 会话并输入 `UNLOCK TABLES;` 以移除锁。

- 2. 回到另一个会话并挂载快照：`mkdir /mnt/snapshot/ -o nouuid /dev/vgdata/lvmariadb-snapshot /mnt/snapshot`。

- 3. 使用 `tar -cvf /root/mariadb.tar /mnt/snapshot/lib/mysql` 创建备份。

- 4. 成功创建备份后，你需要卸载并删除快照：`umount /mnt/snapshot; lvremove /dev/vgdata/lvmariadb-snapshot`。

恢复备份取决于你拥有哪种备份。恢复逻辑备份，你使用类似 `mysql -u root -p videos < /root/videos-db.dump` 的命令。恢复物理备份，你必须先停止 mariadb 服务，之后可以使用 `tar` 恢复备份：

- 1. `systemctl stop mariadb`

- 2. `rm -rf /var/lib/mysql/*`

- 3. `tar xvf /root/mariadb.tar -C /`

在恢复备份之前，务必验证归档文件的内容！

## 总结

在本章中，你学习了 MariaDB 数据库的基础知识。你学习了如何创建一个包含不同表和记录的简单数据库，并学习了如何对该数据库进行基础查询操作。你还学习了如何为数据库创建用户，以及如何进行物理和逻辑备份。

## 考试准备任务

## 复习所有关键主题

复习本章最重要的主题，这些主题在页面外边页用“关键主题”图标标记。表 35.3 列出了这些关键主题及其对应的页码。

### 表 35.3 第 35 章的关键主题

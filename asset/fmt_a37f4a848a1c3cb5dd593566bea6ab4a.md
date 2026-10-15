
```
mysql> SELECT * FROM my_table WHERE age LIKE "2%";
```

MySQL 数据库还可以被其他应用程序（例如 MS Access）远程查询。要允许其他系统查询你的数据库，你可以使用 `GRANT` 命令。要让自己获得从多个域访问数据库的权限，请修改 `DOMAIN_I_WILL_BE_ACCESSING FROM` 并再次运行命令。

```
mysql> GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER

-> ON my database.* TO peter@DOMAIN_I_WILL_BE_ACCESSING FROM

-> IDENTIFIED BY 'peter.password';
```

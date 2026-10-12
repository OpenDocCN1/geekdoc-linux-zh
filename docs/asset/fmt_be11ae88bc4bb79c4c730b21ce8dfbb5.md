
## 1. 项目背景

作为学生，课还需要完成课程任务。IT 协会的学生决定在下次备份的基础上手动备份几个文件到 `/tmp/`。

1) 拷贝到 `/tmp`，并查看，命令如下：

```bash
[root@localhost]# cp -r /etc/* /tmp
[root@localhost]# ls /tmp
```

2) 备份到 `/tmp`，并查看，命令如下：

```bash
[root@localhost]# cp -r root /tmp
[root@localhost]# cd tmp
[root@local tmp]# ll
```

![](img/ec0e03f26e46c767b8ae4c4c4a36e86_56_0.png)

备份系统中的文件

## 2.3 反思与进阶

# Tutorial — Linux Applications

**Max days interval**: 表示两次密码更改之间的最大时间间隔。如果未修改此限制，用户将被永久禁用。当前显示为 `99999`，意味着无需重置密码。

**Warning age**: 当用户的密码过期日期接近上述“最大天数间隔”时，系统将根据此字段的设置发出警告，提醒用户密码将在 `n` 天内过期，应尽快更改。当前显示为 `7` 天。

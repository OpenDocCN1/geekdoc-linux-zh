
```
[root@localhost~]# bash useradd.sh
[root@localhost~]# groupadd class1
[root@localhost~]# tail /etc/group
class1:x:530:std01, std02, std03, std04, std05, std06, std07, std08, std09, std10, std11, std12, std13, std14, std15, std16, std17, std18, std19, std20, std21, std22, std23, std24, std25, std26, std27, std28, std29, std30
```

### 三、操作

1. `[root@localhost~]# useradd -d /home/user01 user01`
2. `[root@localhost~]# tail /etc/group`
   `user01:x:530:/home/user01:/bin/bash`
3. `[root@localhost~]# tail /etc/shadow`
   `user01::18158:0:99999:7::`
4. `[root@localhost~]# password user01`
   更改`user01`的密码。
   新的密码：无效的密码
   无效的密码重新输入密码
   `password`:身份验证更新。
5. `[root@localhost~]# tail /etc/shadow`
   `user01:$S6$OjhFe2zrH1kqBwqx9vbkInxdD1pq77::`
6. 正常登录
7. `[root@localhost~]# passwd -l user01`
   锁定`user01`的密码
   `password`: 操作成功
8. `[root@localhost~]# tail /etc/shadow`
   `user01:!!:$S6$OjhFe2zrH1kqBwqx9vbkInxdD1pq77::`
9. 无法登录
10. `[root@localhost~]# passwd -u user01`
    解锁`user01` 的密码
    `password`: 操作成功
11. `[root@localhost~]# usermod -l user02 user01`
    `[root@localhost~]# tail /etc/shadow`
    `user02:$S6$OjhFe2zrH1kqBwqx9vbkInxdD1pq77::`
12. `[root@localhost~]# userdel -r user02`
13. `[root@localhost~]# groupadd stuff`

# 习题答案

14. `[root@localhost~]# tail /etc/group`
    `stuff:x:532:`
15. `[root@localhost~]# useradd -g stuff user02`
16. `[root@localhost~]# gpasswd stuff`
    Changing the password for group `stuff`
    New Password:
    Re-enter new password:
17. `[root@localhost~]# gpasswd -d user02 stuff`
    Removing `user02` from group `stuff`
18. `[root@localhost~]# tail /etc/group`
    `user01:x:...`
    `stuff:x:532:`
19. `[root@localhost~]# groupdel stuff`

# 项目 5 维护系统的

一、选择题
- 1. C 2. D 3. A 4. A 5. A 7. B

二、填空题
1. `chmod 551 fido`
2. `551` 目录

三、面试
1. (1) 读、写（2）读（3）`chmod +x mydata`
2. `useradd -p zl1234 zhang`
   `groupadd hr`
   `gpasswd -a zhang hr`
   `usermod -s /bin/ksh zhang`
   `touch /home/zhang/zh1.sh`
   `chown zhang /home/zhang/zh1.sh`
   `chmod u+x,g+r,o+r /home/zhang/zh1.sh`

## 项目 6 磁盘管理

一、简答
1. (略)
2. 编辑 `/etc/fstab` 文件在最后一行写入 `/dev/sdb`

## 项目 7 网络通信

一、选择题
- 1. C 2. ACE 3. D

二、填空题
1. `defaults 0`
2. `/sysconfig/network`

# 项目 8 部署 DHCP

一、选择题
- 1. A 2. D 3. C 4. A 5. B 6. C

二、填空题
1. 动态主机配置
2. 探测阶段 请求阶段 确认阶段
3. `DHCP`

## 项目 9 部署 NFS 服务

一、选择题
- 1. C 2. A 3. C

二、填空题
1. Network File 系统
2. Remote Procedure Call
3. `DHCP`

## 项目 10 部署 Samba 服务

一、选择题
- 1. D 2. A 3. D 4. A

二、填空题
1. `rpm -q smb`
2. `smpasswd`
3. `/etc/rc.d/init.d/smb`
4. `test`

# 项目 11 部署 FTP 服务

一、选择题
- 1. B 2. C 3. C 4. B 5. D 6. C

二、填空题
1. 文件传输
2. 主动传输, 被动传输

# 项目 12 部署 DNS 服务

一、选择题
- 1. A 2. C 3. C 4. B 5. D 6. C 7. B

二、填空题
1. `dig`
2. `/etc/hosts`
3.

# 项目 13 部署 Web 服务

一、选择题
- 1. C 2. C 3. A 4. A

二、填空题
1. `httpd` 页面
2. `http`
3. `service http`

# 项目 14 部署电子邮件服务

三、选择题
- 1. E 2. AD 3. A 4. D

四、填空题
1. 用户名 邮箱地址
2. `POP3`
3. `25`

# 项目 15 部署 MariaDB 服务

五、选择题
- 1. B 2. D 3. C 4. B

# 项目 16 部署防火墙

六、填空题
1. 过滤防火墙 代理防火墙 状态防火墙
2. `filter` 表 `nat`
3. `nat`
4. `firewall-config`
5. 伪装 端口转发(映射)

# 项目 17 部署代理服务

七、选择题
- 1. D 2. C

八、填空题
1. `squid`
2. 正向代理 反向代理
3. `/var/sp/squid`

# 参考文献

- [1] 杨云.Linux操作系统与实训[M]. 北京: 中国铁路出版社, 2018.
- [2] 顾润龙, 刘智睿,侯玉香. Linux 操作系统及应用技术[M]. 北京: 航空工业出版社, 2016.
- [3] 曹江华, 杨骁勇. Red Hat Enterprise Linux 7.0 系统管理[M]. 北京: 电子工业出版社, 2015.
- [4] 潘奎, 雨峰. Red Hat Enterprise Linux 6 服务器与管理[M]. 大连: 东软电子出版社, 2015.
- [5] 张敬东. Linux 服务器配置与管理[M]. 北京: 清华大学出版社, 2014.
- [6] 张同光, 陈明, 李跃跃, 等. Linux 操作系统(RHEL/CentOS)[M]. 北京: 清华大学出版社, 2016.

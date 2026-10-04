
# 如果你有需要，可以在这里放置自己的初始化步骤

## 我们想实现 S V 风格的初始化脚本

```
/sbin/ifconfig eth0 down
/sbin/ifconfig eth1 down
/usr/sbin/brctl addif eth0
/usr/sbin/brctl addif eth1
/sbin/ifconfig eth0 up
/sbin/ifconfig eth1 up
touch /var/lock/subsys/local
```

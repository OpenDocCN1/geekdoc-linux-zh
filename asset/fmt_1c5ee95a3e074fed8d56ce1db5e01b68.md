
在这里我们查看三种设备类型，以及它们在驱动程序上线时如何让操作系统感知。

> 图 2.21 字符设备注册：`linux/fs/devices.c`。

```c
100 if (major == 0) {
101   write_lock(&chdevs_lock);
102   for (major = MAX_CHDEV-1; major > 0; major--) {
103     if (chdevs[major].fops == NULL) {
104       chdevs[major].name = name;
105       chdevs[major].fops = fops;
106       write_unlock(&chdevs_lock);
107       return major;
108     }
109   }
110  }
111  write_unlock(&chdevs_lock);
112  return = -EBUSY;
113  if (major >= MAX_CHDEV) {
114   return -EINVAL;
115   write_lock(&chdevs_lock);
116   if (chdevs[major].fops && chdevs[major].fops) {
117     write_unlock(&chdevs_lock);
```

## Linux 操作系统简介 57

```c
119 return -EBUSY;
120 chrdevs[major].name = name;
121 chrdevs[major].fops = fops;
122 write_unlock(&chdevs_lock);
123 return 0;
124 }
125
126 int register_chrdev(unsigned int major, const char * name)
127 {
128 if (major >= MAX_CHDEV)
129 return -EINVAL;
130 write_lock(&chdevs_lock);
131 if (chrdevs[major].fops != strcmp(chrdevs[major].name, name)) {
132 write_unlock(&chdevs_lock);
133 return -EINVAL;
134 }
135 chrdevs[major].name = NULL;
136 chrdevs[major].fops = NULL;
137 write_unlock(&chdevs_lock);
138 return 0;
139 }
141 /*
```

图 2.22 设备注册：`linux/fs/block_dev.c`。

```c
478 len = sprintf(p, "% devices:\n");
479 for (int i = 0; i < MAX_BLKDEV; i++) {
480 if (blkdevs[i].bdops) {
481 len += sprintf(p+len, "%3d %s\n", i, bldevs[i].name);
483 }
484 }
485 return len;
486 }
487 /*
488 返回设备的函数表。
489 如果需要，加载驱动程序。
490 */
491 const struct block_device_operations *get_blkfops(unsigned int major)
492 {
494 const struct block_device_operations *ret = NULL;
495 /* major 0 用于非设备 */
496 if (major >= 0 && major < MAX_BLKDEV) {
497 #ifdef CONFIG_BLKID
498 if (blkdevs[major].bdops) {
499 char name[20];
500 sprintf(name, "block-major-%d", major);
501 request_module(name);
502 }
503 #endif
505 **
```

## 58 TCP/IP 和 Linux 协议实现

```c
504 ret = blkdevs[major].bdops;

505 

506 return ret;

507 }

508

509 int register_blkdev(unsigned int major, const char * name, struct block_device_operations
*bdops)

510 {
```

图 2.23 Linux 网络设备注册 i：`linux/net/core/dev.c`。

```c
2151 /*
2152  * 查看调用者在论论哪个接口。
2153  */

2154

2155 switch(cmd);

2156 {

2157     /*
2158     * 这些 ioctl 调用：
2159     * - 所有人都可以执行。
2160     * - 是原子的且不需要锁。
2161     * - 返回一个值
2162     */

2163     case SIOCGIFFLAGS:

2164     case SIOCGIMETRIC:

2165     case SIOCGIFMTU:

2166     case SIOCGIFADDR:

2167     case SIOCGIFSLAVE:

2168     case SIOCGIFMAP:

2169     case SIOCGIFINDEX:

2170     case SIOCGIFLEN:

2171     dev_load(ifr.name);

2172     write_lock(&dev_base_lock);

2173     ret = dev_ifctl(&ifr, cmd);

2174     read_unlock(&dev_base_lock);

2175     if (ret) {

2176         colon = ':';

2177         if (copy_to_user(arg, &ifr, sizeof(struct))
2178             return -EFAULT;

2179     }
2180     return ret;

2181 }

2182

2183 /* - 需要超级用户权限。
2184     * - 需要严格序列化。
2185     * - 不返回一个值
2186 */
```

## Linux 操作系统简介 59

### 图 2.24 网络设备注册 ii：`linux/net/core/dev.c`。

```c
case SIOCSIFFLAGS:

case SIOCSFIMRIC:

case SIOCSITMU:

case SIOCSIMAP:

case SIOCSIHWAND:

case SIOCSIFLAVE:

case SIOCADDMULTI:

case SIOCDELMULTI:

case SIOCSIROADCAST:

case SIOCSIFTQLEN:

case SIOCSIFNAME:

case SIOCGETTOOL:

if (!capable(CAP_NET_ADMIN)) {

    return -EPERM;

}

dev_load(ifr.ifr_name);

dev_probe_lock();

tnl_lock();

ret = dev_ifsloc(&ifr, cmd);

tnl_unlock();

dev_probe_unlock();

return ret;

}
```

### 图 2.25 网络设备注册 iii：`linux/net/core/dev.c`。

```c
case SIOCDGIFEM:
    /* 获取设备的内存空间。我们可以添加它，但目前
   不支持它 */
case SIOCSIFMEM:
    /* 设置设备的内存缓冲区。在我们的案例中不适用 */
case SIOCSIFLINK:
    return -EINVAL;

/*
   未知或私有的 ioctl。
*/
default:
    if (cmd <= SIOCDEVPPRIVATE + 15) {
        dev_load(ifr.ifr_name);
        dev_probe_lock();
        ntnl_lock();
        ret = dev_ifsloc(&ifr, cmd);
        ntnl_unlock();
        dev_probe_unlock();
        if (ret & copy_to_user(user, &ifr, sizeof(struct)))
            return -EFAULT;
    }
```

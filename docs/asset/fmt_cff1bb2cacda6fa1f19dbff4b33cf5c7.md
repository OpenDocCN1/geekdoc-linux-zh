
```c
#include <linux/module.h>
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/proc_fs.h>

MODULE_AUTHOR("Test Author (laus@Linux-netzwerkarchitektur.de)");
MODULE_DESCRIPTION("这是一个示例模块");

/* 模块变量 */
unsigned int variable1;
unsigned long variable2[3] = {0, 1, 2};

/* 函数; 将被作为符号导出 */
void method(int test1, char *test2);

register_proc_files() {
    struct proc_dir_entry *test_dir;
    struct proc_dir_entry *entry;

    test_dir = proc_create("test", &proc_root, NULL, NULL, test_proc_get_info);
    if (!test_dir) {
        printk(KERN_DEBUG "Error创建 /proc/test.");
        return;
    }
    entry = proc_create("rw", 0644, test_dir, NULL);
    if (entry) {
        entry->data = (void *)&variable1;
        entry->read_proc = test_proc_read;
        entry->write_proc = test_proc_write;
    }
}

unregister_proc_files() {
    remove_proc_entry("test", NULL); // 注意：OCR 中的逻辑似乎不完整，但保留了结构
    remove_proc_entry("rw", NULL);
    remove_proc_entry("test", NULL);
}

test_proc_read(char *buf, char **start, off_t offset, int count, int *eof, void *data) {
    unsigned int *ptr_var1 = data;
    return sprintf(buf, "%u\n", *ptr_var1);
}

test_proc_write(struct file *file, const char *buffer) {
    unsigned int *ptr_var1 = data;
    printk(KERN_DEBUG "TEST: variable1 设置为: %s", buffer);
    *ptr_var1 = simple_strtoul(buffer, NULL, 10);
    return count;
}

test_proc_get_info(char *buf, char **start, off_t offset, int len) {
    len = sprintf(buf, "\n 这是一个测试模块\n");
    len += sprintf(buf, " Integer: %u\n", variable1);
    len += sprintf(buf, " Long[0]: %lu\n", variable2[0]);
    len += sprintf(buf, " Long[1]: %lu\n", variable2[1]);
    len += sprintf(buf, " Long[2]: %lu\n", variable2[2]);
    return len;
}

int skull_init(void) {
    /* 注册模块的功能， */
    /* 例如：register_netdevice, inet_add_protocol, dev_add_pack, 等. */
    #ifdef CONFIG_PROC_FS
    register_proc_files();
    #endif
    return 0;
}

void skull_cleanup(void) {
    /* 注销模块的功能， */
    /* 例如：unregister_netdevice, inet_del_protocol, dev_remove_pack, 等. */
    #ifdef CONFIG_PROC_FS
    unregister_proc_files();
    #endif
}

module_init(skull_init);
module_exit(skull_cleanup);
```

```c
(void *) 1,
NULL
};
int test_pack_rcv(struct sk_buff *skb, struct net_device *dev, struct
    packet_type *pt)
{
    printk(KERN_DEBUG "Test protocol: Packet Received with length: %u\n",
    skb->len);
    return skb->len;
}
int init_module(void)
{
    dev_add_pack(&test_protocol);
    return 0;
}
void cleanup_module(void)
{
    dev_remove_pack(&test_protocol);
}
```

## 录录 F

### 传输协议示例

**传输协议示例**

编译：

`gcc -I/lib/modules/uname -r/build/include -c file.c`

```c
#ifndef __KERNEL__
#define __KERNEL_
#endif
#ifndef MODULE
#define MODULE
#endif

#include <linux/module.h>
#include <linux/version.h>
#include <linux/kernel.h>
#include <linux/init.h>
#include <linux/skbuff.h>
#include <linux/in.h>
#include <net/protocol.h>

MODULE_AUTHOR("Test Author (fixme@Linux-netzwerkarchitektur.de)")
MODULE_DESCRIPTION("带有四层测试协议的模块");

int test_proto_rcv(struct sk_buff *skb);
static struct inet_protocol test_protocol = {
	&test_proto_rcv,    /* 协议处理器 */
	NULL,               /* 错误控制 */
	NULL,               /* 下一个 */
	IPPROTO_TCP,        /* 协议 ID */
};
```

```c
0,
NULL,                /* 拷贝 *//* 数据 */
    "Test_Protocol"      /* 名称 */
;
int test_proto_rcv(struct sk_buff *skb)
{
    printk(KERN_DEBUG "Test protocol: Packet Received with length: %u\n",
           skb->len);
    return skb->len;
}
int init_module(void)
{
    inet_add_protocol(&test_protocol);
    return 0;
}
void cleanup_module(void)
{
    inet_del_protocol(&test_protocol);
}
```

## 录录 G

### 基于 Socket 的通信示例

#### G.1 服务器端

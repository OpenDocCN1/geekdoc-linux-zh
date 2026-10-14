
```c
ssize_t (*show)(struct class *class, struct class_attribute *attr,
                char *buf);

ssize_t (*store)(struct class *class, struct class_attribute *attr,
                 const char *buf, size_t count);
};
```

在 `vinput.c` 中，`include/linux/device.h` 中定义的宏 `CLASS_ATTR_WO(export)` 和 `CLASS_ATTR_WO(unexport)`（在这种情况下，`device.h` 在 `include/linux/input.h` 中被包含）将生成名为 `class_attr_export` 和 `class_attr_unexport` 的 `class_attribute` 结构。然后，将它们放入 `vinput_class_attrs` 数组中，宏 `ATTRIBUTE_GROUPS(vinput_class)` 将生成 `struct attribute_group` `vinput_class_group`，该组应分配给 `vinput_class`。最后，调用 `class_register(&vinput_class)` 在 sysfs 中创建属性。

要创建 `vinputX` sysfs 条目和 `/dev` 节点。

```sh
echo "ykbd" | sudo tee /sys/class/input/export
```

要取消导出设备，只需在 `unexport` 中回显其 id 即可：

```sh
echo "0" | sudo tee /sys/class/input/unexport
```

```c
/*
 * vinput.h
 */

#ifndef VINPUT_H
#define VINPUT_H

#include <linux/input.h>
#include <linux/spinlock.h>
#define VINPUT_MAX_LEV 128
#define MAX_VINPUT 32
#define VINPUT_MINORS MAX_VINPUT
#define dev_to_vinput(dev) container_of(dev, struct vinput, dev)

struct vinput_device;

struct vinput {
    long id;
    long devno;
    long last_entry;
    spinlock_t lock;
    void *priv_data;
    struct device dev;
    struct list_head list;
    struct input_dev *input;
    struct vinput_device *type;
};

struct vinput_ops {
    int (*init)(struct vinput *);
    int (*kill)(struct vinput *);
    int (*send)(struct vinput *, char *, int);
    int (*read)(struct vinput *, char *, int);
};

struct vinput_device {
    char name[16];
    struct list_head list;
    struct vinput_ops *ops;
};

int vinput_register(struct vinput_device *dev);
void vinput_unregister(struct vinput_device *dev);
#endif

/*
 * vinput.c
 */

#include <linux/cdev.h>
#include <linux/input.h>
#include <linux/module.h>
#include <linux/slab.h>
#include <linux/spinlock.h>
#include <linux/version.h>
#include <asm/uaccess.h>
#include "vinput.h"

#define DRIVER_NAME "vinput"
#define dev_to_vinput(dev) container_of(dev, struct vinput, dev)

static DECLARE_BITMAP(vinput_ids, VINPUT_MINORS);
static LIST_HEAD(vinput_devices);
static LIST_HEAD(vinput_vdevices);
static int vinput_dev;
static spinlock_t vinput_lock;
static struct class vinput_class;

/* Search the name of vinput device in the vinput_devices linked list,
 * which added at vinput_register().
 */
static struct vinput_device *vinput_get_device_by_type(const char *type)
{
    int found = 0;
    struct vinput_device *vinput;
    struct list_head *curr;
    spin_lock(&vinput_lock);
    list_for_each (curr, &vinput_devices) {
        vinput = list_entry(curr, struct vinput_device, list);
        if (vinput && strncmp(type, vinput->name, strlen(vinput->name)) == 0) {
            found = 1;
            break;
        }
    }
    spin_unlock(&vinput_lock);
    if (found)
        return vinput;
    return ERR_PTR(-ENODEV);
}

/* Search the id of virtual device in the vinput_vdevices linked list,
 * which added at vinput_alloc_device().
 */
static struct vinput *vinput_get_vdevice_by_id(long id)
{
    struct vinput *vinput = NULL;
    struct list_head *curr;
    spin_lock(&vinput_lock);
    list_for_each (curr, &vinput_vdevices) {
        vinput = list_entry(curr, struct vinput, list);
        if (vinput && vinput->id == id)
            break;
    }
    spin_unlock(&vinput_lock);
    if (vinput && vinput->id == id)
        return vinput;
    return ERR_PTR(-ENODEV);
}

static int vinput_open(struct inode *inode, struct file *file)
{
    int err = 0;
    struct vinput *vinput = NULL;
    vinput = vinput_get_vdevice_by_id(imino(inode));
```

```c
if (IS_ERR(vinput))
    err = PTR_ERR(vinput);
else
    file->private_data = vinput;
return err;
}

static int vinput_release(struct inode *inode, struct file *file)
{
    return 0;
}

static ssize_t vinput_read(struct file *file, char __user *buffer, size_t count,
```

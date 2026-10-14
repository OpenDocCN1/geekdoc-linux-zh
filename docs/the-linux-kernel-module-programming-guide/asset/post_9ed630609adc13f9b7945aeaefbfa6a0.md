
```
}
module_init(vinput_init);
module_exit(vinput_end);

MODULE_LICENSE("GPL");
MODULE_DESCRIPTION("Emulate input events");
```

Here the virtual keyboard is one of example to use vinput. It supports all KEY_MAX keycodes. The injection format is the KEY_CODE such as defined in include/linux/input.h. A positive value means KEY_PRESS while a negative value is a KEY_RELEASE. The keyboard supports repetition when the key stays pressed for too long. The following demonstrates how simulation work.
Simulate a key press on "g" (KEY_G = 34):

```
echo "+34" | sudo tee /dev/vinput0
```

Simulate a key release on "g" (KEY_G = 34):

```
echo "-34" | sudo tee /dev/vinput0
```

```
/*
 * vkbd.c
 */

#include <linux/init.h>
#include <linux/input.h>
#include <linux/module.h>
#include <linux/spinlock.h>

#include "vinput.h"

#define VINPUT_KBD "vkbd"
#define VINPUT_RELEASE 0
#define VINPUT_PRESS 1

static unsigned short vkeymap[KEY_MAX];

static int vinput_vkbd_init(struct vinput *vinput)
{
    int i;

    /* Set up the input bitfield */
    vinput->input->evbit[0] = BIT_MASK(EV_KEY) | BIT_MASK(EV_REP);
    vinput->input->keycodesize = sizeof(unsigned short);
    vinput->input->keymax = KEY_MAX;
    vinput->input->keycode = vkeymap;

    for (i = 0; i < KEY_MAX; i++)
        set_bit(vkeymap[i], vinput->input->keybit);
```
```
30
31  /* vinput will help us allocate new input device structure via
32   * input_allocate_device(). So, we can register it straightforwardly.
33   */
34  return input_register_device(vinput->input);
35 }
36
37 static int vinput_vkbd_read(struct vinput *vinput, char *buff, int len)
38 {
39     spin_lock(&vinput->lock);
40     len = sprintf(buff, len, "%d\n", vinput->last_entry);
41     spin_unlock(&vinput->lock);
42
43     return len;
44 }
45
46 static int vinput_vkbd_send(struct vinput *vinput, char *buff, int len)
47 {
48     int ret;
49     long key = 0;
50     short type = VINPUT_PRESS;
51
52     /* Determine which event was received (press or release)
53      * and store the state.
54      */
55     if (buff[0] == '+')
56         ret = kstrtol(buff + 1, 10, &key);
57     else
58         ret = kstrtol(buff, 10, &key);
59     if (ret)
60         dev_err(&vinput->dev, "error during kstrtol: %d\n", ret);
61     spin_lock(&vinput->lock);
62     vinput->last_entry = key;
63     spin_unlock(&vinput->lock);
64
65     if (key < 0) {
66         type = VINPUT_RELEASE;
67         key = -key;
68     }
69
70     dev_info(&vinput->dev, "Event %s code %d\n",
71              (type == VINPUT_RELEASE) ? "VINPUT_RELEASE" : "VINPUT_PRESS",
72              key);
73
74     /* Report the state received to input subsystem. */
75     input_report_key(vinput->input, key, type);
76     /* Tell input subsystem that it finished the report. */
77     input_sync(vinput->input);
78
79     return len;
80 }
81
82 static struct vinput_ops vkbd_ops = {
83     .init = vinput_vkbd_init,
84     .send = vinput_vkbd_send,
85     .read = vinput_vkbd_read,
86 };
```
```
86 static struct vinput_device vkbd_dev = {
87     .name = VINPUT_KBD,
88     .ops = &vkbd_ops,
89 };
91 static int __init vkbd_init(void)
92 {
93     int i;
95     for (i = 0; i < KEY_MAX; i++)
96         vkeymap[i] = i;
97     return vinput_register(&vkbd_dev);
99 }
101 static void __exit vkbd_end(void)
102 {
103     vinput_unregister(&vkbd_dev);
104 }
106 module_init(vkbd_init);
107 module_exit(vkbd_end);
109 MODULE_LICENSE("GPL");
110 MODULE_DESCRIPTION("Emulate keyboard input events through /dev/vinput");
```

## 17 Standardizing the interfaces: The Device Model

Up to this point we have seen all kinds of modules doing all kinds of things, but there was no consistency in their interfaces with the rest of the kernel. To impose some consistency such that there is at minimum a standardized way to start, suspend and resume a device model was added. An example is shown below, and you can use this as a template to add your own suspend, resume or other interface functions.

```
1 /*
2  * devicemodel.c
3  */
4 #include <linux/kernel.h>
5 #include <linux/module.h>
6 #include <linux/platform_device.h>
7 #include <linux/version.h>
9 struct devicemodel_data {
10     char *greeting;
11     int number;
12 };
14 static int devicemodel_probe(struct platform_device *dev)
15 {
16     struct devicemodel_data *pd =
17         (struct devicemodel_data *)(dev->dev.platform_data);
```

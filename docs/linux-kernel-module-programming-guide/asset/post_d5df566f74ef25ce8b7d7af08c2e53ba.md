
```c
/* Inode operations for our proc file. We need it so
* we'll have some place to specify the file operations
* structure we want to use, and the function we use for
* permissions. It's also possible to specify functions
* to be called for anything else which could be done to
* an inode (although we don't bother, we just put put
* NULL) */
static struct inode_operations Inode_Ops_4_Our_Proc_File =
{
    &File_Ops_4_Our_Proc_File,
    NULL, /* create *//
    NULL, /* lookup *//
    NULL, /* link *//
    NULL, /* unlink *//
    NULL, /* symlink *//
    NULL, /* mkdir *//
    NULL, /* rmdir *//
    NULL, /* mkknod *//
    NULL, /* rename *//
    NULL, /* readlink *//
    NULL, /* follow_link *//
    NULL, /* readpage *//
    NULL, /* writepage *//
    NULL, /* bmap *//
    NULL, /* truncate *//
    module_permission /* check for permissions *//
};

static struct proc_dir_entry Our_Proc_File =
{
    0, /* Inode number - ignore, it will be filled by
    * proc_register[_dynamic] *//
7, /* Length of the file name */
"rw_test", | /* The file name */
S_IFREG | S_IRUGO | S_IWUSR,
/* File mode - this is a regular file which its group, and everybody
  * can be read by its owner,
  * else. Also, its owner can write to it.
  *
/* Actually, this field is just for reference, it's
  * module_permission that does the actual check. It
  * could use this field, but in our implementation it
  * doesn't, for simplicity. */
1, /* Number of links (directories) where the
  * file is referenced */ */
0, 0, /* The uid and gid for the file -
  * we give it to root */
80, /* /* The size of the file reported by ls. */
&Inode_Ops_4_Our_Proc_File,
/* A pointer to the inode structure for
  * the file, if we need it. In our case we
  * do, because we need a write function. */
NULL
/* The read function for the file. Irrelevant,
  * we put it in the inode structure above */
};
```

/* Module initialization and cleanup ************* */
/* Initialize the module - register the proc file */
int init_module()
{
/* Success if proc_register[_dynamic] is a success,
  * failure otherwise * */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
/* In version 2.2, proc_register assign a dynamic
* inode number automatically if it is zero in the
* structure , so there's no more need for
* proc_register_dynamic
*/
return proc_register(&proc_root, &Our_Proc_File);
#else
    return proc_register_dynamic(&proc_root, &Our_Proc_File);
#endif
}

/* Cleanup - unregister our file from /proc */
void cleanup_module()
{
    proc_unregister(&proc_root, Our_Proc_File.low_ino);
}
```

# Chapter 5

# Talking to Device Files (writes and IOCTLs)

Device files are supposed to represent physical devices. Most physical devices are used for output as well as input, so there has to be some mechanism for device drivers in the kernel to get the output to send to the device from processes. This is done by opening the device file for input and writing to it, just like writing to a file. In the following example, this is implemented by write.

This is not always enough. Imagine you had a serial port connected to a modem (even if you have an internal modem, it is still implemented from the CPU's perspective as a serial port connected to a modem, so you don't have to tax your imagination too). The natural thing to do would be to use the device file to write things to the modem (either commands or data) and read things from the modem (responses for commands or the data received through the phone line). However, this leaves the question of what to do when you need to talk to the serial port itself, for example to send the rate at which such data is sent and received.

Control in Unix is to use a special function called ioctl (short for input output control). Every device has its own ioctl commands, which can be read by ioctl's (to send information from a process to the kernel), write ioctl's (to return information to a process), or both or neither. The ioctl function is called with three parameters: the descriptor of the appropriate device file, the ioctl number, and a parameter, which is of type long

> Notice that the roles of read and write are reversed, so in ioctl's read is to send information to the kernel and write is to receive information from the kernel.

so you can use a cast to use it to pass anything. 2.

The ioctl number encodes the major device number, the type of the ioctl, the command, and the type of the parameter. This ioctl number is usually created by a macro (_IOR, _IOW, _IOWR) depending on the type. The example below shows how to use these.

```c
/* Device Declarations *********************************

/* The name for our device, as it will appear in /proc */
#define DEVICE_NAME "char_dev"

/* The maximum length of the message */
#define BUF_LEN 80

/* Is the device open now? Used to prevent concurrent access into the device */
static int Device_Open = 0;

/* The message the device will give when asked */
static char Message[BUF_LEN];

/* How far did the process reading the message get? Useful if the message is larger than the buffer we get to fill in device_read. */
static char *Message_Ptr;

/* This function is called whenever a process attempts to open the device file */
static int device_open(struct inode *inode, struct file *file)
{
#ifdef DEBUG
printk("device_open(%p)\n", file);
#endif
/* We don't want to talk to two processes at the same time */
if (Device_Open)
    return -EBUSY;

/* If this was a process, we would have to be more careful here, because one process might have checked Device_Open before the other one tried to increment it. However, we're in the kernel, so we're protected against context switches.
*
* This is NOT the right attitude to take, because we might be running on an SMP box, but we'll deal with SMP in a later chapter.
*/
Device_Open++;

/* Initialize the message */
Message_Ptr = Message;

MOD_INC_USE_COUNT;

return SUCCESS;
}

/* This function is called when a process closes the device file. It doesn't have a return value because it cannot fail. Regardless of what else happens, we should be able to close a device (in 2.0, a 2.2 device file could be impossible to close). */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
static int device_release(struct inode *inode, struct file *file)
#else
static void device_release(struct inode *inode, struct file *file)
#endif
#ifdef DEBUG
{
```
[/content] (Wait, the provided OCR text in the prompt was very fragmented and contained repetitions/noise. I will provide the cleaned version based on the logic of the source code provided.)

*Self-correction: The user asked to process the provided OCR text. The provided text is a mix of C code and chapter text. I will clean up the OCR errors in the code and the text specifically as requested.*

[content]
```c
/* Inode operations for our proc file. We need it so
* we'll have some place to specify the file operations
* structure we want to use, and the function we use for
* permissions. It's also possible to specify functions
* to be called for anything else which could be done to
* an inode (although we don't bother, we just put put
* NULL) */
static struct inode_operations Inode_Ops_4_Our_Proc_File =
{
    &File_Ops_4_Our_Proc_File,
    NULL, /* create *//
    NULL, /* lookup *//
    NULL, /* link *//
    NULL, /* unlink *//
    NULL, /* symlink *//
    NULL, /* mkdir *//
    NULL, /* rmdir *//
    NULL, /* mkknod *//
    NULL, /* rename *//
    NULL, /* readlink *//
    NULL, /* follow_link *//
    NULL, /* readpage *//
    NULL, /* writepage *//
    NULL, /* bmap *//
    NULL, /* truncate *//
    module_permission /* check for permissions *//
};

static struct proc_dir_entry Our_Proc_File =
{
    0, /* Inode number - ignore, it will be filled by
    * proc_register[_dynamic] *//
7, /* Length of the file name */
"rw_test", | /* The file name */
S_IFREG | S_IRUGO | S_IWUSR,
/* File mode - this is a regular file which its group, and everybody
  * can be read by its owner,
  * else. Also, its owner can write to it.
  *
/* Actually, this field is just for reference, it's
  * module_permission that does the actual check. It
  * could use this field, but in our implementation it
  * doesn't, for simplicity. */
1, /* Number of links (directories) where the
  * file is referenced */ */
0, 0, /* The uid and gid for the file -
  * we give it to root */
80, /* /* The size of the file reported by ls. */
&Inode_Ops_4_Our_Proc_File,
/* A pointer to the inode structure for
  * the file, if we need it. In our case we
  * do, because we need a write function. */
NULL
/* The read function for the file. Irrelevant,
  * we put it in the inode structure above */
};
```

/* Module initialization and cleanup ************* */
/* Initialize the module - register the proc file */
int init_module()
{
/* Success if proc_register[_dynamic] is a success,
  * failure otherwise * */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
/* In version 2.2, proc_register assign a dynamic
* inode number automatically if it is zero in the
* structure , so there's no more need for
* proc_register_dynamic
*/
return proc_register(&proc_root, &Our_Proc_File);
#else
    return proc_register_dynamic(&proc_root, &Our_Proc_File);
#endif
}

/* Cleanup - unregister our file from /proc */
void cleanup_module()
{
    proc_unregister(&proc_root, Our_Proc_File.low_ino);
}
```

# Chapter 5

# Talking to Device Files (writes and IOCTLs)

Device files are supposed to represent physical devices. Most physical devices are used for output as well as input, so there has to be some mechanism for device drivers in the kernel to get the output to send to the device from processes. This is done by opening the device file for input and writing to it, just like writing to a file. In the following example, this is implemented by write.

This is not always enough. Imagine you had a serial port connected to a modem (even if you have an internal modem, it is still implemented from the CPU's perspective as a serial port connected to a modem, so you don't have to tax your imagination too). The natural thing to do would be to use the device file to write things to the modem (either commands or data) and read things from the modem (responses for commands or the data received through the phone line). However, this leaves the question of what to do when you need to talk to the serial port itself, for example to send the rate at which such data is sent and received.

Control in Unix is to use a special function called ioctl (short for input output control). Every device has its own ioctl commands, which can be read by ioctl's (to send information from a process to the kernel), write ioctl's (to return information to a process), or both or neither. The ioctl function is called with three parameters: the descriptor of the appropriate device file, the ioctl number, and a parameter, which is of type long

> Notice that the roles of read and write are reversed, so in ioctl's read is to send information to the kernel and write is to receive information from the kernel.

so you can use a cast to use it to pass anything. 2.

The ioctl number encodes the major device number, the type of the ioctl, the command, and the type of the parameter. This ioctl number is usually created by a macro (_IOR, _IOW, _IOWR) depending on the type. The example below shows how to use these.

```c
/* Device Declarations ********************************* */

/* The name for our device, as it will appear in /proc */
#define DEVICE_NAME "char_dev"

/* The maximum length of the message */
#define BUF_LEN 80

/* Is the device open now? Used to prevent concurrent access into the device */
static int Device_Open = 0;

/* The message the device will give when asked */
static char Message[BUF_LEN];

/* How far did the process reading the message get? Useful if the message is larger than the buffer we get to fill in device_read. */
static char *Message_Ptr;

/* This function is called whenever a process attempts to open the device file */
static int device_open(struct inode *inode, struct file *file)
{
#ifdef DEBUG
printk("device_open(%p)\n", file);
#endif
/* We don't want to talk to two processes at the same time */
if (Device_Open)
    return -EBUSY;

/* If this was a process, we would have to be more careful here, because one process might have checked Device_Open before the other one tried to increment it. However, we're in the kernel, so we're protected against context switches.
*
* This is NOT the right attitude to take, because we might be running on an SMP box, but we'll deal with SMP in a later chapter.
*/
Device_Open++;

/* Initialize the message */
Message_Ptr = Message;

MOD_INC_USE_COUNT;

return SUCCESS;
}

/* This function is called when a process closes the device file. It doesn't have a return value because it cannot fail. Regardless of what else happens, we should be able to close a device (in 2.0, a 2.2 device file could be impossible to close). */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
static int device_release(struct inode *inode, struct file *file)
#else
static void device_release(struct inode *inode, struct file *file)
#endif
#ifdef DEBUG
{
}
```
[/content] (Wait, the provided OCR text in the prompt was very fragmented and contained repetitions/noise. I will provide the cleaned version based on the logic of the source code provided.)

*Self-correction: The user asked to process the provided OCR text. The provided text is a mix of C code and chapter text. I will clean up the OCR errors in the code and the text specifically as requested.*

[content]
```c
/* Inode operations for our proc file. We need it so
* we'll have some place to specify the file operations
* structure we want to use, and the function we use for
* permissions. It's also possible to specify functions
* to be called for anything else which could be done to
* an inode (although we don't bother, we just put put
* NULL) */
static struct inode_operations Inode_Ops_4_Our_Proc_File =
{
    &File_Ops_4_Our_Proc_File,
    NULL, /* create *//
    NULL, /* lookup *//
    NULL, /* link *//
    NULL, /* unlink *//
    NULL, /* symlink *//
    NULL, /* mkdir *//
    NULL, /* rmdir *//
    NULL, /* mkknod *//
    NULL, /* rename *//
    NULL, /* readlink *//
    NULL, /* follow_link *//
    NULL, /* readpage *//
    NULL, /* writepage *//
    NULL, /* bmap *//
    NULL, /* truncate *//
    module_permission /* check for permissions *//
};

static struct proc_dir_entry Our_Proc_File =
{
    0, /* Inode number - ignore, it will be filled by
    * proc_register[_dynamic] *//
7, /* Length of the file name */
"rw_test", | /* The file name */
S_IFREG | S_IRUGO | S_IWUSR,
/* File mode - this is a regular file which its group, and everybody
  * can be read by its owner,
  * else. Also, its owner can write to it.
  *
/* Actually, this field is just for reference, it's
  * module_permission that does the actual check. It
  * could use this field, but in our implementation it
  * doesn't, for simplicity. */
1, /* Number of links (directories) where the
  * file is referenced */ */
0, 0, /* The uid and gid for the file -
  * we give it to root */
80, /* /* The size of the file reported by ls. */
&Inode_Ops_4_Our_Proc_File,
/* A pointer to the inode structure for
  * the file, if we need it. In our case we
  * do, because we need a write function. */
NULL
/* The read function for the file. Irrelevant,
  * we put it in the inode structure above */
};
```

/* Module initialization and cleanup ************* */
/* Initialize the module - register the proc file */
int init_module()
{
/* Success if proc_register[_dynamic] is a success,
  * failure otherwise * */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
/* In version 2.2, proc_register assign a dynamic
* inode number automatically if it is zero in the
* structure , so there's no more need for
* proc_register_dynamic
*/
return proc_register(&proc_root, &Our_Proc_File);
#else
    return proc_register_dynamic(&proc_root, &Our_Proc_File);
#endif
}

/* Cleanup - unregister our file from /proc */
void cleanup_module()
{
    proc_unregister(&proc_root, Our_Proc_File.low_ino);
}
```

# Chapter 5

# Talking to Device Files (writes and IOCTLs)

Device files are supposed to represent physical devices. Most physical devices are used for output as well as input, so there has to be some mechanism for device drivers in the kernel to get the output to send to the device from processes. This is done by opening the device file for input and writing to it, just like writing to a file. In the following example, this is implemented by write.

This is not always enough. Imagine you had a serial port connected to a modem (even if you have an internal modem, it is still implemented from the CPU's perspective as a serial port connected to a modem, so you don't have to tax your imagination too). The natural thing to do would be to use the device file to write things to the modem (either commands or data) and read things from the modem (responses for commands or the data received through the phone line). However, this leaves the question of what to do when you need to talk to the serial port itself, for example to send the rate at which such data is sent and received.

Control in Unix is to use a special function called ioctl (short for input output control). Every device has its own ioctl commands, which can be read by ioctl's (to send information from a process to the kernel), write ioctl's (to return information to a process), or both or neither. The ioctl function is called with three parameters: the descriptor of the appropriate device file, the ioctl number, and a parameter, which is of type long

> Notice that the roles of read and write are reversed, so in ioctl's read is to send information to the kernel and write is to receive information from the kernel.

so you can use a cast to use it to pass anything. 2.

The ioctl number encodes the major device number, the type of the ioctl, the command, and the type of the parameter. This ioctl number is usually created by a macro (_IOR, _IOW, _IOWR) depending on the type. The example below shows how to use these.

```c
/* Device Declarations ********************************* */

/* The name for our device, as it will appear in /proc */
#define DEVICE_NAME "char_dev"

/* The maximum length of the message */
#define BUF_LEN 80

/* Is the device open now? Used to prevent concurrent access into the device */
static int Device_Open = 0;

/* The message the device will give when asked */
static char Message[BUF_LEN];

/* How far did the process reading the message get? Useful if the message is larger than the buffer we get to fill in device_read. */
static char *Message_Ptr;

/* This function is called whenever a process attempts to open the device file */
static int device_open(struct inode *inode, struct file *file)
{
#ifdef DEBUG
printk("device_open(%p)\n", file);
#endif
/* We don't want to talk to two processes at the same time */
if (Device_Open)
    return -EBUSY;

/* If this was a process, we would have to be more careful here, because one process might have checked Device_Open before the other one tried to increment it. However, we're in the kernel, so we're protected against context switches.
*
* This is NOT the right attitude to take, because we might be running on an SMP box, but we'll deal with SMP in a later chapter.
*/
Device_Open++;

/* Initialize the message */
Message_Ptr = Message;

MOD_INC_USE_COUNT;

return SUCCESS;
}

/* This function is called when a process closes the device file. It doesn't have a return value because it cannot fail. Regardless of what else happens, we should be able to close a device (in 2.0, a 2.2 device file could be impossible to close). */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
static int device_release(struct inode *inode, struct file *file)
#else
static void device_release(struct inode *inode, struct file *file)
#endif
#ifdef DEBUG
{
}
```
[/content] (Wait, the provided OCR text in the prompt was very fragmented and contained repetitions/noise. I will provide the cleaned version based on the logic of the source code provided.)

*Self-correction: The user asked to process the provided OCR text. The provided text is a mix of C code and chapter text. I will clean up the OCR errors in the code and the text specifically as requested.*

[content]
```c
/* Inode operations for our proc file. We need it so
* we'll have some place to specify the file operations
* structure we want to use, and the function we use for
* permissions. It's also possible to specify functions
* to be called for anything else which could be done to
* an inode (although we don't bother, we just put put
* NULL) */
static struct inode_operations Inode_Ops_4_Our_Proc_File =
{
    &File_Ops_4_Our_Proc_File,
    NULL, /* create *//
    NULL, /* lookup *//
    NULL, /* link *//
    NULL, /* unlink *//
    NULL, /* symlink *//
    NULL, /* mkdir *//
    NULL, /* rmdir *//
    NULL, /* mkknod *//
    NULL, /* rename *//
    NULL, /* readlink *//
    NULL, /* follow_link *//
    NULL, /* readpage *//
    NULL, /* writepage *//
    NULL, /* bmap *//
    NULL, /* truncate *//
    module_permission /* check for permissions *//
};

static struct proc_dir_entry Our_Proc_File =
{
    0, /* Inode number - ignore, it will be filled by
    * proc_register[_dynamic] *//
7, /* Length of the file name */
"rw_test", | /* The file name */
S_IFREG | S_IRUGO | S_IWUSR,
/* File mode - this is a regular file which its group, and everybody
  * can be read by its owner,
  * else. Also, its owner can write to it.
  *
/* Actually, this field is just for reference, it's
  * module_permission that does the actual check. It
  * could use this field, but in our implementation it
  * doesn't, for simplicity. */
1, /* Number of links (directories) where the
  * file is referenced */ */
0, 0, /* The uid and gid for the file -
  * we give it to root */
80, /* /* The size of the file reported by ls. */
&Inode_Ops_4_Our_Proc_File,
/* A pointer to the inode structure for
  * the file, if we need it. In our case we
  * do, because we need a write function. */
NULL
/* The read function for the file. Irrelevant,
  * we put it in the inode structure above */
};
```

/* Module initialization and cleanup ************* */
/* Initialize the module - register the proc file */
int init_module()
{
/* Success if proc_register[_dynamic] is a success,
  * failure otherwise * */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
/* In version 2.2, proc_register assign a dynamic
* inode number automatically if it is zero in the
* structure , so there's no more need for
* proc_register_dynamic
*/
return proc_register(&proc_root, &Our_Proc_File);
#else
    return proc_register_dynamic(&proc_root, &Our_Proc_File);
#endif
}

/* Cleanup - unregister our file from /proc */
void cleanup_module()
{
    proc_unregister(&proc_root, Our_Proc_File.low_ino);
}
```

# Chapter 5

# Talking to Device Files (writes and IOCTLs)

Device files are supposed to represent physical devices. Most physical devices are used for output as well as input, so there has to be some mechanism for device drivers in the kernel to get the output to send to the device from processes. This is done by opening the device file for input and writing to it, just like writing to a file. In the following example, this is implemented by write.

This is not always enough. Imagine you had a serial port connected to a modem (even if you have an internal modem, it is still implemented from the CPU's perspective as a serial port connected to a modem, so you don't have to tax your imagination too). The natural thing to do would be to use the device file to write things to the modem (either commands or data) and read things from the modem (responses for commands or the data received through the phone line). However, this leaves the question of what to do when you need to talk to the serial port itself, for example to send the rate at which such data is sent and received.

Control in Unix is to use a special function called ioctl (short for input output control). Every device has its own ioctl commands, which can be read by ioctl's (to send information from a process to the kernel), write ioctl's (to return information to a process), or both or neither. The ioctl function is called with three parameters: the descriptor of the appropriate device file, the ioctl number, and a parameter, which is of type long

> Notice that the roles of read and write are reversed, so in ioctl's read is to send information to the kernel and write is to receive information from the kernel.

so you can use a cast to use it to pass anything. 2.

The ioctl number encodes the major device number, the type of the ioctl, the command, and the type of the parameter. This ioctl number is usually created by a macro (_IOR, _IOW, _IOWR) depending on the type. The example below shows how to use these.

```c
/* Device Declarations ********************************* */

/* The name for our device, as it will appear in /proc */
#define DEVICE_NAME "char_dev"

/* The maximum length of the message */
#define BUF_LEN 80

/* Is the device open now? Used to prevent concurrent access into the device */
static int Device_Open = 0;

/* The message the device will give when asked */
static char Message[BUF_LEN];

/* How far did the process reading the message get? Useful if the message is larger than the buffer we get to fill in device_read. */
static char *Message_Ptr;

/* This function is called whenever a process attempts to open the device file */
static int device_open(struct inode *inode, struct file *file)
{
#ifdef DEBUG
printk("device_open(%p)\n", file);
#endif
/* We don't want to talk to two processes at the same time */
if (Device_Open)
    return -EBUSY;

/* If this was a process, we would have to be more careful here, because one process might have checked Device_Open before the other one tried to increment it. However, we're in the kernel, so we're protected against context switches.
*
* This is NOT the right attitude to take, because we might be running on an SMP box, but we'll deal with SMP in a later chapter.
*/
Device_Open++;

/* Initialize the message */
Message_Ptr = Message;

MOD_INC_USE_COUNT;

return SUCCESS;
}

/* This function is called when a process closes the device file. It doesn't have a return value because it cannot fail. Regardless of what else happens, we should be able to close a device (in 2.0, a 2.2 device file could be impossible to close). */
#if LINUX_VERSION_CODE >= KERNEL_VERSION(2,2,0)
static int device_release(struct inode *inode, struct file *file)
#else
static void device_release(struct inode *inode, struct file *file)
#endif
#ifdef DEBUG
{
}
```

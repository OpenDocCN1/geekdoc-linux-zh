
# Bootstrap: Notifier Chain

A blocking notifier chain runs in the process context. The calls in the blocking notification chain, as the name suggests, can be blocked because they run in a process context. The Linux network module uses blocking notifier chains to inform other modules of change in quality of service (QoS) value or addition of a new device. Thus, notifications that are not highly critical can use blocking notifier chains.

The <include/linux/notifier.h> defines the Linux notifier chain framework's key data structures and interface definitions. The key data structure `struct notifier_block` offers a framework for the publisher module to extend events. The subscriber modules, which expect these events, register a callback for the extended events:

```
struct notifier_block {
 int (*notifier_call)(struct notifier_block *, unsigned long,void *);
 struct notifier_block *next;
 int priority;
};
```

The `struct notifier_block` contains a function pointer for the callback functions, and the list extends provision for multiple subscribers. The priority field creates a sorted list of the notifier requests.

The modules (publisher) provide notification support also have to maintain a list head to manage and traverse the notification list. The <include/linux/notifier.h> file defines the prototype of this blocking notifier head as `struct blocking_notifier_head`.

```
struct blocking_notifier_head {
 struct rw_semaphore rwsem;
 struct notifier_block *head;
};
```

The structure maintains a head pointer pointing to the list of subscribers and a semaphore to avoid a race condition.

The Linux notifier chain subsystem also provides interface functions to add and delete `struct notifier_block` objects and from the head of the list. Any subscriber can add to the head of the publisher module's list by using the `block_notifier_chain_register` application programming interface (API). You can delete from the list using `blocking_notifier_chain_unregister`, where *` is the type of notifier chain.

## Chapter 5 = USB Device Notification

### Note

Network drivers often use the notification chain framework.

The `blocking_notifier_chain_register` method operates like a simple linked list program. The method adds the `struct notifier_block` to the blocking_notifier_head head based on the priority set in the notifier block:

```
int blocking_notifier_chain_register(struct blocking_notifier_head *nh, struct notifier_block *nb);
```

You can use `blocking_notifier_chain_unregister`, provided by the notifier framework, to remove the registered `struct notifier_block` callback from the list head:

```
int blocking_notifier_chain_unregister(struct blocking_notifier_head *nh, struct notifier_block *nb);
```

Once you have successfully created the notifier chain, the callbacks have to be executed when a particular event occurs. The `blocking_notifier_call_chain` interface function calls the registered callback functions. This interface function takes the notifier head and traverses it to call the registered functions. With the other parameter, void pointer *`v`, is passed to the subscriber with an unsigned long `val` to indicate the type of event:

```
int blocking_notifier_call_chain(struct blocking_notifier_head *nh, unsigned long val, void *v);
```

Having seen an overview of the notifier chain framework, now you'll see how the Linux USB subsystem uses the notifier chain framework for communication between different modules.

## LINUX USB Notification

The Linux-USB notification framework is part of the uscore functionality, and its key functionality is to communicate or removal of a USB device/bus to other modules, such as the file system or class framework. You can find the USB notification framework's data structure definitions in `linux/usb.h` and the functional implementation in `/drivers/usb/core/notify.c`.

![](img/779a74a6577501a55983f193067274a3_77_0.png)

**Figure 5.1**
Functional breakdown of the USB notification.

A top-down breakdown of this framework would look like Figure 5.1. You can visualize this framework as routines that manage the list and routines that handle notifications.

The routines that manage the lists are exported and act as an interface. The interface functions enable modules to register their callback functions and thereby receive USB device notification.

Having seen the breakdown of the USB notification module, you'll now explore the key data structures, API, and internals.

The notification handler extends support for four events: addition of a USB device, addition of a USB bus, and removal of a USB bus. These events are defined by `linux/usb.h` and are illustrated next. They originate from `usbcore` and subsequently are passed to the other USB modules:

```
/* Events from the usb core **/
#define USB_DEVICE_ADD 0x0001 (Represents addition of a USB device)
#define USB_DEVICE_REMOVE 0x0002 (Represents removal of a USB device)
#define USB_BUS_ADD 0x0003 (Represents addition of a USB bus)
#define USB_BUS_REMOVE 0x0004 (Represents removal of a USB bus)
```

While using a notifier chain, the first step in the process is to define a head of the notification list. The USB notification framework uses a blocking notifier chain to pass on the device notifications, because the information is not that time critical. The `notify.c` declares a notification list head `usb_notifier_list` of type `struct blocking_notifier_head` to maintain information on the list of callbacks registered:

```
static BLOCKING_NOTIFIER_HEAD(usb_notifier_list);
```

Other routines use this head notification link to register and manage the notification list.

Now you'll look at the functions that act on the list. The `usb_register_notify` interface function adds the `notifier_block` passed on to the head pointer `usb_notifier_list`, using the `blocking_notifier_chain_register` function. The `blocking_notifier_chain_register`, which was discussed in the previous section, takes care of the insertion into the list based on the priority set in the `struct_block`:

```
void usb_register_notify(struct notifier_block *nb)
{
 blocking_notifier_chain_register(&usb_notifier_list, nb);
EXPORT_SYMBOL_GPL(usb_register_notify);
}
```

The `usb_unregister_notify` interface function allows other subsystems to remove a `struct notifier_block` object from the `usb_notifier_list`, and the routine internally uses `blocking_notifier_chain_unregister` provided by the Linux notification subsystem to remove the `struct notifier_block` object.

```
void usb_unregister_notify(struct notifier_block *nb)
{
 blocking_notifier_chain_unregister(&usb_notifier_list, nb);
EXPORT_SYMBOL_GPL(usb_unregister_notify);
}
```

With these interface routines, other subscribing can register their blocks with the USB subsystem. Recall from the previous sections that this subsystem publishes four events: USB_DEVICE_ADD, USB_DEVICE_REMOVE, USB_BUS_ADD, and USB_BUS_REMOVE. When these events occur, the publisher must notify the subscriber. To do this, the Linux framework uses blocking_notifier_call_chain. The USB notification module exports the following routines to notify these events:

```
void usb_notify_add_device(struct usb_device *udev)
{
 blocking_notifier_call_chain(&usb_notifier_list, USB_DEVICE_ADD, udev);
}

void usb_notify_remove_device(struct usb_device *udev)
{
  /* Protect against simultaneous us open */
  mutex_lock(&ubsf_mutex);
  blocking_notifier_call_chain(&usb_notifier_list, USB_DEVICE_REMOVE, udev);
  mutex_unlock(&ubsf_mutex);
}
void usb_notify_add_bus(struct usb_bus *ubus)
{
  blocking_notifier_call_chain(&usb_notifier_list, USB_BUS_ADD, ubus);
}
void usb_notify_remove_bus(struct usb_bus *ubus)
{
  blocking_notifier_call_chain(&usb_notifier_list, USB_BUS_REMOVE, ubus);
}
```

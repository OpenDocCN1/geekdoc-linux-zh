![](bbox=[0.125, 0.095, 0.898, 0.368])

**Figure 5.4**nSequence of activities when a device is removed from the system.

Similarly, the usb-generic framework handles any USB device removal as illustrated in Figure 5.4. It passes on the device removal using the usb_notify_remove_device interface function. This function internally traverses the usb_notification_list using the blocking_notifier_call_chain function to pass on the USB_DEVICE_REMOVE information to the subscriber modules.

When the modules are no longer using the USB events, they have to unsubscribe from the USB notification framework. The subscriber modules can unregister their notification block using the usb_unregister_notify interface function. Figure 5.5 illustrates three frameworks of the Linux USB subsystem unregistering their notification blocks with the USB notification framework.

# Writing a Simple USB Notification-Subscriber

In the preceding sections, you learned about the USB notification framework. In this section, you learn how to use this framework to receive information about addition and removal of a USB device. To achieve this, you have to write a simple module that subscribes itself to the USB notification framework and prints a message when a device is added or removed.
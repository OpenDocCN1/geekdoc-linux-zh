```
vms_cleanup(void)
{

/* Unregister from the input subsystem */
input_unregister_device(vms_input_dev);

/* Cleanup sysfs node */
sysfs_remove_group(&vms_dev->dev.kobj, &vms_attr_group);

/* Unregister driver */
platform_device_unregister(vms_dev);
return;
}

module_init(vms_init);
module_exit(vms_cleanup);
```

Let's take a closer look at Listing 7.2. During initialization, the vms driver registers itself as an input device driver. For this, it first allocates an `input_dev` structure using the core API, `input_allocate_device()` :

```
vms_input_dev = input_allocate_device();
```

It then announces that the virtual mouse generates relative events:

```
set_bit(EV_REL, vms_input_dev->evbit);  /* Event Type is EV_REL */
```

Next, it declares the event codes that the virtual mouse produces:

```
set_bit(REL_X, vms_input_dev->relbit); /* Relative 'X' movement */
set_bit(REL_Y, vms_input_dev->relbit); /* Relative 'Y' movement */
```

If your virtual mouse is also capable of generating button clicks, you need to add this to `vms_init()`:

```
set_bit(EV_KEY, vms_input_dev->evbit);  /* Event Type is EV_KEY */
set_bit(BTN_0, vms_input_dev->keybit);  /* Event Code is BTN_0 */
```

Finally, the registration:

```
input_register_device(vms_input_dev);
```

`write_vms()` is the `sysfs store()` method that attaches to `/sys/devices/platform/vms/coordinates`. When `coord.c` writes an X/Y pair to this file, `write_vms()` does the following:

```
input_report_rel(vms_input_dev, REL_X, x);
input_report_rel(vms_input_dev, REL_Y, y);
input_sync(vms_input_dev);
```
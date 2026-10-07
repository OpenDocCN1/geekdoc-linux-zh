# Bootstrap Essentials: Power Management

```
int (*runtime_suspend)(struct device *dev);
int (*runtime_resume)(struct device *dev);
int (*runtime_idle)(struct device *dev);
);
```

The struct dev_pm_ops also includes the device runtime power management callbacks, which you can use at the driver level to manage power.

# Note

The new runtime power management framework was introduced only in 2.6.32 of the kernel.

+   - int (*runtime_suspend)(struct device *dev)
nThe runtime_suspend callback takes the device to a low-power suspended mode that stops communicating with the system. The runtime_suspend can be executed only for active devices.

+   - int (*runtime_resume)(struct device *dev)
The runtime_resume callback resumes the suspended device to a normal state. You can execute the runtime_resume only for suspended devices. Generally, the subsystem runtime callback is responsible for resuming the device appropriately even without the runtime_resume.

+   - int (*runtime_idle)(struct device *dev)
The runtime_idle callback sets devices appearing to be inactive to a low-power suspended mode that stops communicating with the system. When runtime_suspend callback is executed for a device, the runtime_idle callback will not be executed for the same device.

The power management framework also defines wrapper functions to interface with the device power management callback operations. These interface functions are defined in the include/linux/pm_runtime.h header file and exported from drivers/base/power/runtime.c. Some of the key interface functions of power management are listed here.

+   - nt pm_runtime_suspend(struct device *dev)
The pm_runtime_suspend method suspends the device passed on by invoking the runtime_suspend callback. It returns 0 when successful and appropriate error codes such as -EBUSY based on the device state.
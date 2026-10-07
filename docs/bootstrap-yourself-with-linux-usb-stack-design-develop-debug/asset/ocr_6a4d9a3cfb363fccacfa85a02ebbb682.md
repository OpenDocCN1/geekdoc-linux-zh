+   int pm_runtime_resume(struct device *dev)

The pm_runtime_resume method resumes the device passed on by invoking the pm_runtime_resume callback. It returns 0 when successful and appropriate error codes as -EAGAIN based on the device state.

+   int pm_runtime_idle(struct device *dev)

The pm_runtime_idle method notifies to suspend the device by invoking the pm_runtime_idle callback. It returns 0 when successful and appropriate error codes as -EINPROGRESS based on the device state.

+   void pm_runtime_enable(struct device *dev)

When the device starts, the runtime power management is disabled for all devices. The pm_runtime_enable method enables runtime power management for the device by decrementing the disable_depth field of power management info data structure.

+   void pm_runtime_disable(struct device *dev)

The pm_runtime_disable method disables runtime power management for the device and cancels all pending power management operations. Internally, the method increments the disable_depth field of power management info data structure to note the disable call.

+   nt pm_runtime_set_active(struct device *dev)

The pm_runtime_set_active method sets the status of the device and its children to power management active status. This method is unsuccessful when the runtime error and disable depth fields of device info are not 0 or when the device's parent is not active and has set the Ignore Children field. In such a case, the method returns an appropriate error code as -EAGAIN or -EBUSY to indicate the state of the device.

Another important data structure of the power management framework is struct dev_pm_info, which holds key power management framework-related information. The device data structure adds this power management info data structure as a member. One of the most often-used members is the runtime usage_count, which holds information about whether a callback can be executed.
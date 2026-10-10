# **Figure 7.1. The input subsystem.**

![](bbox=[0.0, 0.05, 1.0, 0.75])

Because event drivers are standardized and available for all input classes, you are more likely to implement a device driver than an event driver. Your device driver can use a suitable existing event driver via the input core to interface with user applications. Note that this chapter uses the term *device driver* to refer to an input device driver as opposed to an input event driver.
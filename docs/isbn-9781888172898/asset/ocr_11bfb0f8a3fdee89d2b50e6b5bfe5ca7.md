![](bbox=[0.27, 0.12, 0.85, 0.45])

Figure 8.16: Adding/Editing Routes

The system clock is not changed until you click on the **Set System Clock** button.

Click on **Reset Time** to set the time machine time back to that of the system.

> **Please Note:** Changing the time can seriously confuse programs that depend on the normal progression of time, and could possibly cause problems. Try to quit as many applications and processes as possible before changing the time or date.

# ## 8.6 Kernel Daemon Configuration

As discussed in Chapter 5, Red Hat Linux includes **kerneld**, the Kernel Daemon, which automatically loads some software and hardware support into memory as it is needed, and unloads it when it is no longer being used.

The tool shown in Figure 8.17 manages the configuration file for kerneld. While kerneld can load some things, such as filesystems, without explicit configuration, it needs to be told what hardware support to load when it
![](bbox=[0.14, 0.135, 0.22, 0.22])

n the previous chapters, you have learned how to install and configure Oracle on Linux. This chapter builds on that knowledge and provides information on how to administer the Oracle system on Linux, once the initial configuration steps have been completed and it is running in a production environment. This chapter includes cautions and issues to be aware of when making Linux changes in an Oracle environment, as well as "best practices" for administering your Linux system.

# Configuring the Linux Kernel

As mentioned earlier in this book, and in the previous chapters on configuring and installing the Oracle RAC system on Linux, it is necessary to configure the Linux kernel in order for Oracle to allocate sufficient resources to function properly. Those recommendations in previous chapters provided the standard configuration parameters for the Oracle installation and for general Oracle functionality. However, in the event that your configuration needs to be tuned for a larger SGA or for more semaphores, you might have to tune the Linux parameters as well.

# Configuring Shared Memory

The Linux shared memory parameters need to be large enough to allow Oracle to allocate enough shared memory for the SGA to fit into.

The maximum size of the SGA is dictated by the shared memory parameters that are found in the /proc/sys/kernel/shmall, /proc/sys/kernel/shmmax, and /proc/sys/kernel/shmni files; they are described here:

| Parameter | Value | Description |
| :---- | :---- | :---- |
| shmall | 297152 | Maximum number of shared memory pages system-wide |
| shmmax | 1/2 the size of memory (minimum 1610612736) | Maximum size of a shared memory segment |
| shmni | 4096 | Maximum number of shared memory segments system-wide |

In order to create an SGA up to 2GB in size, we normally set the value of SHMMAX to be 2147483648. In the event that a larger SGA is needed, SHMMAX should be increased.

# Configuring Semaphores and Other Kernel Parameters

When processes connect into the Oracle instance, semaphores are used. As the number of users increases, the number of semaphores might need to be increased
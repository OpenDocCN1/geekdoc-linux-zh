![](bbox=[0.17, 0.12, 0.77, 0.37])

# Linux Initialization

Recall that after a boot loader loads the Linux operating system kernel into memory, the kernel resumes control and executes the first daemon process on the system called init. The init daemon then uses its configuration file /etc/inittab (init table) to load other daemons on the system that provide system services and ultimately allow users to log in and to use the system. Furthermore, the init daemon is responsible for unloading daemons that are loaded in memory when the system is halted or rebooted.

# Runlevels

Because several daemons might need to be managed by the init daemon on a typical Linux system, the init daemon categorizes the system into runlevels. A runlevel defines the number and type of daemons that are loaded into memory and executed by the kernel on a particular system. At any one time, a Linux system might be in any of seven standard runlevels; these runlevels are defined in Table 9-3.

| Runlevel | Common Name | Description |
| :--- | :--- | :--- |
| 0 | Halt | A system that has no daemons active in memory and is ready to be powered off. |
| 1, s, S, single | Single User Mode | A system that has only enough daemons to allow one user to log in and perform system maintenance tasks. A user is automatically logged in to the system as the root user when entering Single User Mode. |
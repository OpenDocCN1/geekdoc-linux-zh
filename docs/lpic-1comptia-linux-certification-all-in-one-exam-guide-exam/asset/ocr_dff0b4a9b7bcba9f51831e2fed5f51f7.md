![](bbox=[0.05, 0.08, 0.77, 0.34])

# ## Managing Systems Without External Peripherals

Depending upon your job role, you may need to manage systems that don't have any external peripherals, even a keyboard. Many servers are managed in this manner, as are many virtualized systems running on a hypervisor.

You have a couple of options for managing these types of systems. If the system has an integrated management interface (such as is found on high-end server systems), you can usually access this interface using a web browser and perform all kinds of manage-ment tasks, including accessing the system display, shutting down the system, and even powering the system on.

If the system doesn't have an integrated management interface, then you have two other options:

+   * **SSH** Using SSH, you can securely access the shell prompt of the system and run commands as if you were sitting in front of the system. You can also tunnel X server traffic through the SSH connection, allowing you to securely access the graphical desktop of the system.
+   * **VNC** You can also use Virtual Network Computing (VNC) to remotely access the graphical desktop of the system. VNC is great, but it lacks the security provided by SSH tunneling, so it is usually used only on secure networks.

We'll discuss configuring SSH in a later chapter. We'll also secure look at configuring xinetd to enable VNC on a Linux system in a later chapter. For now, just understand that these are options you can use to access a system that doesn't have any external peripherals installed.

With this hardware background in mind, let's look next at how Linux drivers work.

# ## Working with Linux Drivers

Back in the *old* days of Linux, working with hardware was hit or miss at best. If you were installing commonly used hardware from a well-known vendor, it would usually work. However, if you were installing specialty hardware or hardware from a less-visible vendor, chances were that the device wouldn't work under Linux.
+   27. **ps:** Process Status
+       - Lists running processes.
+       - Example: `ps aux`

+   28. **kill:** Terminate Process
+       - Sends signals to processes, often used to terminate them.
+       - Example: `kill -9 1234`

These basic Bash commands provide a foundation for navigating and managing a Debian system through the command line interface. Practice and familiarity with these commands will greatly enhance your ability to work efficiently in a Debian environment.

# # System Startup and Shutdown

Understanding the system startup and shutdown processes is crucial for managing a Debian system effectively. Debian uses systemd as its init system, which manages the boot process and system services.

# ## System Startup Process

+   1. **BIOS/UEFI Initialization:**
+   
+      - The computer’s BIOS or UEFI firmware initializes hardware components.
+      - It locates the boot device (e.g., hard drive, SSD) containing the bootloader.

+   2. **Bootloader (GRUB):**
+   
+      - GRUB (Grand Unified Bootloader) loads and presents boot options.
+      - It loads the Linux kernel and initial RAM disk (initrd) into memory.

+   3. **Kernel Initialization:**
+   
+      - The Linux kernel initializes hardware drivers and mounts the root file system.
+      - It starts the init process (systemd in Debian).
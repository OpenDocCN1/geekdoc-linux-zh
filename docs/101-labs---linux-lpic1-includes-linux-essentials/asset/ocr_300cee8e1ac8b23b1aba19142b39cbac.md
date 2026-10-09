# LAB 33

# Install a Boot Manager

**Lab Objective:**

Learn how to install and configure a boot manager.

**Lab Purpose:**

In this lab, you will learn about GRUB and how to configure it.

**Lab Tool:**

Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

**Task 1:**

Classically, to edit GRUB configuration you would make changes to grub.cfg, menu.lst, and other files manually. In Ubuntu 18.04, the configurations are auto-generated based on the contents of /etc/grub.d and /etc/default/grub.

Open the Terminal, and with your favorite editor, edit /etc/default/grub:

+   * Change GRUB_TIMEOUT_STYLE to menu.
+   * Change GRUB_TIMEOUT to 10 or another value you prefer (in seconds).
+   * Change GRUB_CMDLINE_LINUX_DEFAULT to "", or experiment with other values for default kernel boot options.
+   * Change the background by setting GRUB_BACKGROUND to a beautiful image of your choice.
+   * (See Answer 1 below if you're struggling to find a working /etc/default/grub file.)
+   * Finally, close the editor and run sudo update-grub
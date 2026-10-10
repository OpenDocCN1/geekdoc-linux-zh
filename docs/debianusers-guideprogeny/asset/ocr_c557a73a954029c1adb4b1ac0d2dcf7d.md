# Understanding Configuration Methods

Linux includes dozens of configuration tools, from command line utilities that ask you questions to graphical interfaces. However, the most common methods for configuration in Progeny Debian are:

+   - `dpkg-reconfigure` TOOLS: Configures using simple question and answer dialogs. Two useful tools are `ethernet` and `pppconf`.

+   - GNOME Control Center > System: The same tools that you used during the install are available there.

+   - Manually editing the necessary configuration files: This method requires exact knowledge, but allows complex configuration and is always available so long as you have a text editor.

> **Note**
> 
> Hardware connected with the graphical display including the monitor, video card, and pointer can be configured by editing the profiles in the /etc/X11/Xf86Config-4 file. In each section of the file, the first profile is used by default.

+   - Recompile the kernel: This method requires exact knowledge, and can be intimidating to new users. However, it may be necessary, especially if hardware is undetected.

# Understanding the System Settings

Progeny Debian includes the tools used to configure during the install as part of the GNOME Control Center.

+   1. Do one of the following:

+   - From the panel, select the Control Center icon from the panel.
+   - From the menu, select Settings > System.
+   - From the menu, select Programs > Settings > System.
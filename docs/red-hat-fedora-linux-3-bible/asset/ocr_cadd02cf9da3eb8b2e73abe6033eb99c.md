from hand-held devices to PCs to enterprise servers. Chapter 27 contains a more complete description of 2.6 kernel features.

# # ALSA Sound System

The ALSA sound system replaces the OSS sound system used in Fedora Core 1 and previous versions of Red Hat Linux. See Chapter 8 for information on features in the ALSA sound system.

# # Security Enhanced Linux

Security Enhanced Linux (SELinux), added in Fedora Core 2 and enhanced in Fedora Core 3, represents a new model for managing the security of your Linux system. When SELinux is enabled, a set of policies is used to define the permissions that users and processes have to manipulate different components of the operating system.

SELinux is turned on by default, with the *targeted policy* enabled. The targeted policy provides a contained, useful set of rules that are used to protect the system from infiltration through a common set of daemon processes. So, for example, if someone were to infiltrate the computers Web server (httpd daemon), potential damage could be limited to a small set of files and processes on the system. A *strict policy* (which is included by not enabled by default), provides a broader range of SELinux policies that can be useful for someone configuring their own secure system using SELinux.

To work with SELinux, a useful set of graphical tools called setools-gui has been added to Fedora Core 3. Those tools include seauid (an audit log analysis tool) and seusers (a system user manager for managing roles in SELinux). See Chapter 28 for further information on SELinux.

# # System config tools

Red Hat has renamed and continued to enhance its growing arsenal of graphical administrative tools. Since dropping the linuxconf and bypassing the Webmin graphical administrative interfaces, Red Hat has been steadily developing and adding its own administrative tools to its Fedora and Red Hat Linux distributions. As a result, a systems administrator can often skip running shell commands and editing plain-text configuration files to set up servers, manage system resources, or add users.

The following list provides an overview of GUI administration tools and what each is used to configure:

+   - **system-config-bind** — Domain Name System server
+   - **system-config-boot** — Change boot loader settings
+   - **system-config-date** — System time and date
+   - **system-config-display** — Configure the X display, monitor and video card
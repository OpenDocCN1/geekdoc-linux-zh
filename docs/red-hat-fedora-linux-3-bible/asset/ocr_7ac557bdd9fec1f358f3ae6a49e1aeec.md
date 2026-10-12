# Tools in SELinux

Tools available with SELinux let you work with and change policy settings in SELinux. Tools include the following:

+   * **system-config-securitylevel** — Graphical interface for modifying SELinux settings
+   * **selsnf** — Prints policy statistics
+   * **sepcut** — Graphical policy customization tool
+   * **sesearch** — Searches type enforcement rules in SELinux policies
+   * **seuser** — Works with users and roles associated with a policy
+   * **seuseradd** — Adds SELinux features to the useradd tool for adding Linux users
+   * **seusermod** — Adds SELinux features to the usermod tool for modifying Linux user accounts
+   * **seuserdel** — Adds SELinux features to the userdel tool for deleting Linux user accounts
+   * **seaudit** — Graphical audit tool for analyzing log files for SELinux

I recommend that you go through the following procedure for getting started with SELinux. It will help you understand how SELinux works and the tools that are available.

# Using SELinux in Fedora Core 3

If you use the targeted SELinux policy (which is delivered and on by default), you can still administer Linux as you always have. To use the strict SELinux policy, you must change the way you administer your Linux system. If you are new to Linux, turning on the strict policy in SELinux is not a good place to start. Besides being fairly new and somewhat unstable, the extra amount of thought required to learn SELinux makes it most appropriate for environments that must be highly secure.

The following procedure describes the software packages you need to use SELinux and starts you off working with the default targeted policy.

# Getting SELinux

Support for SELinux is built into the Linux 2.6 kernel, as well as a range of supporting operating system features that come with Fedora Core 3. To use SELinux in Fedora Core 3, however, during installation you must enable it.

Enabling SELinux during Fedora Core installation is done on the Firewall Configuration screen. When that screen appears during installation, make sure that Active is selected next to the Enable SELinux box.

With SELinux enabled, you also have to install the following software packages:
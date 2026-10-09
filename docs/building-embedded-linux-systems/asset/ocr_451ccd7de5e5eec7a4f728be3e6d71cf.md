However, as you can see from the original TinyLogin website, http://tinlogin.busybox.net, the project hasn't been updated since 2003. These logging utilities are now actively maintained in BusyBox.

To address the setuid security issues, BusyBox drops its root privileges for applets that don't require root access. It can also be configured to check the /etc/busybox.conf configuration file specifying those privileged applets. For the most paranoid users, the safest solution is still to build two separate BusyBox binaries, one for privileged applets and one for unprivileged applets.

Among the options you can configure, pay special attention to the CONFIG_FEATURE_SHADOWPASSWD, CONFIG_USE_BB_SHADOW, and CONFIG_USE_BB_PWD_GRP configuration options, which are documented in the configuration interface. The most important one is CONFIG_FEATURE_SHADOWPASSWD, which adds support for passwords encrypted in a separate etc/shadow file.

Traditionally, /etc/passwd could be read by anyone in the system, and this in turn became a security risk as more and more programs for cracking passwords were available. Hence, the use of so-called shadow passwords became the norm. When in use, the password fields in /etc/passwd contain only filler characters. The real encrypted passwords are stored in /etc/shadow, which can be read only by a process running with root privileges. Note that if you configure uClibc without shadow password support, enabling CONFIG_FEATURE_SHADOWPASSWD and linking with uClibc will result in a failed build.

You should enable CONFIG_USE_BB_SHADOW to let BusyBox use its own shadow functions for accessing shadow passwords, unless you plan to use glibc's NSS libraries with a properly configured /etc/nsswitch.conf file.

If you enable CONFIG_USE_BB_PWD_GRP, the logging utilities will directly use the /etc/passwd and /etc/group files instead of using the password and group functions provided by glibc. Otherwise, you will also need the C library NSS libraries and a /etc/nsswitch.conf file.

Note that you will not need to create and manage the /etc/group, /etc/passwd, and /etc/shadow files by hand, as the addgroup, adduser, delgroup, and deluser commands take care of creating or updating these files.

For more information on the creation and manipulation of group, password, or shadow password files, as well as system administration in general, see the Linux System Administrator's Guide (O'Reilly, also available from the Linux Documentation Project [LDP]), Running Linux, and the Linux From Scratch book (mentioned earlier in "Complete Standard Applications").

# embutits

embutits is another set of miniaturized and optimized replacements for mainstream Unix commands. Although embutits groups some of the commands in a single binary,
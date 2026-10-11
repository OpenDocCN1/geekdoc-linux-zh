# Objective 2 Create and Manage AppArmor Profiles

SUSE Linux Enterprise Server 10 comes with AppArmor Profiles for various applications, such as named, ntpd, nscd, and others.

The profiles are contained in */etc/apparmor.d/*. The filename of the profile represents the filename of the application including the path, with “/” being replaced by a “:”. The profile for /usr/sbin/squid would be contained in /etc/apparmor.d/usr.sbin.squid.

A profile can include other files with an **#include** statement. The directory */etc/apparmor/abstractions/* contains several files that are intended to be included in profiles, depending on the kind of program to be protected by AppArmor. There are abstractions for files that should be readable or writable by all programs (base), for name service-related files like */etc/passwd* (nameservice), for files related to console operations (console), and others.

The profiles are plain text files and it is therefore possible to create and modify them with any text editor. However, command line tools as well as a YaST module greatly simplify the process of creating profiles.

In addition to the active profiles in */etc/apparmor.d/*, several profiles are already prepared in */etc/apparmor/profiles/extras/* that you can customize to your needs and copy to */etc/apparmor.d/* to activate them.

To successfully administer AppArmor, you need to

+   * Understand Profiles and Rules
+   * Administer AppArmor Profiles with YaST
+   * Administer AppArmor Profiles with Command Line Tools
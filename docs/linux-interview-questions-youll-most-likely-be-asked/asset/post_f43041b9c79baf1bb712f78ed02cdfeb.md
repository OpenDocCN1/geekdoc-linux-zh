
## 34: What command will update all available packages on a Red Hat Linux installation?

- a) yum update
- b) yum -u upgrade
- c) rhn_notify
- d) rpm update

**Answer:** a) yum update

## 35: What is the preferred command to use to install updates, when using the Red Hat Network?

- a) yum
- b) yast
- c) up2date
- d) rhn_notify

**Answer:** c) up2date

## 36: What user does Apache run as, in RHEL/CentOS?

- a) apache
- b) httpd
- c) apache2
- d) www-data

**Answer:** a) apache

# Debian/Ubuntu

## 37: Where is the default configuration file for Apache located?

- a) /etc/httpd/conf/httpd.conf
- b) /etc/apache2/conf/httpd.conf
- c) /etc/httpd.conf
- d) /etc/apache/conf/httpd.conf

**Answer:** b) /etc/apache2/conf/httpd.conf

## 38: What mail server software solution does NOT come with Debian GNU/Linux?

- a) Sendmail
- b) Postfix
- c) Exim
- d) Qmail

**Answer:** d) Qmail

## 39: Which utility will add startup symbolic links to the /etc/rc.d directory?

- a) update-rc.d
- b) chkconfig
- c) init.d
- d) init-rc.d

**Answer:** a) update-rc.d

## 40: What command will install the package 'vim', and all of its dependencies?

- a) dpkg -i vim-version.deb
- b) apt-get install vim
- c) deb install vim-version.deb
- d) yum install vim

**Answer:** b) apt-get install vim

## 41: What command will list all packages installed on a Debian GNU/Linux installation?

- a) `dpkg -l`
- b) `dpkg -v`
- c) `dpkg --show`
- d) `dpkg -s`

**Answer:** a) `dpkg -l`

## 42: What command will remove an individual Debian GNU/Linux package?

- a) `dpkg -e package-version`
- b) `yum remove package`
- c) `apt-get remove package`
- d) `dpkg -r package-version`

**Answer:** a) `dpkg -e package-version`

## 43: What command will upgrade the version of Debian installed?

- a) `apt-get install debian-version`
- b) apt-get dist-upgrade
- c) dpkg -i debian-release-version.deb
- d) apt-get upgrade

**Answer:** b) apt-get dist-upgrade

## 44: What command will update all available packages from Debian's update server?

- a) apt-get install
- b) yum upgrade
- c) apt-get upgrade
- d) apt-get update;apt-get upgrade

**Answer:** d) apt-get update;apt-get upgrade

## 45: If you need a newer version of a package (and still want to use an official Debian package), what distribution version should you look for a newer package in?

- a) testing
- b) stable
- c) newer
- d) unstable

**Answer:** a) testing

## 46: If you need the absolute newest version of a package, than what is provided in Debian stable, what distribution version should you look for the newest package in?

- a) unstable
- b) stable
- c) testing
- d) unreliable

**Answer:** a) unstable

## 47: What user does Apache run as, in RHEL/CentOS?

- a) apache
- b) httpd
- c) apache2
- d) www-data

**Answer:** a) apache

# Various Commands & Utilities

## 48: Which command allows you to view the mail server for an external domain?

- a) dig
- b) mx
- c) lookup
- d) dig-mx

**Answer:** a) dig

## 49: What command will "reverse grep" a string, showing lines that DON'T match a string?

- a) grep "string"
- b) grep -r "string"
- c) grep -c "string"
- d) grep -v "string"

**Answer:** d) grep -v "string"

## 50: Which redirector should be used to append to a file?

- a) '>'
- b) '>>'
- c) '|'
- d) '%'

**Answer:** b) '>>'

## 51: Which character (or command) can be used after a command to send the command into the background (while still executing)?

- a) >/dev/null
- b) &
- c) %
- d) | null

**Answer:** b) &

## 52: What utility allows you to manually test SMTP functionality, troubleshoot firewall restrictions, and connect to other servers?

- a) telnet
- b) ssh
- c) echo
- d) Ping

**Answer:** a) telnet

## 53: Which command switch to the 'ping' utility will allow you to adjust the "TTL, or Time to Live"?

- a) --ttl
- b) -l
- c) -t
- d) -p

**Answer:** c) -t

## 54: What command will allow you to view the routers and hosts that a packet makes it's way through, from the computer you are on, to an outside host?

- a) traceret
- b) traceroute
- c) trace_route
- d) route

**Answer:** b) traceroute

## 55: What command will show listening network connections, as well as active network connections?

- a) connections
- b) conn_list
- c) list
- d) netstat

**Answer:** d) netstat

## 56: What command will allow you to see all processes running on the server?

- a) `ps -a`
- b) `ps -auw`
- c) `ps -waux`
- d) `ps --all-processes`

**Answer:** c) `ps -waux`

## 57: What command will remove an empty directory?

- a) `rm`
- b) `rmdir`
- c) `deltree`
- d) `remove`

**Answer:** b) `rmdir`

## 58: What three commands are typically used to compile software, utilizing the standard 'make' system?

**Answer:** `./configure, make, make install`

## 59: What is the proper syntax to apply a source code patch (called patch.diff) to a source code tree, assuming that the current directory is that of the source code tree?

**Answer:** patch < patch.diff

## 60: When compiling the Linux kernel, what is the command to configure the compilation process, using an ncurses-based menu?

**Answer:** make menuconfig

## 61: What is the proper command to use, to delete all compiled executables, and object files from a source directory (most often used to remove these files to troubleshoot compilation issues)?

**Answer:** make clean

## 62: What is the proper command to use, to remove an installed source package, when the source tree used to compile the software is retained (and the current directory is that of the source tree)?

**Answer:** make uninstall

# General Administration

## 63: What command allows you to change group ownership of a file?

- a) chown groupname filename
- b) chgrp groupname filename
- c) chown groupname:filename
- d) chmod 707 filename

**Answer:** b) chgrp groupname filename

## 64: If you recently created a new user, but they receive an "access denied" error upon logging onto the server, what command did you forget?

- a) chmod 755 /home/username
- b) chown -R username /home/username
- c) passwd username
- d) adduser username

**Answer:** b) chown -R username /home/username

## 65: What file contains the encrypted password of a user?

- a) `/etc/passwd`
- b) `/etc/shadow`
- c) `/etc/users`
- d) `/etc/group`

**Answer:** b) `/etc/shadow`

## 66: What file contains most system errors?

- a) `/var/log/syslog`
- b) `/var/log/errors`
- c) `/var/log/messages`
- d) `/var/messages`

**Answer:** c) `/var/log/messages`

## 67: What command will search for a string, within vi?

- a) `% string`
- b) `/string`
- c) "string
- d) $string

**Answer:** b) /string

## 68: What command will quit vi, without saving the changes to a file?

- a) :q
- b) :wq
- c) :q!
- d) :e!

**Answer:** c) :q!

## 69: What single key will allow you to modify a line of text, within vi?

- a) w
- b) i
- c) q
- d) n

**Answer:** b) i

## 70: What command will write the changes to a file, without quitting vi?

- a) `:wq`
- b) `:w!q`
- c) `:w`
- d) `:g`

**Answer:** c) `:w`

## 71: What file contains the list of preferred DNS servers to use, when looking up the IP address of a domain name?

- a) `/etc/dns`
- b) `/etc/sysconfig/networking`
- c) `/etc/resolv.conf`
- d) `/etc/sysconfig/dns`

**Answer:** c) /etc/resolv.conf

## 72: What file controls text displayed to every user that logs into the server?

- a) /etc/message
- b) /etc/motd
- c) /etc/warning
- d) /etc/bash_profile

**Answer:** b) /etc/motd

## 73: What file contains a user's shell variable settings, and scripts launched at every login (BASH)?

- a) /home/username/.bash_script
- b) /home/username/.bash
- c) /home/username/.bash_profile
- d) /home/username/.bash_history

**Answer:** c) /home/username/.bash_profile

# Summary

In this chapter, we discussed some important system services that come with most
Linux systems. These services can function stand-alone (can work whether or not
the system is in multiuser mode) and as do not rely on network support. Their
implementation can vary slightly from host to host or from distro to distro, but the core
objectives and the problem they aim to solve remain the same.

Here’s a quick recap of the chapter:

+   - init is the master of all processes in the system, with a PID of 1. On pure System
V-based distros, it also controls runlevels and can be configured through the
/etc/initdab

+   - upstart is an alternative program that aims to replace the functionality of init
s some Linux distributions. upstart also offers additional functionality and
improvement.

+   - system is another alternative to init and upstart. It is a system and service
manager for Linux-based operating systems. Several popular distros are
standardizing around it. It offers many benefits and advanced features in
comparison to any of the currently available solutions. It is quickly becoming
semi-mature, opinionated, and idealistic and dreams of solving all the problems
in the world today—including some technical-related ones!

+   - inetd, although barely used, the original super-server that listens
to requests on behalf of a larger number of smaller, less frequently used
services. When it accepts a request for any of those services, inetd starts the
actual service and quickly forwards data between the network and actual
service. Its configuration file is /etc/inetd.conf.

+   - xined is the modern replacement for the classic inetd super-server. It offers
more configuration options and better built-in security. Its configuration
file is /etc/xinetd.conf.

+   - syslog is the system-wide logging daemon used on Fedora, openSUSE,
Ubuntu, and other popular distros. It can act as a drop-in replacement for the
more common and traditional syslog daemon. Some of the advanced features
of rsyslog include writing logs directly to a configured database and allowing
other extensive management of log messages.

+   - systemd-journald (journald) is the newest kid on the block in the world of
system log management. It is fast, nimble, young, and bright with dreams
of solving all the logging problems in the open source world with the aid of its
aptly named command-line utility journalctl.

+   - Finally, the cron service allows you to schedule events to occur at certain dates
 times, which is great for periodic events, such as backups and e-mail
reminders. All the configuration files on which it relies are handled via the
crontab program.
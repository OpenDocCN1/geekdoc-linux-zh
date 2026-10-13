# CERTIFICATION SUMMARY

RHEL 6 includes two VNC servers that can help you configure remote connections to a local GUI desktop environment. They require open ports starting with 5900 and up, depending on the number of remote GUI connections that you want to allow. Such communication can be encrypted over an SSH connection. Be aware, the viewer for the KVM graphical console also uses VNC.

A variety of system administration commands can help you as an administrator to monitor and manage the resources used on a system. These commands include ps, top, kill, nice, and renice. In addition, with the right commands, you can create archives. However, special commands are required to back up files with specialized attributes such as those based on ACLs and SELinux.

The cron and at daemons can help you manage what jobs are run on a system on a schedule. With related configuration files, access to these daemons can be limited to certain users. While cron configuration files follow a specific format documented in /etc/crontab, those configuration directives have been integrated with the anacron system that supports job management on systems that are powered off on a regular basis.

RHEL 6 includes the rsyslog daemon, configured primarily for local systems in the /etc/rsyslog.conf file. Log files are normally collected in the /var/log directory. The rsyslog daemon also supports the creation of a logging server that can collect log file information from a variety of systems.
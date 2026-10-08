# 202 | Layered Security and Linux

# The Power of SELinux

On one level, SELinux is conceptually like a good firewall. All actions are first denied. SELinux contexts are created for users, applications, and services to work normally. These contexts are associated with just the configuration files and program libraries needed by authorized users to make desired actions and services work.

SELinux can be used to assign access and transition rights to every user, process, and file. Interactions between these entities are governed by SELinux policies. If any of these entities do not belong, then neither access transition rights are granted. For example, if the user name apache somehow gets full root administrative access, that user won't be allowed to modify a different service such as an FTP server.

# Basic SELinux Configuration

The simplest way to find the current status of SELinux on the local system is with the sestatus command. It confirms the configuration shown in the /etc/sysconfig/selinux file. If you want to find the current SELinux status of files in the local directory, try the ls -Z command. As an example, look at the SELinux characteristics of the default FTP server directory:

```
$ ls -Z /var/ftp/
drw-xr-xr root system_u:object_r:public_content_t pub
```

The output shows SELinux characteristics of the pub/ subdirectory in /var/ftp/ directory. If you'd configure a different directory for the FTP server, SELinux contexts must be associated with the system user (system_u), system objects (object_r), and a directory type associated with public information (public_content_t).

One way to change another directory is by running some chcon commands. Specifically, you would want to change the SELinux context associated with that user, system, and directory. For example, to change the user and contexts on a /srv/ftp/ directory, you'd run the following:

```
# chcon -system_u -t public_content_t /srv/ftp/
```

A number of other commands can help you configure SELinux from the command-line interface. As you customize SELinux for your systems, there will be many cases where you modify SELinux policies to enable normal operation of regular services on the target system.

# Configuration from the Command Line

On Red Hat systems, most of the important command-line tools are part of the policycoreutils. sesetools, and libselinux-utils packages. That package includes a couple of configuration files: sestatus.conf and selinux/restore.conf in the /etc/ directory. These files include list of critical files and services to be watched for changes. You might want to add more files and services to these lists. The commands from the aforementioned packages are described briefly in Table 7-2.
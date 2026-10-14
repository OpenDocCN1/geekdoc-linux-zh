
```text
eric       pts/1    192.168.1.100   Sat Feb 26 09:55 - 09:55  (00:00)
belandja   pts/4    192.168.1.100   Sat Feb 26 09:54 - down     (14:02)
hart       pts/1    192.168.1.100   Sat Feb 26 09:53 - 09:54  (00:01)
root       pts/3    :0.0             Sat Feb 26 09:46 - down     (14:11)
belandja   pts/2    192.168.1.100   Sat Feb 26 09:12 - 10:14  (01:01)
hart       pts/1    192.168.1.100   Sat Feb 26 08:44 - 09:53  (01:08)
root       pts/0    0                Sat Feb 26 08:44 - down     (15:12)

wtmp begins Mon Feb 14 19:00:40 2005
```

You can use a separate command to quickly extract the last login times of certain accounts. This can be a quick way to check for unused accounts or accounts that are being used but shouldn't be. Here's an example of the lastlog command:

```text
Athena:~ # lastlog
Username         Port     From               Latest
root             pts/2    athena.universal   Sun Feb 27 12:30:43 -0500 2005
bin                       **Never logged in**
daemon                    **Never logged in**
lp                        **Never logged in**
games                     **Never logged in**
man                       **Never logged in**
.                         **Never logged in**
.                         **Never logged in**
ldap                      **Never logged in**
dhcpd                     **Never logged in**
belandja  1      192.168.1.100   Sun Feb 27 12:29:40 -0500 2005
eric      2      192.168.1.100   Sun Feb 27 12:23:43 -0500 2005
hart      1      192.168.1.100   Sat Feb 26 10:08:46 -0500 2005
peter                     **Never logged in**
pol       pts/3  192.168.1.240   Sun Feb 27 14:25:20 -0500 2005
mark      pts/4  hermes.universal Sun Feb 27 14:31:03 -0500 2005
ted       tty5                   Sun Feb 27 14:29:25 -0500 2005
```

This command provides a listing of all the accounts on the system as well as the times they were last logged in to the system and the source of the login. Because of the large number of system accounts, the list can grow quite large. You might be tempted to parse the output of this command using grep to remove all accounts that have never been used:

```text
Athena:~ # lastlog | grep -v -e "**Never"

Username   Port      From              Latest
root       pts/2     athena.universal  Sun Feb 27 12:30:43 -0500 2005
belandja   1         192.168.1.100     Sun Feb 27 12:29:40 -0500 2005
eric       2         192.168.1.100     Sun Feb 27 12:23:43 -0500 2005
hart     1        192.168.1.100   Sat Feb 26 10:08:46 -0500 2005
pol      pts/3    192.168.1.240   Sun Feb 27 14:25:20 -0500 2005
mark     pts/4    hermes.universal Sun Feb 27 14:31:03 -0500 2005
ted      tty5                      Sun Feb 27 14:29:25 -0500 2005
```

Parsing the output this way is an acceptable practice if you are looking for individual accounts that you know have been active. The raw lastlog command does, however, provide additional information about the system process accounts. Verifying that they have not been used for an interactive login could prove quite useful.

Knowing that a specific account was used in an inappropriate manner is one thing. Being able to identify the individual who used the account is much more difficult. Verifying the number of login failures for an account is an important step. Excessive login failures might be an indication of a password hack attack—possibly a successful one. The faillog command allows you to check the number of times a login attempt was unsuccessful against each account:

```text
Athena:~ # faillog
Username   Failures  Maximum  Latest
root       3         0        Wed Feb 16 03:49:05 -0500 2005 on 0
belandja   0         0        Mon Feb 14 19:02:11 -0500 2005 on 1
eric       0         0        Tue Feb 15 18:06:28 -0500 2005 on 2
hart       0         0        Tue Feb 15 06:57:10 -0500 2005 on 4
```

An indication of a large number of login failures on an account might indicate that the password on the account was hacked. It may also be a ruse. Having a sound account password policy and including the PAM module pam_tally to lock out accounts after a set number of failed attempts are important steps you can take. This way, you can mitigate some of the exposure to password-harvesting attacks. This also helps you in ensuring that the person who last logged in to a specific account knew the password.

In this section, you saw numerous methods for extracting user login information. You can use this information to help investigate resource issues. This information can also be used as a starting point in investigating suspect behavior on the system.

## System Tuning

The initial performance of a server is based on a number of parameters set by the supplier of the operating system. In the case of SLES, these parameters are chosen to satisfy a broad range of server types. Each service can require different resources. Some services are memory or bandwidth intensive, whereas

others are CPU intensive. These various factors are balanced by default to provide a responsive server regardless of its initial tasking.

What cannot be anticipated, however, are the resources available from the hardware supplied. SUSE specifies a number of minimum requirements to provide a stable environment. In most cases, meeting these minimum requirements is not an issue. As resource limits start contributing to performance issues, memory or disk space can be added to a server.

In some situations, however, the tasking of a server is outside the designed norm. In these cases, you must entertain changes to the fundamental assumptions in the original configuration.

In Linux- and Unix-based systems, the core program of the operating system is called the kernel. The kernel is built just like any other program. It incorporates within its structure the original assumptions of the configuration team. These assumptions govern which device types are available such as IDE or SCSI disks, how memory will be managed, and if additional modules can be loaded dynamically. Adding and removing capabilities within the configuration of the kernel can increase flexibility and performance.

When such situations arise, you often need to alter the actual Linux kernel itself. This can be done in a couple of different ways. One option is to recompile the kernel to include additional functionality. The preferred method, when available, is to take advantage of the flexibility of the default kernel and simply tune some of its runtime parameters.

### Tuning Kernel Parameters

A number of applications have been ported to Linux. Some of them, such as database applications, have resource requirements that are significantly different from those of typical Linux services. To satisfy these needs, you must make changes to the way the kernel operates by tuning application-specific parameters.

In older versions of Unix, these changes required a rebuild of the kernel itself. Though not an insurmountable feat, rebuilding the kernel is certainly a daunting task for someone who has never done it. Luckily, the Linux kernel is flexible and dynamic. Changes to the Linux kernel can be made in real-time without requiring a reboot.

As an example, let's look at the changes required to the Linux kernel for it to be able to run Oracle 10g. These changes are supplied in a script run at install time; for arguments' sake, say you want to make these changes manually. The Oracle 10g requirements are shown in Table 7.3.

### TABLE 7.3

Oracle 10g SUSE LINUX Kernel Requirements

| KERNEL PARAMETER | MINIMUM VALUE REQUIRED (UNITS DEPEND ON PARAMETER) | DESCRIPTION |
|---|---|---|
| `kernel.shmall` | `2097152` | Available memory for shared memory in 4KB blocks |
| `kernel.shmmax` | `2147483648` | Maximum size of a shared memory segment |
| `kernel.shmni` | `4096` | Maximum number of shared segments |
| `kernel.sem` | `250 32000 100 128` | Semaphores |
| `fs.file-max` | `65536` | Maximum number of file handles allocated by the kernel |
| `net.ipv4.ip_local_port_range` | `1024 65000` | Required available ports |

### NOTE

Tuning the kernel is a task that should only be undertaken with great care. Changes made could generate an environment that is unable to function. There are a number of sites on the Internet that discuss the Linux kernel, and its parameters. Visit one of these for more information:

- http://www.suse.de/~agruen/kernel-doc/
- http://www.kernelnewbies.org/
- http://www.bb-zone.com/SLGFG/chapter4.html

You can use the sysctl command to query the values currently in use by the running kernel. Specifying the -a switch lists all the parameters. Each individual parameter can be checked using syntax similar to the following:

```text
Athena:~ # sysctl kernel.shmmax
kernel.shmmax = 33554432
```

As you can see, this parameter value is well below the minimum required for Oracle. To set the value, use the following syntax:

```text
Athena:~ # sysctl -w kernel.shmmax=2147483648
kernel.shmmax = 2147483648
```

This syntax sets the new value for the kernel parameter and acknowledges the new value.

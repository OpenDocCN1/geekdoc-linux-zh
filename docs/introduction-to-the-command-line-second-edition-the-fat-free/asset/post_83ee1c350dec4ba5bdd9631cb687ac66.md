
## runlevel

Purpose: Display the previous and current runlevel.

Usage syntax: `runlevel`

```
$ `runlevel`
3 1
```

Output of the runlevel command

The `runlevel` command displays the current and previous runlevel. The runlevel is an initialization sequence called by the `init` process and defines procedures for system startup and shutdown. In the above example, `runlevel` is used to display the current runlevel information. The first number displayed is the previous runlevel and the second number is the current runlevel.

> Note
> If there is no previous runlevel, the system will display N in the first field.

Common usage examples:

- `runlevel`: Display the previous and current runlevel

## service

**Purpose:** Manage services on a Linux system.

**Usage syntax:** `service [OPTIONS] [SERVICE] [ACTION]`

![](img/fa2f95b64a707c963dfa0445bd9281a7_129_0.png)

The `service` command manages services on Linux systems. In the above example, the `--status-all` option displays the status of all services on the system. The `+` symbol indicates a running service and the `-` symbol indicates a stopped service.

The `start`, `stop`, `restart`, and `status` options can be used to control individual services as demonstrated in the next example.

![](img/fa2f95b64a707c963dfa0445bd9281a7_129_1.png)

Common usage examples:

| Command | Description |
| :--- | :--- |
| `service [SERVICE] stop` | Stop the specified service |
| `service [SERVICE] start` | Start the specified service |
| `service [SERVICE] restart` | Restart the specified service |
| `service [SERVICE] status` | Display the status of the specified service |
| `service --status-all` | Display the status of all services |

## sysv-rc-conf

**Purpose: Display and edit Linux runlevel configuration.**

**Usage syntax:** `sysv-rc-conf [OPTIONS] [SERVICE] [ON|OFF]`

```
# sysv-rc-conf
SysV Runlevel Config -- stop service w/+: start service h: help q: quit

 Service  1  2  3  4  5  0  6  S
acpid   [ ]  [X] [X] [X] [X] [X] [ ]  [ ]  [ ]
anacron [ ]  [X] [X] [X] [X] [ ]  [ ]  [ ]
apache  [ ]  [X] [X] [X] [X] [X] [ ]  [ ]  [ ]
apparmor[ ]  [ ] [ ] [ ] [ ] [ ]  [ ]  [X]
apport  [ ]  [X] [X] [X] [X] [ ]  [ ]  [ ]
atd     [ ]  [X] [X] [X] [X] [ ]  [ ]  [ ]
bind9   [ ]  [X] [X] [X] [X] [ ]  [ ]  [ ]

Use the arrow keys or mouse to move around. ^n: next pg ^p: prev pg
Space: toggle service on / off
```

Example output of the `sysv-rc-conf` command

The `sysv-rc-conf` command manages `service/runlevel` configuration on Linux systems. In the above example, executing `sysv-rc-conf` starts a configuration utility which enables the user to select which services start on the various runlevels.

Services can also be displayed and modified via the command line using the `--list` and `--level` options as demonstrated in the next example.

```
# sysv-rc-conf --level 2345 apache off
# sysv-rc-conf --list apache2
apache2    2:off  3:off  4:off  5:off
# sysv-rc-conf --level 2345 apache2 on
# sysv-rc-conf --list apache2
apache2    2:on   3:on   4:on   5:on
```

Using the `sysv-rc-conf` command to manage services on the command line

**Common usage examples:**

- `sysv-rc-conf`: Display the runlevel configuration utility
- `sysv-rc-conf --list`: List runlevel configuration for all services
- `sysv-rc-conf --level [LEVEL] [SERVICE] on`: Enable a service on the specified level(s)
- `sysv-rc-conf --level [LEVEL] [SERVICE] off`: Disable a service on the specified level(s)

## chkconfig

Purpose: Display and edit runlevel configuration on Red Hat Linux-based systems.

Usage syntax: `chkconfig [OPTIONS] [SERVICE] [ON|OFF] [LEVEL]`

```
# chkconfig -1
```

| Service | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| acpi-support | off | off | on | on | on | on | off |
| acpid | off | off | on | on | on | on | off |
| alsa-utils | off | off | off | off | off | off | off |
| anacron | off | off | on | on | on | on | off |
| apache2 | off | off | off | off | off | off | off |
| apport | off | off | on | on | on | on | off |
| ... | | | | | | | |

Listing service configuration with the chkconfig command

The `chkconfig` command manages services on Red Hat Linux systems. The `-1` parameter lists the current runlevel configuration, as shown in the above example. If no service is specified, all services will be displayed. Specifying a service name will display the runlevel configuration for the service, as shown in the next example.

```
# chkconfig -1 apache2
```

| Service | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| apache2 | off | off | on | on | on | on | off |

Listing a specific service with the chkconfig command

The `-s` option is used to enable or disable services at the specified run levels as demonstrated in the next example.

```
# chkconfig -s apache2 off 2345
# chkconfig -1 apache2
```

| Service | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| apache2 | off | off | off | off | off | off | off |

```
# chkconfig -s apache2 on 2345
# chkconfig -1 apache2
```

| Service | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| apache2 | off | off | on | on | on | on | off |

Managing services with the chkconfig command

Common usage examples:

- `chkconfig -1`: List runlevel configuration for all services
- `chkconfig -1 [SERVICE]`: List a service's current configuration
- `chkconfig -s [SERVICE] on [LEVEL]`: Enable a service on the specified level(s)
- `chkconfig -s [SERVICE] off [LEVEL]`: Disable a service on the specified level(s)

## rc-status

Purpose: Display the status of services on Gentoo Linux systems.

Usage syntax: `rc-status [OPTIONS]`

```
# rc-status
Runlevel: default
amavisd
                [ started ]
apache2
                [ started ]
clamd
                [ started ]
courier-authlib
                [ started ]
courier-imapd
                [ started ]
courier-imapd-ssl
                [ started ]
courier-pop3d
                [ started ]
hostname
                [ started ]
keymaps
                [ started ]
...
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_132_0.png)

The rc-status displays the status of services on Gentoo Linux systems. In the above example, all services for the current level are listed along with their current status.

> Note: Gentoo Linux uses a nontraditional init structure that differs from most Linux systems. You can read more about Gentoo's init system online at www.gentoo.org/doc/en/handbook/.

Common usage examples:

- `rc-status`: List services for the current runlevel
- `rc-status -a`: List all services
- `rc-status -l`: List all defined run levels

## rc-update

**Purpose**: Display and edit runlevel configuration on Gentoo Linux systems.

**Usage syntax**: `rc-update [OPTIONS] [SERVICE] [LEVEL]`

![](img/fa2f95b64a707c963dfa0445bd9281a7_133_0.png)

The `rc-update` command manages services on Gentoo Linux-based systems. In the above example, the `show` option is used to display the current runlevel configuration.

The `add` and `del` options are used to add and delete services from the specified runlevel, as shown in the next example.

![](img/fa2f95b64a707c963dfa0445bd9281a7_133_1.png)

**Common usage examples:**

| Command | Description |
| :--- | :--- |
| `rc-update show` | List runlevel configuration for all services |
| `rc-update add [SERVICE] default` | Add the specified service to the default runlevels |
| `rc-update del [SERVICE] default` | Remove the specified service from the default runlevels |

## lssrc

Purpose: Display the status of services on AIX systems.

Usage syntax: `lssrc [OPTIONS] [SERVICE/GROUP]`

```
# lssrc -a
Subsystem    Group      PID      Status
syslog       ras        147590   active
sendmail     mail       188508   active
portmap      portmap    126930   active
snmpd/bd     tcpip      151728   active
inetd        tcpip      163958   active
snmpd        tcpip      180316   active
hostmibd     tcpip      159852   active
aixmibd      tcpip      168024   active
bi\od        nfs        196706   active
rpc.statd    nfs        209038   active
rpc.lockd    nfs        204984   active
qdaemon      spooler    217200   active
writesrv     spooler    233588   active
ctmco        ract       241870   active
pconsole     pconsole   270470   active
cmags        229504     active
IBM.ServiceRM  ract_rm  311470   active
IBM.C$MAGentRM ract_rm  291004   active
lpid         spooler    inoperative
...
```

Listing the status of all services

The `lssrc` command displays the status of services on AIX systems. The above example demonstrates using the `-a` option to display the status of all services. The next example demonstrates using the `-s` option to list a specific service.

```
# lssrc -s nfsd
Subsystem    Group      PID      Status
nfsd         nfs        inoperative
```

Listing a specific service

Common usage examples:

| Command | Description |
| :--- | :--- |
| `lssrc -a` | Display the status of all services |
| `lssrc -s [SERVICE]` | Display the status of the specified services |
| `lssrc -g [GROUP]` | Display the status of the specified group of services |

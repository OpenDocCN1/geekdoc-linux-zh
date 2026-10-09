
The *program* is usually a shell, but it can be any program. The following line in the `passwd` file creates a "user" whose only purpose is to execute the `who` utility:

```
who:x:1000:1000::execute who:/usr:/usr/bin/who
```

Logging in with `who` as a username causes the system to log you in, execute the `who` utility, and log you out. The output of `who` flashes by quickly because the new login prompt clears the screen immediately after `who` finishes running. This entry in the `passwd` file does not provide a shell, so you cannot stay logged in after `who` finishes executing.

This technique is useful for providing special accounts that may do only one thing. The `ftp` account, for example, enables anonymous FTP (page 687) access to an FTP server. Because no one logs in on this account, the shell is set to `/bin/false` (which returns a false exit status) or to `/usr/sbin/nologin` (which does not permit a nonprivileged user to log in). When you put a message in `/etc/nologin`, `nologin` displays that message (except it has the same problem as the output of `who`: It is removed so quickly that it is hard to see).

## Do not replace a login shell with a shell script

Do not use shell scripts as replacements for shells in `/etc/passwd`. A user may be able to interrupt a shell script, giving him full shell access when you did not intend to do so. When installing a dummy shell, use a compiled program, not a shell script.

### /etc/printcap
The printer capability database for LPD/LPR (page 548). It is not used with CUPS (Chapter 14), Ubuntu’s default printing system. This file describes system printers and is derived from 4.3BSD UNIX.

### /etc/profile
Contains a systemwide interactive shell initialization script for environment and startup programs. When you log in, the shell immediately executes the commands in this file in the same environment as the shell. (For information on executing a shell script in this manner, refer to the discussion of the `. [dot]` command on page 296.) This file allows the system administrator to establish systemwide environment parameters that individual users can override in their `~/.bash_profile` (page 488) files. For example, this file can set shell variables, execute utilities, set up aliases, and take care of other housekeeping tasks.

The default Ubuntu `/etc/profile` file sets the shell prompt and executes the commands in `/etc/bash.bashrc` (page 492).

Following is an example of a `/etc/profile` file that displays the message of the day (the `/etc/motd` file), sets the file-creation mask (umask, page 459), and sets the interrupt character to CONTROL-C:

```bash
# cat /etc/profile
cat /etc/motd
umask 022
stty intr '^C'
```

### /etc/protocols
Provides protocol numbers, aliases, and brief definitions for DARPA Internet TCP/IP protocols. Do not modify this file.

### /etc/init
Holds Upstart job definition files. See page 438 for more information.

### /etc/init.d
Holds SysVinit initialization scripts. See page 440 for more information.

### /etc/resolv.conf
The resolver (page 824) configuration file, which is used to provide access to DNS. By default, this file is rebuilt by `resolvconf` when you run the `bind9` init script. See “named options” on page 834, “`namesconf` and `resolv.conf`” on page 835, and the `resolver` and `resolv.conf` man pages for more information.

The following example shows the `resolv.conf` file for the `example.com` domain. A `resolv.conf` file usually contains at least two lines—a search line (optional) and a nameserver line:

```
# cat /etc/resolv.conf
search example.com
nameserver 10.0.0.50
nameserver 10.0.0.51
```

The **search** keyword may be followed by a maximum of six domain names. The first domain is interpreted as the host's local domain. These names are appended one at a time to all DNS queries, shortening the time needed to query local hosts. The domains are searched in order in the process of resolving hostnames that are not fully qualified. See *FQDN* on page 1149.

When you put **search example.com** in `resolv.conf`, any reference to a host within the **example.com** domain or a subdomain (such as **marketing.example.com**) can use the abbreviated form of the host. For example, instead of issuing the command **ping speedy.marketing.example.com**, you can use **ping speedy.marketing**. The following line in `resolv.conf` causes the **marketing** subdomain to be searched first, followed by **sales**, and finally the entire **example.com** domain:

```
search marketing.example.com sales.example.com example.com
```

It is a good idea to put the most frequently used domain names first to try to outguess possible conflicts. If both **speedy.marketing.example.com** and **speedy.example.com** exist, for example, the order of the search determines which one is selected when you invoke DNS. Do not overuse this feature: The longer the search list, the more network DNS requests generated, and the slower the response. Three or four names are typically sufficient.

The **nameserver** line(s) indicate which systems the local system should query to resolve hostnames to IP addresses, and vice versa. These machines are consulted in the order they appear, with a timeout between queries. The first timeout is a few seconds; each subsequent timeout is twice as long as the previous one. The preceding file causes this system to query 10.0.0.50, followed by 10.0.0.51 when the first system does not answer within a few seconds. The `resolv.conf` file may be automatically updated when a PPP- (Point-to-Point Protocol) or DHCP- (Dynamic Host Configuration Protocol) controlled interface is activated. Refer to the `resolv.conf` and `resolver` man pages for more information.

### /etc/rpc
Maps RPC services to RPC numbers. The three columns in this file show the name of the server for the RPC program, the RPC program number, and any aliases.

## IMPORTANT FILES AND DIRECTORIES 497

### /etc/services
Lists system services. The three columns in this file show the informal name of the service, the port number/protocol the service uses most frequently, and any aliases for the service. This file does not specify which services are running on the local system, nor does it map services to port numbers. The services file is used internally to map port numbers to services for display purposes.

### /etc/shadow
Contains MD5 (page 1159) hashed user passwords. Each entry occupies one line composed of nine fields, separated by colons:

```
login-name:password:last-mod:min:max:warn:inactive:expire:flag
```

The login-name is the user’s username — the name that the user enters in response to the login: prompt or on a GUI login screen. The password is a hashed password that passwd puts in this file. New accounts that are not set up with a password are given a value of 1 or * in this field to prevent the user from logging in until you assign a password to that user (page 595).

The last-mod field indicates when the password was last modified. The min is the minimum number of days that must elapse before the password can be changed; the max is the maximum number of days before the password must be changed. The warn field specifies how much advance warning (in days) will be given to the user before the password expires. The account will be closed if the number of days between login sessions exceeds the number of days specified in the inactive field. The account will also be closed as of the date in the expire field. The last field in an entry, flag, is reserved for future use. You can use usermod (page 598) to modify these fields.

The shadow password file must be owned by root and must not be publicly readable or writable. Setting ownership and permissions in this way makes it more difficult for someone to break into the system by identifying accounts without passwords or by using specialized programs that try to match hashed passwords.

A number of conventions exist for creating special shadow entries. An entry of *LK* or NP in the password field indicates locked or no password, respectively. No password is different from an empty password; no password implies that this is an administrative account that no one ever logs in directly. Occasionally programs will run with the privileges of this account for system maintenance functions. These accounts are set up under the principle of least privilege (page 420).

Entries in the shadow file must appear in the same order as in the passwd file. There must be exactly one shadow entry for each passwd entry.

### /etc/hosts.deny, /etc/hosts.allow
As part of the client/server model, TCP wrappers rely on these files as the basis of a simple access control language. See page 465 for more information.

### /proc
Provides a window into the Linux kernel. Through the /proc pseudo filesystem you can obtain information on any process running on the system, including its current

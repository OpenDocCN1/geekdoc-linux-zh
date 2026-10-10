
A PAM configuration for a specific service includes four stacks, which are sets of PAM modules that are called in a specific order to perform particular subtasks associated with authentication. Listing 12.1 shows four stacks, as identified by the management group keywords in the first column of the noncomment lines: **auth**, **account**, **password**, and **session**. Each management group defines how PAM controls particular authentication tasks: **auth** verifies passwords, **account** manages nonpassword access rules, **password** handles password maintenance, and **session** handles bookkeeping when users log in or out.

The second column in a PAM configuration file specifies how success or failure of each module is to affect the authentication task. For instance, **required** indicates that the module must succeed in its task, whereas **optional** means that the task can succeed or fail with no particular repercussions. The **include** keyword means that another file in /etc/pam.d is loaded at this point in the stack. (Some distributions use a directive called `@include` in the first column rather than an **include** directive in the second column for this purpose.) Including other files provides a way to easily modify the configuration of several authentication services: you can modify only the included file rather than the files for every tool on the system.

The final column in a PAM configuration file is the name of the module, sometimes with associated options. This is where configuring PAM gets tricky: lots of modules are available, and some add-on packages ship with their own tools. For instance, Samba ships with the Winbind tool for authenticating users against a Windows network account database, and Winbind consists, in part, of a PAM module that you add to an account stack.

Wholesale changes to PAM configuration frequently involve the general-purpose authentication stack—the one that's referred to by any **include** directives in other files, such as **system-auth** in Listing 12.1. You can add or change a module to affect most of the relevant authentication tools.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_561_0.png)

> Changing your PAM configuration is risky. If you get something wrong, you can end up unable to log into the computer. If this happens, you may need to use an emergency boot disk to restore your original files. **Always** make backups of any files you change in /etc/pam.d so you can do this. You should also leave a text-mode root console login running when you make your changes. That way, if you test your changes and find they block all access, you'll be able to revert to your original configuration without booting your emergency disk.

Unfortunately, changing PAM stacks is potentially tricky. Every distribution does things slightly differently, so a change that works well on one distribution may not work at all on another. As a general rule, if you want to add a new authentication tool, you must add a line with the new module to the **auth** and **account** stacks. This line is typically typed **sufficient** and appears immediately before or after the **pam_unix.so** module. In some cases you may need to alter the **pam_unix.so** line or make other changes.

When using network or other unusual authentication methods, you'll still need to create home directories for these users. If you want this to be done automatically, try adding the following line to the end of the **session** stack:

```
session required pam_mkhomedir.so skel=/etc/skel umask=0022
```

This PAM module creates a home directory for users who don’t already have one. This option can be very handy when authenticating against Winbind, NIS, LDAP, or other network servers that maintain account databases but that don’t create home directories on the Linux systems that use the authentication server.

## Using Network Authentication

One means of extending Linux authentication is to enable a network server to hold Linux account information. Chapter 10, “Configuring Network Servers I,” and the preceding section, “Configuring PAM,” mentioned Winbind, which enables you to take advantage of a Windows domain server to provide you with account information. A couple more approaches are the *Network Information Service* (NIS) and the *Remote Authentication Dial In User Service* (RADIUS) tools.

### Using NIS

NIS is a protocol that’s designed to simplify user authentication and related services on a network of multiple Unix or Linux systems. There are several variants of NIS, such as NIS+ and NIS YP and Switch (NYS). The original NIS was once called Yellow Pages (YP), but that’s a registered trademark in some areas, so the name was changed. Nonetheless, most NIS utilities and configuration files still include yp in their names.

Some distributions let you configure NIS during system installation. You may be required to enter the NIS domain name (which may be different from your DNS domain name) and the address of the NIS server. If you want to use NIS after installing the OS, your task is a bit trickier. Your distribution might provide GUI tools to help the process, or you might need to configure the system manually. You should begin by installing the NIS packages. For an NIS client, the *ypbind* package is the most important one, but on most distributions it depends on other packages, such as *yp-tools*.

![](img/a78bc63f22351f522ba5ec1fa0c060d2_562_0.png)

NIS uses both clients and servers. The NIS server holds network account information, and the NIS clients use that information to authenticate users. This section describes the basics of NIS client configuration and the use of certain tools for NIS account maintenance. To learn about NIS server configuration, consult its documentation or a book on the subject, such as *Hal Stern, Mike Eisler, and Ricardo Labiaga’s Managing NFS and NIS, Second Edition* (O’Reilly, 2001).

The *ypbind* NIS package’s main configuration file is */etc/yp.conf*. This file’s primary purpose is to point the NIS tools at an NIS server. The default file normally presents several possible ways to do this in comments. These methods differ in the amount of information you as an administrator have. For instance, if you know the name of your NIS domain and the name of the NIS server, you might use this format:

```
domain NISDOMAIN server NISSERVER
```

At the opposite extreme is a line that contains a single word: **broadcast**. This tells the tools to send out a broadcast query for a suitable NIS server. You should consult your network administrator to learn what option is best for your network.

Once you’ve told the NIS tools about your server, you must also configure Linux to use NIS. This can be accomplished by editing the **/etc/nsswitch.conf** file, which tells Linux what tools to use for name resolution, account information, and so on. A configuration that relies heavily on NIS is shown in Listing 12.2. If you want to use NIS only for user authentication, you can simply change the **passwd**, **group**, and **shadow** lines to add **nis** to the existing options.

**Listing 12.2:** Sample **/etc/nsswitch.conf** File for NIS

```
passwd: compat
group: compat
# For libc5, you must use shadow: files nis
shadow: compat

passwd_compat: nis
group_compat: nis
shadow_compat: nis

hosts: nis files dns

services: nis [NOTFOUND=return] files
networks: nis [NOTFOUND=return] files
protocols: nis [NOTFOUND=return] files
rpc: nis [NOTFOUND=return] files
ethers: nis [NOTFOUND=return] files
netmasks: nis [NOTFOUND=return] files
netgroup: nis
bootparams: nis [NOTFOUND=return] files
publickey: nis [NOTFOUND=return] files
automount: files
aliases: nis [NOTFOUND=return] files
```

Once this is set up, you should start or restart the **ypbind** daemon, which must be running at all times on the NIS client. Client-side tools contact this daemon for information that’s normally stored in **/etc/passwd** and elsewhere; the **ypbind** daemon contacts the NIS server, and the NIS server delivers the requested information. Normally, you start **ypbind** via its SysV startup script.

Once NIS is up and running, you can manage the system with an assortment of commands whose names begin with **yp**. For instance, **yppasswd** changes a password much as **passwd** does, but **yppasswd** changes the password on the NIS server. On the server system, **ypinit** initializes the user account database.

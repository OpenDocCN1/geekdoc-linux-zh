# Listing 23-8  (continued)

```
-10:CAP_NET_BIND_SERVICE
+11:CAP_NET_BROADCAST
-12:CAP_NET_ADMIN
-13:CAP_NET_RAW
+14:CAP_IPC_LOCK
+15:CAP_IPC_OWNER
-16:CAP_SYS_MODULE
-17:CAP_SYS_RAWIO
-18:CAP_SYS_CHROOT
+19:CAP_SYS_PTRACE
+20:CAP_SYS_PACCT
-21:CAP_SYS_ADMIN
+22:CAP_SYS_BOOT
+23:CAP_SYS_NICE
+24:CAP_SYS_RESOURCE
+25:CAP_SYS_TIME
+26:CAP_SYS_TTY_CONFIG
+27:CAP_MKNOD
+28:CAP_LEASE
+29:CAP_HIDDEN
+30:CAP_INIT_KILL
```

The + sign enables the capability and the - sign disables it. For example, in the above listing, the last Linux Capability called `CAP_INIT_KILL` is enabled, which means that a root-owned process could kill any child process (typically daemons) created by the `init` process. You use a text editor to enable or disable the Linux Capabilities.

# Protecting your system by using LIDS-managed Linux Capabilities

You can use LIDS-provided capabilities to protect your system. In this section, I show you how to take advantage of the Linux Capabilities managed by LIDS. You will see how you can protect daemons (such as Apache Web server) from being killed by the root user, how to hide processes from programs like `ps`, how to disable raw access to devices, and how to protect the ext2 immutable flag.

# Protecting daemons from being killed by root

Typically, daemon processes, such as the Sendmail mail transport agent and Apache Web server, are started by the `init` process. If you wish to protect them from being killed by the root user, modify the `CAP_INIT_KILL` settings in `/etc/lids/lids.cap` to be:

```
-30:CAP_INIT_KILL
```
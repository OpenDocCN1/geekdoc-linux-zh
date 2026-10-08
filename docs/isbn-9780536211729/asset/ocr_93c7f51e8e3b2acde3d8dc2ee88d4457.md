command lilo to store these instructions in the Master Boot Record (MBR). Although a reboot is not strictly necessary, you certainly will want one to verify that the changes worked.

The most flexible method is to require that password be entered if boot options are passed to the boot loader. This is particularly useful because it prevents unauthorized personnel from booting into single-user mode while allowing anyone to boot multiuser mode, say, after a crash. Add the following two lines. Either may be either global or per-image.

```
restricted
password=secret
```

Be sure that the configuration file can be read only by root

```
chmod 600 /etc/lilo.conf
chown root /etc/lilo.conf
```

Another way to guard against single-user mode is to not allow anyone to issue any commands to LILO at the keyboard by setting a timeout of zero in global commands section at the top of /etc/lilo.conf. (This is a requirement for Orange Boot C2 security).

```
timeout=0
```

Finally, disallow automatic rebooting by adding the line

```
prompt
```

to /etc/lilo.conf, in the global commands section at the top (before the per-image sections). Thus, if a cracker somehow found a way to remotely alter the Master Boot Record, installed a new kernel, or otherwise arranged to create havoc, cannot boot the new system configuration. Naturally, because Linux is so reliable you should investigate after any crash for the chance that it was cracker-induced.

All of the entries in /etc/lilo.conf cracker systems need to be secure-configured kernels, such as Linux kernels or similar. In other words, none of them should offer single-user mode or file systems with lax file permissions. None should be insecure operating systems. For those on non-Intel hardware, there may be similar capabilities.

# 2.16.5 Defeating Theft by the Floppy

![](bbox=[0.305, 0.796, 0.59, 0.833])

Most people do not take floppies very seriously any more. After all, a 3-1/2-inch floppy holds only 1.44 MB; it would take 14,000 of them to store the data of a common 20 GB disk. Still, it would hold the name, home address, home phone number, and job title of about 10,000 employees, without even using compression, and could make a headhunter
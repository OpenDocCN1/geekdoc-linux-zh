Once I finish experimenting, I'll unload the module.⁴ Specify the name of the kernel module as it appears in kldstat(8).

```
# kldunload ipmi

```

Any module that’s actively in use, such as the `opensolaris.ko` module loaded whenever you use ZFS, will not be permitted to unload. Attempting to unload an active module gives you an error like this:

```
# kldunload opensolaris
kldunload: can't unload file: Device busy

```

Sysadmins load modules much more often than they unload them. Unloading modules is expected to work, and it works the overwhelming majority of the time, but it’s arguably the most common way to panic a system. If unloading a module triggers a panic, file a bug report as per Chapter 24.

# ## Loading Modules at Boot

Use `/boot/loader.conf` to load modules at boot. The default `loader.conf` includes many examples of loading kernel modules, but the syntax is always the same. Take the name of the kernel module, chop off the trailing `.ko`, and add the string `_load="YES"`. For example, to load the module `/boot/kernel/procfs.ko` automatically at boot, add this to `loader.conf`:

```
procfs_load="YES"

```

The hard part, of course, is knowing which module to load. The easy ones are device drivers; if you install a new network or SCSI card that your kernel doesn’t support, you can load the driver module instead of reconfiguring the kernel. In this case, you’ll need to find out which driver supports your card; the man pages and Google are your friends there. I’ll be giving specific pointers to kernel modules to solve particular problems throughout this book.

Wait a minute, though—why would FreeBSD make you load a device driver to recognize hardware if it recognizes almost everything at boot? That’s an excellent question! The answer is that you may have
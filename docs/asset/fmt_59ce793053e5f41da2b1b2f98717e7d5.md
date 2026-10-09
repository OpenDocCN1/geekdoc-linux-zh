
# Task 2:
From the GRUB boot menu, type `'e'` to edit the boot commands. Append `3` to the line beginning with `"linux"`, then hit `Ctrl+X` to boot.

You should find yourself prompted to log in via command line, rather than the graphical prompt you may be used to. After logging in, you will have a shell just as if you had opened the `Terminal` application.

Now run `sudo telinit 5` to start the display manager.

You may also use `init` for the same purpose.

## Notes:
It should be noted that, according to the `telinit` man page in `Ubuntu 18.04`, “the concept of `SysV` runlevels is obsolete.” In the past, you could also use `/etc/inittab` to set the default runlevel—this is also removed in `Ubuntu 18.04`.

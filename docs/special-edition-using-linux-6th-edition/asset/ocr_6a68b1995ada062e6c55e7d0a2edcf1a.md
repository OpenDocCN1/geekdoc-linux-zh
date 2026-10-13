The second way is to use `cat /etc/mtab`. This is a table in `/etc` that will show you mounted filesystems. This will only show you filesystems mounted when the following occurs:

+   - The root filesystem is mounted read-write. (If the root filesystem is mounted read-only, this file will be in error.)
+   - The filesystem was not mounted with the `-n` option. (Don’t write to mtab.)

The third way is to use the `mount` command with no options. Both the mount command and `df` use the `/etc/mtab` file to get lists of mounted filesystems, so both suffer from the same problem mtab suffers from, as discussed previously.

Finally, you can use `cat /proc/mounts`, which will show all mounted filesystems. This works as long as the `/proc` directory is mounted. If `/proc` is not mounted (which it will not be during parts of the boot sequence), this method cannot be used. Only `/proc/mounts` will show the devfs filesystem because it isn’t of general interest.

# DISTRIBUTION DIFFERENCES

As with a number of chapters in this book, some small differences will be encountered between distributions. This does not mean any particular distribution does not follow the FHS, only that some latitude exists for such differences. These differences are generally small and not significant.

This book uses examples from Caldera OpenLinux, because it is the easiest for most Linux neophytes to install. But most of the information applies across the board. This text will attempt to point out significant differences where they exist. Also remember that with directories like `/etc`, much of what you see on your system depends on what packages you’ve installed. If a listed file doesn’t exist on your system, or you have more or other files on your system, don’t worry. This is normal.

In some cases, files exist, but in a slightly different structure. For example, both Caldera and Red Hat have `/etc/XF86Config`, but Debian uses `/etc/X11/XF86Config`. Both are perfectly legitimate. You’ll also find that Caldera and Red Hat collect system initialization files under `/etc/rc.d/`. Debian chose to have the directories found in `/etc/rc.d/` under Caldera directly in `/etc`, and included an `rc.boot` directory that contains files such as those files found directly in `/etc/rc.d` on other systems. When in doubt, or when you can’t find a particular file, try using the `locate` command to find the file:

```
```text
locate myfile
```
```

# EXAMINING KEY DIRECTORIES

Whereas all the directories serve a purpose, a few are worth a closer look. The `/etc` directory contains several directories and files that are crucial to the successful operation of the system. Almost all configuration files reside in the `/etc` directory. Understanding devices, what they are, and how they work is best accomplished by exploring the `/dev` directory. As was mentioned previously, the `/proc` directory is actually a special type of filesystem.
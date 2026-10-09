prevent users from running their own programs, but for it to be effective, also mount /tmp, /var/tmp, and anywhere else users can write their own files noexec as well.

A noexec mount doesn't prevent a user from running a shell script or an interpreted script in Perl or Python or whatever. While the script might be on a noexec filesystem, the interpreter usually isn't.

Another common use for a noexec mount is when you have a filesystem that contains binaries for a different operating system or a different hardware architecture and you don't want anyone to execute them.

# ## Disable Suid

Setuid programs allow users to run programs as if they're another user. For example, programs such as *login(1)* must perform actions as root but must be run by regular users. Setuid programs obviously must be written carefully so that intruders can't exploit them to get unauthorized access to your system. Many system administrators habitually disable all unneeded setuid programs.

The *nosuid* option disables setuid access from all programs on a filesystem. As with noexec, script wrappers can easily evade nosuid restrictions.

# ## Disable Clustering

FFS optimizes reads and writes on the physical media by clustering. Rather than scattering a file all over the hard drive, it writes out the whole thing in large chunks. Similarly, it makes sense to read files in larger chunks. You can disable this feature with the mount options *nocluster* (for read clustering) and *noclusterw* (for write clustering).

# ## Disable Symlinks

The *noSymlink* option disables symlinks, or aliases to files. *Symlinks* are mainly used to create aliases to files that reside on other partitions. To create an alias to another file on the same partition, use a regular link instead. See In(1) for a discussion of links.
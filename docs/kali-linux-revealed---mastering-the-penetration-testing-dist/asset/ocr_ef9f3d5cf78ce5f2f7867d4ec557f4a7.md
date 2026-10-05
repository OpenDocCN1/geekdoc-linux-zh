Two particular rights are relevant to executable files: setuid and setgid (symbolized with the letter "s”). Note that we frequently speak of bit, each of these boolean values can be represented by a 0 or a 1. These two rights allow any user to execute the program with the rights of the owner or the group, respectively. This mechanism grants access to features requiring higher permissions than that you would have.

# setuid and setgid executables

A setuid root program is systematically run under the super-user identity, it is very important to ensure it is secure and reliable. Any user who manages to subvert a setuid root program to a command of their choice could then impersonate the root user and have all rights on the system. Penetration testers regularly search for these types of files when they gain access to a system as a way of escalating their privileges.

A directory is handled differently from a file. Read access gives the right to consult the list of its contents (files and directories); write access allows creating or deleting files; execute access allows crossing through the directory to access its contents (for example, with the cd command). Being able to cross through a directory without being able to read it if the entries therein are known by name, but not to find them knowing their exact name.

The setgid bit applies to directories. Any newly-created item in such directories is automatically assigned the owner group of the parent directory, instead of inheriting the creator’s group as usual. Because of this, you don’t have to change your main group (with the group command) when working in a file tree shared between several users of the same dedicated group.

> The sticky bit (symbolized by the letter "t") is only useful in directories. It is especially useful for temporary directories where everybody has access (such as /tmp/); it restricts deletion of files so that only their owner or the owner of the parent directory can delete them. Lacking this, everyone could delete other users' files in /tmp/.

# SECURITY
setgid directory and sticky bit

Three commands control the permissions associated with a file:

+   - chown user file changes the owner of the file
- Changing the user and group: chown user:group file
- chgrp group file alters the owner group
- chmod rights file changes the permissions for the file

There are two ways of representing rights. Among them, the symbolic representation is probably the easiest to understand and remember. It involves the letter symbols mentioned above. You can define rights for each category of users (u/g/o), by setting them explicitly (with =), by adding
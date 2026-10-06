# Exam Essentials

Describe commands used to copy, move, and rename files in Linux. The cp command copies files, as in cp first second to create a copy of first called second. The mv command double duty as a file-moving and a file-renaming command. It works much like cp, but moves or renames the file rather than copying it.

Summarize directory-manipulation commands. The mkdir creates a new directory, and rmdir deletes a directory. You can use many file-manipulation commands, such as mv and rm (with its -r option), on directories.

Explain the difference between hard and symbolic links. Hard links are directory entries that both point to the same node and hence to the same file. Symbolic links are special files that point to another file or directory by name. Hard links must reside on a single filesystem, symbolic links may point across filesystems.

Summarize the common Linux archiving programs. The tar and gzip are both file-archiving tools that create archives of files using ordinary file access commands. The dd program is a file-copy program; but when it's fed a partition device file, it copies the entire partition on a very low-level basis, which is useful for creating low-image back backups of Linux or non-Linux systems.

Describe Linux's file ownership system. Every file has an owner and a group, identified by name. File permissions can be assigned independently to the file's owner, the file's group, and all other users.

Explain Linux's file permissions system. Linux provides independent read, write, and execute permissions for the file's owner, the file's group, and all other users, resulting in nine main permission bits. Special permissions are also available, enabling you to launch program files with modified access features or alter the Linux rules to control which may delete files.

Summarize the commands Linux uses to modify permissions. The chmod command is Linux's main tool for setting permissions. You can specify permissions using either an octal (base 8 mode) or a symbolic notation. The chown and chgrp commands enable you to change the file's owner and group, respectively.(The chown command can do both but can be run by root.)

Describe the prerequisites of using Linuxs disk quota system. Linux's disk quota system requires support in the Linux kernel for the filesystem where quotas are to be used. You must also run the quotaon command, typically from a SysV script, to enable this feature.

Explain how quotas are set. You can edit quotas for an individual user via the edquota command, as in edquota larry to edit larry's quotas. This command opens an editor on a text file that describes the user's quotas. You can change this description, save the file, and exit the editor to change the user's quotas.
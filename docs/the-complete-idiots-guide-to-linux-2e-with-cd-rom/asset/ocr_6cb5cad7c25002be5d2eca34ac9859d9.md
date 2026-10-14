system. This power is very valuable when you need to perform system administration-type tasks, but it is not an account that you want to use for any other purpose. The root account can perform certain actions that are irreversible, such as erasing all files on the disk or some other catastrophic type of thing!

Until you know more about Linux and UNIX in general, I would recommend that you don’t use the root account unless it is absolutely necessary. Examples include adding software or configuring some aspect of your system that specifically requires you to log on as root.

# Changing Groups: newgrp

Whenever you create a file, your default group is the one assigned to the group ownership of the file. If you are a member of multiple groups, you can change your effective GID by using the newgrp tool. The newgrp tool is analogous to su in that you provide the name of the group you want to use as a default for the session. If you are not a member of the group in question, you are not allowed to change your effective GID.

# Special Users

Your Linux system already comes with several accounts created.

Many of these accounts (bin, adm, lp, sync, halt, mail, and so on) exist for the benefit of a program or some other system functionality. These pseudouser accounts, as they are called, are important for the system to be able to perform certain tasks while still upholding the permissions mechanism.

# Home Directories

Each username has its own home directory. By default, Linux puts home accounts inside of the /home directory. The one glaring exception are accounts of pseudousers. (You should not try to change the location of those accounts.)

Traditionally, UNIX-like operating systems have not arrived so thoroughly configured out of the box. Rather, system administrators have had to explicitly organize home directories by themselves. Standard Linux systems, however, keep user accounts in /home.
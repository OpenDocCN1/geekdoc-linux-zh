Now that you know how to add a group, let's look at some of the things for which you can use groups. Effectively using groups can simplify your job as system administrator.

# Using Groups to Grant Permissions

Granting permissions is one of the most common uses for groups. In UNIX, nearly every feature of the system is controlled by a file or a special file (directory, device, and so on). By manipulating the group ownership and group permissions on a file or device, you can grant or remove access to that file or device on a group basis. For example, you could create a group called net and make Netscape, Lynx, irc, and any other network clients owned by group net and then set the group execute bit only. That way, only members of group net will be able to run those programs.

> **Note**
> 
> This is not a perfect solution. If you leave the world-readable flag set on the binaries owned by the net group, someone who is not a member of the net group could simply copy the binary to his home directory, chown the file to himself, and run it. While this will not work for all programs (some require supporting files or setuid bits to run properly), it might work for some, so care must be taken.

You can also use the pam_group module to configure which groups a user gains access to at which times. This is helpful if you only want to allow people access to the net group or the games group after business hours or on weekends.

> **Note**
> 
> This is also not very secure. If a user can gain access to a group once, he can create a setgid binary to allow him to access files owned by that group at any time in the future, whether he is still a member of the group or not. Consider mounting user-writable filesystems with the nosuid option whenever possible.
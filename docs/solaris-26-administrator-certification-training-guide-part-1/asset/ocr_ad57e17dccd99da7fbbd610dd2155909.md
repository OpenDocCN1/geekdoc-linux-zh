TIP. Change the root login to something other than "root," and never put a system name into the /etc/hosts.equiv file without a name or several names after it.

# The .rhosts File

The .rhosts file is the user equivalent of the /etc/hosts.equiv file. It contains a list of hosts and users. If a host-user combination is listed in this file, the specified user is granted permission to log in remotely from the specified host without having to supply a password. Note that an .rhosts file must reside at the top level of a user's home directory, because .rhosts files located in subdirectories are not consulted. Users can create .rhosts files in their home directories—another way to allow trusted access between their own accounts on different systems without using the /etc/hosts.equiv file.

The .rhosts file presents a major security problem. Although the /etc/hosts.equiv file is under the system administrator's control and can be managed effectively, any user can create an .rhosts file granting access to whomever the user chooses—without the system administrator's knowledge.

When all of the users' home directories are on a single server, and only certain people have superuser access on that server, a good way to prevent a user from using an .rhosts file is to create (as superuser) an empty file in the user's home directory. Then change the permissions in this file to 000 so changing it would be difficult, even as superuser. This would effectively prevent a user from risking system security by using an .rhosts file irresponsibly.

The only secure way to manage .rhosts files is to completely disallow them. One possible exception to this policy is the root account, which might need to have an .rhosts file to perform network backups and other remote services.

# Securing Superuser Access

The UNIX superuser identity is immune from restrictions placed on other users of the system. Any UNIX account with a UID of zero (0) is the superuser. All UNIX systems have a default superuser login named root. The user of this account can access any file and run any command. This login is valuable because any user who might have gotten himself into trouble by removing access permissions or forgetting his password, or who simply needs a file from an area to which he doesn't have access, can be helped by root. Root access, however, can be very dangerous. Root can delete anything, including the operating system (most system administrators remember deleting the entire root file system at one time or another). The root login is both dangerous and necessary. System administrators must not give this password to anyone and should use it themselves only when required.

NOTE. Change the default root login to another name. The first login attempt made by any system cracker is to try logging in as "root." If this login is on the system, the cracker is halfway in and only needs to guess the password to gain access.
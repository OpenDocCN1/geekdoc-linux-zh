owner's access permissions for the file. If the EGID and real GID of a process are the same, the process has the owner's group privileges.

The real UID is the third entry in the /etc/passwd file. Its value is a positive integer that is associated with your login name. When you log on, the login shell is assigned the real UID and all processes spawned from the login shell inherit its permissions. Any process running with a UID of zero belongs to root (the superuser) and has root privileges. The real group identification, the GID, associates a group with your login name. It is found in the fourth field of the /etc/passwd file.
You can use the id command to see these values, as shown in Example 1.6.

# EXAMPLE 1.6

```
1 $ id
uid=502(ellie) gid=502(ellie)
```

The EUID and EGID can be changed to numbers assigned to a different owner. By changing the EUID (or EGID) to another owner, you can become the owner of a process that belongs to someone else. Programs that change the EUID or EGID to another owner are called setuid or setgid programs. The passwd program is an example of a setuid program that gives the user root privileges. This enables an ordinary user to change his password, and update the passwd file (accessible only to root) without calling for a system administrator. The user temporarily becomes the superuser, root, as long as the passwd program is running because his effective user ID is temporarily is set to root. Setuid programs are often sources for security holes. The shell allows you to create setuid scripts, and the shell itself may be a setuid program. (See Chapter 16, "The System Administrator and the Shell."

# 1.6.2 The File Creation Mask

When a file is created it is given a set of default permissions. These permissions are determined by the program creating the file. Child processes inherit a default mask from their parents. The user can change the mask for the shell by issuing the umask command at the prompt or by setting it in the shell's initialization files. The umask command is used to remove permissions from the existing mask.

Initially, the umask is 000, giving a directory 777 (rwxrwxrwx) permissions and a file 666 (rw-rw-rw-) permissions as the default. On most systems, the umask is assigned a value of 022 by the /bin/login program or the /etc/profile initialization file.

The umask value is subtracted from the default settings for both the directory and file permissions as follows:

```
777 (Directory)          666 (File)
-022 (umask value)       -022 (umask value)
----------------          ------------
755                      644
Result: drwxr-xr-x        -rw-r--r--
```
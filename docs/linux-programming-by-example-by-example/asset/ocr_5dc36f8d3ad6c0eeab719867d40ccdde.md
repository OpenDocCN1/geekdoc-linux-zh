```
```
$ ls -l /usr/bin/passwd
-rwxr-xr-x 1 root     bin     703  Aug 10 16:44  /etc/passwd
```
```

Similarly, a setgid program has an s in its group execute bit. To make a program setuid, execute the following command:

```
```
$ chmod u+s mybinary
```
```

The next command makes a program setgid:

```
```
$ chmod g+s mybinary
```
```

> **CAUTION**
> 
> Programs that are setuid or setgid root are security risks because, although executable by merely mortal users, they run with superuser privileges and so have complete access to the system. They can break anything. Exercise extreme caution when executing or creating a setuid root program.

# User Information

Although machines work well with numbers, humans work much better with names. Fortunately, there are two ways to turn UIDs into humanreadable names. The getlogin function returns the login name of the user executing a process. When you have the login name, you can pass it to the getpwnam function, which returns the complete entry in /etc/passwd corresponding to that login name. The other method is to pass a process's UID to the getpwuid function, which also returns the appropriate entry from /etc/passwd.

getlogin, declared in <unistd.h>, is prototyped as follows:

```
```
char *getlogin(void);
```
```

It returns a pointer to a string containing the login name of the user running the process or NULL if this information is not available. getpwnam is declared in <pwd.h>. Its prototype is

```
```
struct passwd *getpwnam(const char *name);
```
```

name must be a pointer to a string containing the login name of interest. getpwnam returns a pointer to a passwd structure. The pointer to the returned passwd structure points to statically allocated memory that will be overwritten by the next call to getpwnam, so if you will need this information later, save the structure information before calling getpwnam again.

# Example

![](bbox=[0.04, 0.74, 0.1, 0.79])

# Example

This example illustrates getlogin's and getpwname's behavior:

```
```
/*
 *getname.c -- Get login names
 */
```
```
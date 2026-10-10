To change file permissions, use the chmod command. To change ownership of files or directories, use the chown command (as root). For example, you can create a simple shell script, such as:

```
```
#!/bin/sh
echo "Your system is:"
uname -r
uname -v

echo "Your name is:"
whoami
echo "Your contact info is:"
finger $USER
```
```

After you create the file (named me, in the following example), it will look like this:

```
```
$ ls -l doit
-rw-rw-r--   1 bball    bball      124 Apr  6 17:18 me
```
```

You can then use the chmod command to make the file executable like this:

```
```
$ chmod +x me
```
```

The file will then look like:

```
```
-rwxwr-xr-x  1 bball    bball      124 Apr  6 17:18 me
```
```

You can also take away permission by using the chmod command like this:

```
```
$ chmod -x me
```
```

Another way to add execute permission and restrict use for the owner is with the chmod command. This time, however, use the numerical values representing the permission notation for the file:

```
```
$ chmod 744
$ ls -l me
-rwxr--r--   1 bball     bball      124 Apr  6 17:18 me
```
```

Here you can see that only the owner, *bball*, has read, write, and execution permission (*rwx* = 7). All others only have read permission (*r* = 4).

# Changing Device Permissions

You will most often change permissions on your hardware's devices in order to allow users to access a device such as a serial port or modem. This is most often
man page names and descriptions. Assuming, for instance, that you cannot remember that it is uname that will give you your current Linux kernel version, you can pass the word kernel to apropos. You will probably get many lines of output, but they should include these:

```
$ apropos kernel  
systemd-udevd-kernel.socket (8) - Device event managing daemon  
uname (2) - get name and information about current kernel  
urandom (4) - kernel random number source devices
```

If you do not need a command’s full documentation, you can quickly get basic data about a command using type. This example uses type to query four separate commands at once. The results show us that cp ("copy") is a program that lives in /bin/cp and that kill (change the state of a running process) is a shell builtin—meaning that it is actually a part of the Bash shell itself:

```
$ type uname cp kill which  
uname is hashed (/bin/uname)  
cp is /bin/cp  
kill is a shell builtin  
which is /usr/bin/which
```

Notice that, besides being a regular binary command like cp, uname is also "hashed." That is because Frank recently used uname and, to increase system efficiency, it was added to a hash table to make it more accessible the next time you run it. If he would run type uname after a system boot, Frank would find that type once again describes uname as a regular binary.

> NOTE A quicker way to clean up the hash table is to run the command hash -d.

Sometimes—particularly when working with automated scripts—you will need a simpler source of information about a command. The which command that our previous type command traced for us, will return nothing but the absolute location of a command. This example locates both the uname and which commands.

```
$ which uname which  
/bin/uname  
/usr/bin/which
```

> NOTE If you want to display information about "builtin" commands, you can use the help command.
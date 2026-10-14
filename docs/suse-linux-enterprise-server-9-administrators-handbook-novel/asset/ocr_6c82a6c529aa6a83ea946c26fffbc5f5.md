# WARNING

You can see from the preceding example how easy it is to create a root SUID program that executes “some command.” Some malicious person can easily substitute the “/bin/bash” command for something really nasty such as “/bin/rm -frv /”! Therefore, if you don’t know where a SUID/SGID (root or not) program comes from or what it will do exactly, do not run it!

# TIP

If you find some file to be suspicious, do not execute it. You can dump all the strings in the file and look for some interesting stuff using the strings command like this:

```
Athena:/home/admin # strings become-root
/lib/ld-linux.so.2
SuSE
libc.so.6
__errno_location
setgid
_IO_stdlin_used
__libc_start_main
setuid
__gmon_start__
GLIBC_2.0
PTRhP
/bin/bash
```

As you can see from the output, strings showed references to setgid, setuid, system, and /bin/bash, suggesting this is a SUID program of some sort. When you use strings, it is relatively easy to figure out what files the binary wants to open, if there are any special messages (such as “Gotcha!” as Trojan horses tend to contain), and so on.

The system() command in the preceding example can also be used to execute a script, and not just commands. Therefore, if you decide that you need a SUID shell script and don’t want to use Perl, you can modify the example slightly and use it as a “wrapper” for your script. You may be tempted to pass the script’s path and name from the command line so you have a generic wrapper. However, this approach can be dangerous. If some disgruntled user stumbles upon it, he or she could use it to execute some nasty script or command that
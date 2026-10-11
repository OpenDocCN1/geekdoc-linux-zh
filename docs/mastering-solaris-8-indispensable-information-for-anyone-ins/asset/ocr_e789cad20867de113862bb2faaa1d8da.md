If you want to limit root login to a single port, use the following example:

```
# root can login only on /dev/term/a serial port only
CONSOL E=/dev/term/a
```

Almost everyone who deals with computers on any level has heard of the Trojan horse. Briefly, it is a program that appears to be innocent but does something either disruptive or destructive to your system. As a simple example, you could store the following program in a file called tfile:

```
while true
do
    echo 'You look terrible today! Out late again? Shame on you!' > /dev/console
done
```

If you were logged on as superuser and ran this command, it would continue to write the rather amusing message to the console. A disgruntled programmer could do much worse by simply changing superuser’s PATH variable to include a publicly writable directory at the start of the PATH string. Then they would need to put the bogus file in that directory. Because the bogus version appears in a directory mentioned earlier than the real one in PATH, the shell would run it. The next time superuser tried to run tfile, the bogus version would run. Although this is a simple example, Trojan horses have been known to create havoc in a computer system. When you log in as root, the shell will use /etc/default/login, but when you use su to become root, the shell reads the /etc/default/su script. Both scripts have a line that defines the variable SUPATH, which controls the value of PATH when you become superuser. Un-comment the line that begins with # SUPATH and change the value assigned to SUPATH there. Do not add . to SUPATH because you may set up a Trojan horse as described. The fewer directories you keep in your PATH when you are root, the less likely you will execute a bogus program as root. If possible, keep only the default /usr/sbin and /usr/bin directories. Remember, never include the working directory anywhere in the PATH string.

Leave the /etc/hosts .equiv and individual users’ .rhosts files empty. You can install products such as SKIP or IPsec, but they are somewhat complicated. Easier steps like preventing remote logins go a long way in keeping your host secure. Solaris does provide a number of utilities and packages for auditing host security setup. There is a three-level package called ASET, or Automated Security Enhancement Tool, that performs security auditing and detection. Process accounting can provide a continuous record of user actions on your system, but it will slow performance somewhat. If you have a large system, you may want to send important syslog information to a
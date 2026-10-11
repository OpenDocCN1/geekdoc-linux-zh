
## Exam 101

36. Which environment variable would be used to specify the location of files that you wish to run without specifying an absolute path?
- A. `HOME`
- B. `PS1`
- C. `PATH`
- D. `TERM`

37. The ____________________ command is used to change ownership of a file.

38. When booting your system you notice that your sound module failed to load; however, the error message scrolled by too quickly. What command can you use to view the errors?
- A. `dmesg`
- B. `messages`
- C. `errors`
- D. `lilo`

39. What command is used to create a new archived file using compression?
- A. `gzip -t`
- B. `tar -cfz`
- C. `compress -tf`
- D. `bzip2 -tbz`

40. Which command is used to view processes running in the background?
- A. `dmesg`
- B. `ls`
- C. `bg`
- D. `jobs`

41. Which utility is used to view the beginning of a file?
- A. `tac`
- B. `cat`
- C. `head`
- D. `top`

42. Which type of quota limit prevents a user from creating new files?
- A. stop limit
- B. soft limit
- C. hard limit
- D. max limit

43. Which runlevel is used for administrative tasks performed locally, disallowing network connections to the system?
- A. 0
- B. 1
- C. 3
- D. 6

44. User quotas are maintained in which file?
- A. `/etc/fstab`
- B. `/etc/passwd`
- C. `/quota.user`
- D. `/lilo`

45. You are told by a co-worker that information pertaining to the syslog command can be found in man page 3. How would you view this information?
- A. `man syslog 3`
- B. `man syslog -3`
- C. `man -3 syslog`
- D. `man 3 syslog`

46. Which command is not used to view the contents of a file?
- A. `cat`
- B. `more`
- C. `less`
- D. `expand`

47. The _______ command is used to unmount a file system.

48. The _______ command will display previously entered commands.

49. What type of information might you find using www.deja.com?
- A. man pages
- B. Usenet postings
- C. software patches
- D. kernel updates

50. Which directory utilizes no disk space?
- A. `/proc`
- B. `/boot`
- C. `/root`
- D. `/local`

51. The ______ command is used to perform a consistency check on file systems.

52. Which command would create a file called mydirlisting that includes a detailed listing of all the files and directories located within your home directory?
- A. `ls -aLR $HOME > mydirlisting`
- B. `ls -d > mydirlisting`
- C. `mydirlisting < ls -al $HOME`
- D. `ls -al | mydirlisting`

## Exam 102

1. The ______ command is used to create an ext2 file system.

2. You're repairing the master boot record on a system. You have booted the system via a boot disk and currently have the root volume mounted to /recover. How would you reinstall LILO?
- A. `lilo -r /recover/boot`
- B. `lilo -f /recover`
- C. `lilo -r /recover`
- D. `lilo -r /recover -b /recover/boot`

3. The ______ file needs to be updated when a new library is added.

4. Which command removes a package named editor-2.0.i386.rpm?
- A. `rpm -i editor-2.0.i386.rpm`
- B. `rpm -e editor-2.0.i386.rpm`
- C. `dpkg -install editor-2.0.i386.rpm`
- D. `apt-get install editor-2.0.i386.rpm`

5. To make a single change to the kernel configuration before compiling, you would edit which file?
- A. `/usr/src/linux/Makefile`
- B. `/usr/src/linux/.config`
- C. `/usr/src/linux/config`
- D. `/usr/src/linux/configure`

6. Which command will tell you which package owns the file /etc/printcap?
- A. `dpkg -F /etc/printcap`
- B. `rpm -f /etc/printcap`
- C. `who /etc/printcap`
- D. `rpm -qf /etc/printcap`

7. The __________ file is executed for all nonlogin bash sessions.

8. Which command shows the route between your host and the remote host www.somedomain.org?
- A. `traceroute -n www.somedomain.org`
- B. `route www.somedomain.org`
- C. `ping -r www.somedomain.org`
- D. `route -n www.somedomain.org`

9. Which command is the best to use to find a contact name for another domain?
- A. `nslookup`
- B. `whois`
- C. `whois`
- D. `dig`

10. Which command(s) must be run after the inetd.conf file is updated?
- A. `/etc/rc.d/init.d/inetd restart`
- B. `kill -1 inetd`
- C. `kill -1 `cat /var/run/inetd.pid``
- D. No command needed.

11. The __________ file can be created to keep nonroot users from logging in to the system.

12. Which command(s) is/are used to enable shadow passwords?
- A. `shadow`
- B. `pwconv`
- C. `pwconv`
- D. `grpconv`

13. Which command(s) is/are used to decompress the file mydoc.gz?
- A. `gunzip mydoc.gz`
- B. `tar -zxv mydoc.gz`
- C. `gzip -d mydoc.gz`
- D. `gunzip -d mydoc.gz`

14. To activate all swap partitions on the system you would use the _______ command (with options).

15. Which command displays the output of the utmp file?
- A. `what`
- B. `who`
- C. `last`
- D. `when`

16. The _______ tool is used to control the Apache httpd service.
- A. `apached`
- B. `httpdctl`
- C. `htmgr`
- D. `apachecl`

17. Which command displays queue information for all local printers?
- A. `lpg -a`
- B. `lpc -a`
- C. `printq`
- D. `lpg -v`

18. Which disk partitioning tool provides a GUI?
- A. `fdisk`
- B. `cfdisk`
- C. `Disk Druid`
- D. `gnodisk`

19. The _______ command shows all loaded kernel modules.

20. Which command in vi searches for the text *Linux*?
- A. ESC, s, Linux
- B. ESC, f, Linux
- C. `\Linux`
- D. `/Linux`

21. Which command must be run when a new mail alias is added?
- A. `newalias`
- B. `newaliases`
- C. `genaliases`
- D. `kill -1 `cat /var/run/sendmail.pid``

22. You want to make the directory / share available via NFS. All users on your local network should be allowed to read and write files. Which of the following is correct, assuming that your local network is 192.168.1.0 and your machine is part of the DNS domain mydomain.org?
- A. `/local 192.168.1.0/255.255.255.0(rw)`
- B. `/local 192.168.1.0/*(rw)`
- C. `/local *.org(rw)`
- D. `/local ALL.mydomain.org(rw)`

23. Which script is run when X Window starts?
- A. `.xinit`
- B. `.xrc`
- C. `.startxrc`
- D. `.xinirc`

24. Which command adds a new default route to the system?
- A. `ifconfig add default gw 1.2.3.4`
- B. `route add gw 1.2.3.4`
- C. `route add default gw 1.2.3.4`
- D. `ifconfig add 0.0.0.0 mask 255.255.255.0 gw 1.2.3.4`

25. Dave is going away on vacation for two weeks and wants his mail forwarded to Sue while he is away. Which change should he make?
- A. Add "sue" to `/etc/aliases`.
- B. Add "sue" to `~/.forward`.
- C. Add "sue" to `~/.aliases`.
- D. Add a rule to pine to forward the mail.

26. The Samba daemon responsible for handling name resolution is which of the following?
- A. `nmbd`
- B. `smbd`
- C. `winds`
- D. `named`

27. The ________ command can be used to change to another user.

28. Which command should be used to allow the host norbert to connect to the local X server?
- A. `xhost +`
- B. `cat norbert > .rhosts`
- C. `xhost +norbert`
- D. `rhosts +norbert`

29. You have just configured a new mail server named deathstar. Which entry should you make into DNS to make this the primary mail server?
- A. `IN MX 20 deathstar`
- B. `IN MX 10 deathstar`
- C. `IN MX 0 deathstar`
- D. `IN MX 100 deathstar`

30. Which command would you use to copy the /Documents directory and all subdirectories from the current system to the remote system newman?
- A. `cp -R /Documents newman:/`
- B. `scp -r /Documents root@newman:/`
- C. `rcp -R /Documents newman:/`
- D. `scp -R root@newman:/ /Documents`

31. Which command would update your Debian system to the latest version of all installed packages?
- A. `apt-get update ; apt-get upgrade`
- B. `apt-get upgrade ; apt-get update`
- C. `apt-get refresh`
- D. `apt get update ; apt get upgrade`

32. You have set up a new mail server behind your firewall. You now need to open up port _______ for access to work.

33. The _______ tool outputs a file showing the PnP configuration of the system.

34. What does the following IP chains block accomplish? (Select all that apply.)

```bash
iptables -F input
echo 1 > /proc/sys/net/ipv4/ip_forward
iptables -A output -src 192.168.1.0/24 -dst ! 192.168.1.0/24 -j MASQ
iptables -A input -dst 192.168.1.12 -j ACCEPT
```

- A. The 192.168.1.0/24 network is being masq'd.
- B. IP forwarding is disabled.
- C. IP forwarding is enabled.
- D. Access to 192.168.1.12 is allowed.

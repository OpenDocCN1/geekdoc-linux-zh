# Initial Triage and Live Response: Data Analysis • Chapter 97

+   - Presuming the UNIX dialect supports IPv6, to list only open IPv6 network files, use:

```
lsof -i 6
```

+   - To list all files using any protocol on ports 513, 514, or 515 of host wonderland.cc.purdue.edu, use:

```
lsof -i @wonderland.cc.purdue.edu:513-515
```

+   - To list all files using any protocol on any port of mace.cc.purdue.edu (cc.purdue.edu is the default domain),

```
lsof -i @mace
```

+   - To list all open files for login name "abe," or user ID 1234, or process 456, or process 123, or process 789,

```
lsof -p 456,123,789 -u 1234,abe
```

+   - To list all open files on device /dev/hd4, use:

```
lsof /dev/hd4
```

+   - To find the process that has /u/abe/foo open, use:

```
lsof /u/abe/+L1
```

Additionally, I like to use the “+L1” to display all of the unlinked (or marked for deletion) files. (See Figure 4.14).

# Figure 4.14 +L1 Switch

```
root@Forensics3:~# lsof +L1
COMMAND PID USER FD TYPE SIZE NODE NAME
init 1 root root CIR 5,1 0 2265/console (deleted)
init 1 root 1U CIR 5,1 0 2265/console (deleted)
init 1 root 2U CIR 5,1 0 2265/console (deleted)
deskbar-a 5085 copeque REG 8,1345 0 4145318 /home/copeque/mozilla/firefox/12726kwq.deautail/prefs.js
root@Forensics3:~# 
```

This command switch proved itself useful more than once, when an illicit user has tried to cover their tracks by deleting something.

![](bbox=[0.737, 0.861, 0.952, 0.883])
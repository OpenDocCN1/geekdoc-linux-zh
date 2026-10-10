
# CLI of the Metasploit Framework

Metasploit CLI (msfcli) is one of the interfaces that allow the Metasploit Framework to perform its tasks. This is a good interface to learn how to manage Metasploit Framework, or to evaluate/write a new exploit. It is also useful in case it is required to use it in scripts and apply automation for tasks.

```
# msfcli -h
# msfcli
# msfcli [Exploit Route] [Option = Value]
```

The following example will use the auxiliary module called “MySQL Server Version Enumeration” which allows enumerating the version of MySQL servers.

For the following example, the auxiliary module named “Tomcat Application Manager Login Utility” will be used in the Metasploit Framework, which will simply attempt to authenticate to the Tomcat Application Manager instance using specific users and passwords.

```
msf> search tomcat
msf> use auxiliary/scanner/http/tomcat_mgr_login
msf auxiliary (tomcat_mgr_login)> show options
msf auxiliary (tomcat_mgr_login)> set RHOSTS [Objective IP]
msf auxiliary (tomcat_mgr_login)> set RPORT 8180
msf auxiliary (tomcat_mgr_login)> set USER_FILE /usr/share/metasploit-framework/data/wordlists/tomcat_mgr_default_users.txt
msf auxiliary (tomcat_mgr_login)> set PASS_FILE /usr/share/metasploit-framework/data/wordlists/tomcat_mgr_default_pass.txt
msf auxiliary (tomcat_mgr_login)> exploit
msf auxiliary (tomcat_mgr_login)> back
Using common usernames
```

The demonstrations presented below allow strengthening the use of some tools presented during the Course. These demonstrations focus on the Exploitation and Post-Exploitation phase, that is, the processes that an attacker would perform after gaining access to the system by exploiting a vulnerability.

### Demonstration using a local exploit to escalate privileges.

```
# ssh -l msfadmin 192.168.159.129
```

Once inside the system we proceed to use the "sudo" command.

```
# sudo cat /etc/shadow
# sudo passwd root
```

Enter a new password and then:

```
# su -
# id
```

The Post Exploitation phase would be similar to the one detailed in the first example.

# Chapter 7 – Solving Level Problems

## Level 0 Problem

**Login: level08 Password: guest Study: Introduction Level 0**

Since it is extremely simple, it is just meant to make you understand some of the concepts you will need to move on to the next levels. I will take this space to explain. Our main objective at level0, as in all others, is to get the password to the next level. This can be done by running the `pass`, which is in the `bin` directory. Try connecting to HackersLab and typing `pass`. A screen appears that will wax and show you the level0 password. So to get the password for the level1, do I have to login as this user? How is this possible?

There is another way. At every level, there is a file that has the UID (user identification number) higher than yours and the GID (identical group identification number). The task is: how to explore this file so that through it you can execute the `pass` command and get the next password? Now if we do this through it and it has a higher user privilege (UID), our system will “think” that we are the other user. Difficult? Let’s see an example.

Suppose we connect to HackersLab. Let's create one imaginary level0, just as a test:

```
Login: level0
Password: [level0]
[level0 @ level0] $ whoami
level0
[level0 @ level0] $ id
UID=2000 GID=2000 OTHER ANY=9999
```

So far, what have we achieved? We have successfully logged in to level0, we have entered the `whoami` command, which informed us that the username is level0, and the `id` command, which provided us with user IDs (UID), group IDs (GID), and other things that will not be needed for us.

Now I will have the system search for files that have a UID superior to ours. For example, if our UID is 2000, then I want to search for files that have UID 2001 (level1).

```
[level0 @ level0] $ find / -uid 2001 -gid 2000
/tmp/suzuki: Permission Denied
/bin/joy: Permission Denied
```

Permission Denied
/etc/test
/usr/local/yu: Permission Denied
/var/shenmue: Permission Denied.

I asked the system to show me all the files that they allowed and are user level1 (which has UID 2001) and group level0 (from GID 2000). Why look for the GID? Simple. The file needs to be from our group so that we can manipulate it. This will become clearer in a moment. We only found the `/etc/test` file. Everything else with Permission Denied is rubbish.

How to list, then, only the files we want?

```
[level0 @ level0]$ find / -uid 2001 --gid 2000 2>/dev/null
/etc/test
```

Redoing the command, I included the string `2> /dev/null`, which I told the system “anything not necessary (2) send to (>) the trash (/dev/null)”. Thus, we only got the result we expected. So, let’s list the in-file formations.

```
[level0 @ level0]$ ls -la /etc/test
-rwxr-x--- 1 level1 level0 10876 Mar 8 06:24 test
```

From the information, we confirmed what we wanted. It is a file created by user level1 and that belongs to group level0. The user who created it has the permission of total users, group users are allowed to execute only, and others not even that. Just out of curiosity, I could browse the file using the username instead of UID? Of course!

Perfect. We found the file the same way. How can we just run the file, let’s try:

```
[level0 @ level0] $ cd /etc
[level0 @ level0 etc]$ ./test
Error: file not found.
```

An error has occurred. This is because our executable file is not in PATH. `PATH` is a variable that indicates which directories are the files that can be run from the directory you are in. We can then only co-place “./” (dot and slash) in front of the executable. Necessarily will run it without relying on PATH.

```
[level0 @ level0 etc] $ ./test
/bin/pass
```

Congratulations ... the password for level1 is xxxxx. Ready! In our imaginary example, the test file ran the pass (that command that gives us the password, remember?). But it gave us the password of level1 instead of 0? This was because the test had user permission from level1, so we fooled the pass command and it gave us the prize. At every level, this must be done differently.

If you have not understood this, we will answer your questions now, in the practical part step by step and then, we'll connect to drill.hackerslab.org via telnet:

```
Login: level0
Password: guest
Connecting to level0.
```

We entered. I typed the `whoami` and `id` commands to see the username and identification numbers (IDs). It doesn't have to be done; I just did it for your ease of understanding. We are ready to search for our target file. I typed `find / -user level1 -group level0 2> /dev/null` to look for files created by level1 and having level0 as a group. The system found some files, including `/dev/.hi`. Dev means devices. Following the level hint, I will try this file first. I listed the information and saw that it has executed permissions for users of the level0 group. So let's run it and see what happens. I typed `cd /dev` to access the directory where the target file is. I typed, so `.hi`. The system returned an error saying that the command was not found. This means that the command is not in the PATH. No problem ... we hit a “./” in front of the command and execute it: `./.hi`. Apparently, nothing happened.

Let's check: Let's try the `id` command. Oh! A surprise! A new ID has appeared with EUID number 2001 (level1). This EUID didn't exist before ... it was given to us by the program. We will then try the `whoami` command, just to take the doubts. That! The command informed us that we are level1 (or at least that we have permission from level1). How could `.hi` do this? Simple, he was a backdoor (funds or trojan horse). The moment we ran it, he ran the `/bin/sh` command and created another shell (command session) within the first one, but with your permissions. This means that if we try to type the `pass` command (which returns the level password), now we get ... The password for the next level !!! The password for level1, then, is the newworld.

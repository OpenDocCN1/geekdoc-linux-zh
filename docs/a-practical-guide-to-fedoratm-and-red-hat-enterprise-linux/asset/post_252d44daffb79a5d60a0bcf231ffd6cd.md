
by a user by giving the command **kill -15 -1** or, equivalently, **kill -TERM -1** while you are logged in as that user. Using **-1 (one)** in place of the process ID tells **kill** to send the signal to all processes that are owned by that user. For example, working as **root** you could enter the following command:

```
# su zach -c 'kill -TERM -1'
```

If this does not kill all processes (sometimes **TERM** does not kill a process), you can use the **KILL** signal (**-9**). The following line will definitely **kill** all processes owned by **Zach** and will not be friendly about it:

```
# su zach -c 'kill -KILL -1'
```

If you do not include **su zach -c**, this command brings the system down.

# **lsof: FINDS OPEN FILES**

The **lsof** (list open files) utility displays the names of open files. Its options display only certain processes, only certain file descriptors of a process, or only certain network connections (network connections use file descriptors just as normal files do and **lsof** can show these as well). After you have identified a suspect process using **ps** **-ef**, enter the following command:

```
# lsof -s -p pid
```

Replace **pid** with the process ID of the suspect process; **lsof** displays a list of file descriptors that process **pid** has open. The **-s** option displays the sizes of all open files, and the **-p** option allows you to specify the PID number of the process of interest (**lsof** does not work if you combine these options). This size information is helpful in determining whether the process has a very large file open. If it does, contact the owner of the process or, if necessary, kill the process. The **-n** option redisplay the output of **lsof** every **n** seconds.

# KEEPING A MACHINE LOG

A machine log that includes the information shown in Table 15-3 can help you find and fix system problems. It is useful to note the time and date of each entry in the log. Avoid the temptation to keep the log **only** on the computer—it will be most useful to you when the system is down. Also keep email that details user problems. One strategy is to save this mail to a separate file or folder as you read it. Another approach is to set up a mail alias that users can send mail to when they have problems. This alias can then forward mail to you and also store a copy in an archive file. Following is an example of an entry in the **/etc/aliases** file (page 746) that sets up this type of alias:

```
trouble: admin,/var/spool/mail/admin.archive
```

Email sent to the **trouble** alias will be forwarded to the **admin** user as well as stored in the file **/var/spool/mail/admin.archive**.

## Table 15-3 Machine log

| Entry | Function |
| :--- | :--- |
| Hardware modifications | Keep track of the system hardware configuration: which devices hold which partitions, the model of the new NIC you added, and so on. |
| System software modifications | Keep track of the options used when building Linux. Print such files as /usr/src/linux/.config (Linux kernel configuration). The file hierarchy under /etc/sysconfig and /etc/default contain valuable information about the network configuration, among other things. |
| Hardware malfunctions | Keep as accurate a list as possible of any problems with the system. Make note of any error messages or numbers the system displays on the system console and identify what users were doing when the problem occurred. |
| User complaints | Make a list of all reasonable complaints made by knowledgeable users (for example, “Machine is abnormally slow”). |

# Keeping the System Secure

No system with dial-in lines or public access to terminals is absolutely secure. Nevertheless, you can make a system as secure as possible by changing the passwords of the root password frequently and by choosing passwords that are difficult to guess. Do not tell anyone who does not absolutely need to know the root password. You can also encourage system users to choose difficult passwords and to change them periodically.

- **Passwords** This section contains a technical discussion of passwords; see “Password Security” on page 136 for a more practical discussion.

By default, passwords for Fedora/RHEL use MD5 (page 1260) hashing, which makes them more difficult to crack than passwords encrypted with DES (page 1159). Of course, it makes little difference how well encrypted your password is if you make it easy for someone to find out or guess what the password is. The system-config-authentication utility allows you to specify a local password hashing algorithm: Select the Advanced Options tab and make a selection from the drop-down box labeled Password Hashing Algorithm.

A password that is difficult to guess is one that someone else would not be likely to think you would choose. Do not use words from the dictionary (spelled forward or backward); names of relatives, pets, or friends; or words from a foreign language. A good strategy is to choose a couple of short words, include some punctuation (for example, put a ^ between them), mix the case, and replace some of the letters in the words with numbers. If it were not printed in this book, an example of a good password would be C&cyGram5 (candygrams). Ideally, you would use a random combination of ASCII characters, but that would be difficult to remember.

You can use one of several password-cracking programs to find users who have chosen poor passwords. These programs work by repeatedly hashing words from dictionaries, phrases, names, and other sources. If the hashed password matches the output of the program, then the program has found the password of the user. Two programs that crack passwords are `crack` (crack package) and `john` (John the Ripper; www.openwall.com/john; `john` package). These and many other programs and security tips are available from CERT (www.cert.org), which was originally called the Computer Emergency Response Team.

It takes a lot of computational power to crack a good password. Password-cracking programs generally start by looking at the character set comprising uppercase and lowercase letters and numbers. When you add symbols, they have to do more work to crack a password. Also, the longer the password, the more computational power it takes to crack. Make your password long enough so it will be harder to crack and short enough so you can remember it; 8–20 characters is usually a good length. Include a few symbols such as #, @, and %. If it takes too long to crack your password, the person or machine doing the dirty work might move on to easier accounts.

![](img/243613168ac865b539f12460d966088e_682_0.png)

Make sure no one except a user with `root` privileges can write to files containing programs that are owned by `root` and run in setuid mode (for example, `passwd`, `su`, and `sudo`; page 196). Also make sure users do not transfer programs that `run` in setuid mode and are owned by `root` onto the system by means of mounting tapes or disks. These programs can be used to circumvent system security. One technique that prevents users from having `setuid` files is to use the `nosuid` flag to `mount`, which you can set in the flags section in the `fstab` file. Refer to “Mount Options” on page 522.

![](img/243613168ac865b539f12460d966088e_682_1.png)

The `BIOS` in many machines gives you some degree of protection from an unauthorized person who tries to modify the `BIOS` or reboot the system. When you set up the `BIOS`, look for a section named `Security`. You can probably add a `BIOS` password. If you depend on the `BIOS` password, lock the computer case—it is usually a simple matter to reset the `BIOS` password by using a jumper on the motherboard.

# LOG FILES AND MAIL FOR ROOT

Users frequently email `root` and `postmaster` to communicate with the system administrator. If you do not forward `root`'s mail to yourself (`/etc/aliases` on page 746), remember to check `root`'s mail periodically. You will not receive reminders about mail that arrives for `root` when you use `su` to perform system administration tasks. However, you can use the command `su -c 'mail -u root'` to look at `root`'s mail.

Review the system log files regularly for evidence of problems. Some important files are `/var/log/messages`, where the operating system and some applications record errors; `/var/log/secure`, which holds messages pertaining to system security; `/var/log/maillog`, which contains errors from the mail system; and `/var/log/cron`, which contains messages from `cron`.

The `logwatch` utility (`logwatch` package) is a report writer that is written in Perl and sends email reports about log files. Installing the `logwatch` package creates the `/etc/cron.daily/logwatch` file that runs this script daily and emails its output to `root`. Refer to the `logwatch` `man` page and to the script itself for more information.

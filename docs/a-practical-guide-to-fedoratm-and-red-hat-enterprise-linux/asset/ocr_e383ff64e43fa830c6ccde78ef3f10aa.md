by a user by giving the command **kill -15 -1** or, equivalently, **kill -TERM -1 while you are logged in as that user.** Using **-1 (one)** in place of the process ID tells **kill** to send the signal to all processes that are owned by that user. For example, working as **root** you could enter the following command:

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
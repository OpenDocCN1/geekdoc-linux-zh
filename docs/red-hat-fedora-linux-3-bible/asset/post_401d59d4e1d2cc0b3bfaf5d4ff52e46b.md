
Block grace time: 7days; inode grace time: 7days

User used soft hard grace used soft hard grace
root -- 1973984 0 0 2506 3 0 0
jake -- 1296 700 1700 6days

In this example, jake has exceeded his soft limit of 700 blocks. He currently has six days left in his grace period to remove enough files so that he does not become the hard limit.

### Using du to check disk use

You can discover the most voracious consumers of disk space using the du command. Invoke du with the -s option and give it a list of directories; it reports the total disk space used by all the files in each directory. Add an -h option to display disk space used in numbers, followed by kilobytes (k), megabytes (M), or gigabytes (G). The -c option adds a total of all requested directories at the end. The following checks disk usage for several home directories:

```bash
# du -hcs /home/tom /home/bill /home/tina /home/sally
```

This should result in a list of all of your users' home directories preceded by the number of kilobytes that each directory structure uses. It looks something like this:

```bash
339M	/home/tom
81M	/home/bill
31M	/home/tina
44k	/home/sally
450M	total:
```

### Removing temp files automatically

Some potential disk-consumption problems are set up to take care of themselves. For example, directories for storing temporary files used by applications (such as /tmp and /var/tmp) can consume lots of disk space over time. To deal with the problem, Fedora includes the tmpwatch facility. The tmpwatch command runs from the cron file /etc/cron.daily/tmpwatch to delete unused temporary files. Here's what that file contains:

```bash
/usr/sbin/tmpwatch 240 /tmp
/usr/sbin/tmpwatch 720 /var/tmp
for d in /var/{cache/man,catman}[/cat?;X11R6/cat?,local/cat?]; do
    if [ -d "$d" ]; then
        /usr/sbin/tmpwatch -f 720 $d
    fi
done
```

Each day, this tmpwatch script runs to delete temporary files that haven't been used for a while. Files from the /tmp and /var/tmp directories are removed after 240 and 720 hours of not being accessed, respectively. Temporary man page files stored in /var/cache subdirectories are also checked and deleted after 720 hours of disuse.

## Sending Mail to All Users

Occasionally, you need to send messages to all users on your system. Warning users of planned downtime for hardware upgrades is a good example. Sending e-mail to each user individually is extremely time consuming and wasteful; this is precisely the kind of task that e-mail aliases and mailing lists were invented for. Keeping a mailing list of all the users on your system can be problematic, however. If you are not diligent about keeping the mailing list current, it becomes increasingly inaccurate as you add and delete users. Also, if your system has many users, the mere size of the alias list can become unwieldy.

The following script, called `mailfile`, provides a simple method of working around these problems. It grabs the login names from the `/etc/passwd` file and sends e-mail to all users.

> **NOTE:** The following script skips the first 17 accounts in your `/etc/passwd` file (to exclude administrative accounts from receiving the e-mail). Check your `/etc/passwd` file and change the script to include the exact number of administrative accounts (which could be around 50, depending which package you have installed). Then make sure that all user accounts are listed after your administrative accounts in that file.

```bash
#!/bin/csh
#
# mailfile:  This script mails the specified file to all users
#             of the system.  It skips the first 17 accounts so
#             we do not send the email to system accounts like
#             `root'.
#
# USAGE: mailfile "Subject goes here" filename.txt
#
# Check for a subject
if ( `echo $1 | awk '{ print $1 }' == "" ) then
    echo You did not supply a subject for the message.
    echo Be sure to enclose it in quotes.
    exit 1
else
    # Get the subject of the message
    set subject=$1
endif

# Check for a filename
if ( $2 == "" ) then
    echo You did not supply a file name.
    exit 2
else
    # Get the name of the file to send
    set filename=$2
endif

#
# Check that the file exists
#
if ( -f $filename ) then
    echo Sending file $filename
else
    echo File does not exist.
    exit 3
endif

#
# Loop through every login name, but skip the first 17 accounts
#
foreach user ( `awk -F: '{ print $1 }' /etc/passwd | tail +17` )
    # Mail the file
    echo Mailing to $user
    mail -s "$Subject" $user < $filename

    # sleep for a few seconds so we don't overload the mailer
    # On fast systems or systems with few accounts, you can
    # probably take this delay out.
    sleep 2
end
```

The script accepts two parameters. The first is the subject of the e-mail message, which is enclosed in quotes. The second is the name of the file containing the text message to send. Thus, to send an e-mail message to all users warning them about an upcoming server hardware upgrade, I may do something similar to the following:

```bash
mailfile "System upgrade at 5:00pm"  upgrade.txt
```

The file upgrade.txt contains the text of the message to be sent to each user. The really useful thing about this approach is that I can save this text file and easily modify and resend it the next time I upgrade the system.

> **TIPS:** If your users log in to your system using text-based logins instead of graphical logins, you can add messages to the /etc/motd file to have them reach your users. Any text in that file will be displayed on each user's screen after the user logs in and before the first shell prompt appears.

## Summary

It is not uncommon for a Linux system to be used as a single-task server with no actual users. It sits quietly in a server room, serving Web pages or handling domain name service, never crashing, and rarely needing attention. This is not always the case, however. You may have to support users on your Linux system, and that can be the most challenging part of your system administration duties.

Fedora provides a variety of tools that help you with your administrative chores. The `useradd`, `usermod`, and `userdel` commands enable easy command-line manipulation of user account data. Furthermore, creating a support mailbox and building shell scripts to automate repetitive tasks lightens your load even more. Fedora Linux builds on top of the rich history of UNIX and provides an ideal platform to support the diverse needs of your users.

## Chapter 12: Automating System Tasks

### In This Chapter

- Understanding shell scripts
- System initialization
- System startup and shutdown
- Scheduling system tasks

You'd never get any work done if you typed every command that needs to be run on your Fedora system when it starts. Likewise, you could work more efficiently if you grouped together sets of commands that you run all the time. Shell scripts can handle these tasks.

A shell script is a group of commands, functions, variables, or just about anything else you can use from a shell. These items are typed into a plain-text file. That file can then be run as a command. Fedora uses system initialization shell scripts during system startup to run commands needed to get things going. You can create your own shell scripts to automate the tasks you need to do regularly.

This chapter provides a rudimentary overview of the inner workings of shell scripts and how they can be used. You learn how shell scripts are responsible for the messages that scroll by on the system console during booting and how simple scripts can be harnessed to a scheduling facility (such as cron or at) to simplify administrative tasks.

You also learn to fine-tune your machine to start at the most appropriate run level and to run only services you need. With that understanding, you'll be able to personalize your computer and cut down on the amount of time you spend repetitively typing the same commands.

### Understanding Shell Scripts

Have you ever had a task that you needed to do over and over that took a lot of typing on the command line? Do you ever think to yourself, “Wow, I wish there was just one command I could type to do all this of this”? Maybe a shell script is what you're after.

Shell scripts are the equivalent of batch files in MS-DOS, and can contain long lists of commands, complex flow control, arithmetic evaluations, user-defined variables, user-defined


5. Ben updates his Ubuntu system's packages using the `sudo apt-get upgrade` command, and now the Apache Web service is not working properly. What command should he run?

- A. `sudo apt-get clean`
- B. `sudo zypper clean -a`
- C. `sudo ldd /usr/sbin/apache2`
- D. `sudo rpm -aV`
- E. `sudo apt-get check`

6. Peter writes a new C++ application to use for managing his older Linux server. The new app contains no programming or logic errors. However, when he tries to compile it, it does not work. Which of the following is most likely the issue?

- A. An incorrect application permission
- B. An incorrect file permission
- C. A missing or outdated GCC
- D. A missing or outdated device
- E. A repository problem

7. Mary confirms via the `sealert` utility that her application cannot access the file `flash.txt`. What command should she use next?

- A. `ls -l flash.txt`
- B. `ls -Z flash.txt`
- C. `ls -l flash.txt -directory`
- D. `setroubleshoot`
- E. `restorecon`

8. A clock-in/out application, which uses an NTP server on the local network, is throwing an error concerning reaching the server. There are currently no network problems. Which of the following are steps in the troubleshooting process for this issue? (Choose all that apply.)

- A. Check the firewall ACLs on the NTP server.
- B. Check the firewall ACLs on the application server.
- C. Use the `firewall-cmd --get-default-zone` command.
- D. Check the `/etc/services` file for NTP ports and transport protocols.
- E. View firewall log entries.

9. Your system administrator team member Norman tells you the device located at the communications port is not working. What command should you issue to start the troubleshooting process?

- A. `dmesg | grep -i COM`
- B. `dmesg | grep -i ttys`
- C. `sudo setserial -a /dev/COM1`
- D. `sudo setserial -a /dev/ttyS0`
- E. `cat /proc/interrupts`

10. Harry’s newly installed USB printer is not working. The system employs CUPS. Which of the following are steps that may be included in the troubleshooting process? (Choose all that apply.)

- A. Issue the `less /etc/printcap` command.
- B. Use the `lpinfo -m` command to view available USB ports.
- C. Put a watch on the appropriate log file and plug in the USB cable.
- D. Use the `dmesg` and `grep` utilities to find printer information.
- E. Use the `lsusb -v` command to see if the device is on the USB bus.

## Automating Your System

PART VI

![](img/c0a399aca0d18f8822d714ad0a173123_762_0.png)

### Chapter 25

#### Deploying Bash Scripts

![](img/c0a399aca0d18f8822d714ad0a173123_764_0.png)

✓ Objective 3.1: Given a scenario, create simple shell scripts to automate common tasks

![](img/c0a399aca0d18f8822d714ad0a173123_765_0.png)

Linux system administrators often need to perform the same tasks over and over, such as checking available disk space on the system or creating user accounts. Instead of entering multiple commands every time, you can write scripts that run in the shell to do these tasks automatically for you. This chapter explores how Bash shell scripts work and demonstrates how you can write your own scripts to automate everyday activities on your Linux system.

## The Basics of Shell Scripting

*Shell scripting* allows you to write small programs that automate activities on your Linux system. Shell scripts can save you time by giving you the flexibility to quickly process data and generate reports that would be cumbersome to do by manually entering multiple commands at the command prompt. You can automate just about anything you do at the command prompt using shell scripts.

The following sections walk through the basics of what shell scripts are and how to get started writing them.

## Running Multiple Commands

So far in this book we’ve been entering a single command at the command prompt and viewing the results. One exciting feature of the Linux command line is that you can enter multiple commands on the same command line and Linux will process them all. Just place a semicolon between each command you enter:

```
$ date ; who
rICH    :0      2022-02-24  19:15 ( :0)
$ 
```

The Linux Bash shell runs the first command (*date*) and displays the output; then it runs the second command (*who*) and displays the output from that command immediately following the output from the first command. Although this may seem trivial, this is the basis of how shell scripts work.

## Redirecting Output

Another building block of shell scripting is the ability to store command output. Often, when you run a command, you'd like to save the output for future reference. To help with this, the Bash shell provides output redirection.

*Output redirection* allows us to redirect the output of a command from the monitor to another device, such as a file. This feature comes in handy when you need to log data from a shell script that runs after business hours, so you can see what the shell script did when it ran.

To redirect the output from a command, you use the greater-than symbol (> ) after the command and then specify the name of the file that you want to use to capture the redirected output. This is demonstrated in Listing 25.1.

**Listing 25.1: Redirecting output to a file**

```
$ date > today.txt
$ cat today.txt
Thu Feb 24 19:21:12 EST 2022
$
```

The example shown in Listing 25.1 redirects the output of the `date` command to the file named `today.txt`. Notice that when you redirect the output of a command, nothing displays on the monitor output. All of the text from the output is now in the file, as shown by using the `cat` command to display the file contents.

The greater-than output redirection operator automatically creates a new file for the output, even if the file already exists. If you prefer, you can append the output to an existing file by using the double greater-than symbol (>>), as shown in Listing 25.2.

**Listing 25.2: Appending command output to a file**

```
$ who >> today.txt
$ cat today.txt
Thu Feb 24 19:21:12 EST 2022
rich :0 2022-02-24 19:15 (:0)
$
```

The `today.txt` file now contains the output from the original `date` command in Listing 25.1 and the output from the `who` command ran in Listing 25.2.

![](img/c0a399aca0d18f8822d714ad0a173123_767_0.png)

In Linux, everything is a file, including the input and output processes of a command. Linux identifies files with a file descriptor, which is a non-negative integer. The Bash shell reserves the first three file descriptors for input and output. File descriptor 0 is called STDIN and points to the standard input for the shell, which is normally the keyboard. File descriptor 1 is called STDOUT, which points to the standard output for the shell, typically the monitor. This is where the standard output messages go. File descriptor 2 is called STDERR, which is where the shell sends messages identified as errors. By default, this points to the same device as the STDOUT file descriptor, the monitor. You can redirect only the errors from your shell script to a separate file from the normal output by using `>>` instead of the standard `>` output redirection character. This allows you to specify a separate file for monitoring error messages from commands.

Output redirection is a crucial feature in shell scripts. With it, we can generate log files from our scripts, giving us a chance to keep track of things as the script runs in background mode on the Linux system.

## Piping Data

While output redirection allows us to redirect command output to a file, *piping* allows us to redirect the output to another command. The second command uses the redirected output from the first command as input data. This feature comes in handy when using commands that process data, such as the `sort` command.

The piping symbol is the bar (\|) symbol, which usually appears above the backslash key on U.S. keyboards. Listing 25.3 shows an example of using piping.

**Listing 25.3: Piping command output to another command**

```
$ ls | sort
Desktop
Documents
Downloads
Music
Pictures
Public
Templates
test.txt
today.txt
Videos
$
```


nmap (short for network mapper) is a port-scanning tool that can rapidly scan large networks and determine what hosts are available on the network, what services they offer, what operating system (and operating-system version) they run, what type of packet filters or firewalls they use, and dozens of other characteristics. You can read more about nmap at http://nmap.org.

If nmap isn't already installed, you can easily install it on your distribution by using the command apt-get install nmap or the software search facility of YaST (find nmap) or any distribution-specific interface you may have.

If you want to try nmap to scan your local-area network, type a command similar to the following (replacing the IP address range with addresses that are appropriate for your network):

```
nmap -O -sS 192.168.0.4-8
```

Following is typical output from that command:

```
Starting nmap 7.60 (http://www.insecure.org/nmap/) at 2018-08-28 16:20 EDT
Interesting ports on 192.168.0.4:
(The 1659 ports scanned but not shown below are in state: closed)
PORT STATE SERVICE
21/tcp open ftp
22/tcp open ssh
111/tcp open rpcbind
631/tcp open ipp
MAC Address: 00:C0:49:63:78:3A (U.S. Robotics)
Device type: general purpose
Running: Linux 3.9.X|3.9.X|3.9.X
OS details: Linux 2.4.18 - 2.6.7
Uptime 9.919 days (since Thu Aug 18 18:18:15 2018)
Nmap finished: 5 IP addresses (5 hosts up) scanned in 30.846 seconds
```

As you can see, nmap displays the names of the open ports and hazards a guess at the operating-system name and version number.

For a quick scan of your own machine, you can use the IP address of 127.0.0.1 (see Figure 3-1). Ideally, the scan will verify that the ports are closed.

## FIGURE 3-1:
You can view any open ports with nmap.

![](img/322157d1fa7d965f05bcd68ed0ffc36b_443_0.png)

## 7 Scripting

## Contents at a Glance
- CHAPTER 1: Introductory Shell Scripting ................................ 431
  Trying Out Simple Shell Scripts ................................ 432
  Exploring the Basics of Shell Scripting ................................ 433

CHAPTER 2: Working with Advanced Shell Scripting ........ 443
  Trying Out sed ................................ 443
  Working with awk and sed ................................ 446
  Final Notes on Shell Scripting ................................ 450

CHAPTER 3: Programming in Linux ................................ 451
  An Overview of Programming ................................ 452
  Exploring the Software-Development Tools in Linux ........ 453
  Understanding the Implications of GNU Licenses ........... 473

## IN THIS CHAPTER
- » Trying some simple shell scripts
- » Discovering the basics of shell scripting
- » Exploring bash’s built-in commands

## Chapter 1
## Introductory Shell Scripting

As you've seen throughout many of the preceding chapters, Linux gives you a plethora of small and specialized commands, along with the ability to connect these commands in such a way that one command's output can be used as a second command's input. `bash` (short for Bourne-Again Shell) — the default shell in most Linux systems — provides this capability in the form of I/O redirection and pipes. `bash` also includes conditionals such as the `if` statement that you can use to run commands only when a specific condition is true and the `for` statement that can repeat the set of commands a specified number of times. You can use these features of `bash` when writing programs called *shell scripts*: task-oriented collections of shell commands stored in a file.

This chapter shows you how to write simple shell scripts, which are used to automate various tasks. When your Linux system boots, for example, many shell scripts stored in various subdirectories in the `/etc` directory (such as `/etc/init.d`) perform many initialization tasks.

## Trying Out Simple Shell Scripts

If you’re not a programmer, it’s common to feel apprehensive about programming. But you can put that apprehension aside: Shell scripting (or programming) can be as simple as storing a few commands in a file that can then be executed. In fact, you can have a useful shell program that has in it only a single command.

Shell scripts are popular among system administrators because they can be used to help automate tasks you perform often. If a hard drive seems to be getting full, for example, you may want to find all files that exceed some determined size (say, 5MB) and that have not been accessed in the past 30 days. Once the files are found, you may want to send an email message to all the users identified with those large files, requesting that they archive and clean up those files. You can perform all these tasks with a shell script. You might start with the following find command to identify large files:

```
find / -type f -atime +30 -size +5000k -exec ls -l {} \; > /tmp/largefiles
```

This command creates a file named /tmp/largefiles, which contains detailed information about old files taking up too much space. After you get a list of the files, you can use a few other Linux commands — such as sort, cut, and sed — to prepare and send mail messages to users who have large files to clean up. Instead of typing all these commands manually, place them in a file and create a shell script. That, in a nutshell, is the essence of shell scripts — to gather shell commands in a file so that you can easily perform repetitive system administration tasks. Although you could do all this on the command line without a script file, doing so would require you to type the command — complete with parameters and correct syntax — each and every time.

bash scripts, just like most Linux commands, accept command-line options. Inside the script, you can refer to the options as $1, $2, and so on. The special name $0 refers to the name of the script itself.

Here’s a typical bash script that accepts arguments:

```
#!/bin/sh
echo "This script's name is: $0"
echo Argument 1: $1
echo Argument 2: $2
```

The first line runs the /bin/sh program, which subsequently processes the rest of the lines in the script. The name /bin/sh traditionally refers to the Bourne shell — the first Unix shell. In most Linux systems, /bin/sh is a symbolic link to /bin/bash, which is the executable program for bash.

Save this simple script in a file named simple and make that file executable with the following command:

```
chmod +x simple
```

Now run the script as follows:

```
./simple
```

It displays the following output:

```
This script's name is: ./simple
Argument 1:
Argument 2:
```

The first line shows the script’s name. Because you have run the script without arguments, the script displays no values for the arguments.

Now try running the script with a few arguments, like this:

```
./simple "This is one argument" second-argument third
```

This time, the script displays more output:

```
This script's name is: ./simple
Argument 1: This is one argument
Argument 2: second-argument
```

As the output shows, the shell treats the entire string within the double quotation marks as a single argument. Otherwise, the shell uses spaces as separators between arguments on the command line.

This sample script ignores the third argument (and any others that you might give after it in subsequent attempts) because the script is designed to print only the first two arguments, and nothing references $3 or beyond.

## Exploring the Basics of Shell Scripting

Like any programming language, the bash shell supports the following features:

- » Variables that store values, including special built-in variables for accessing command-line arguments passed to a shell script and other special values.
- The capability to evaluate expressions.
- Control structures that enable you to loop over several shell commands or execute some commands conditionally.
- The capability to define functions that can be called in many places within a script. bash also includes many built-in commands that you can use in any script.

The next few sections illustrate some of these programming features through simple examples. (It's assumed that you're already running bash, in which case you can try the examples by typing them at the shell prompt in a terminal window. Otherwise, all you have to do is open a terminal window; bash runs and displays its prompt in that window.)

## Storing stuff

You define variables in bash just as you define environment variables. Thus, you may define a variable as follows:

```
count=12 # note no embedded spaces are allowed
```

To use a variable's value, prefix the variable's name with a dollar sign ($). $PATH, for example, is the value of the variable PATH. (This variable is the famous PATH environment variable that lists all the directories that bash searches when trying to locate an executable file.) To display the value of the variable count, use the following command:

```
echo $count
```

bash has some special variables for accessing command-line arguments. As I mention earlier in this chapter, in a shell script, $0 refers to the name of the shell script. The variables $1, $2, and so on refer to the command-line arguments. The variable $* stores all the command-line arguments as a single variable, and $? contains the exit status of the last command the shell executes.

From a bash script, you can prompt the user for input and use the read command to read the input into a variable. Here's an example:

```
echo -n "Enter a value: "
read value
echo "You entered: $value"
```

When this script runs, the read value command causes bash to read whatever is typed in at the keyboard and store that input in the variable called value.

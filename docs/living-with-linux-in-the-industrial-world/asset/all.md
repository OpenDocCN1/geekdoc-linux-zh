![](Images/cover.jpg)

![Cover](Images/cover.jpg)

## **Contents**

[About the Author](../Text/body.xhtml)

[Foreword](../Text/body1.xhtml)

[Linux Commands Overview](../Text/body2.xhtml)

[Linux Commands List](../Text/body3.xhtml)

[HTOP Tool](../Text/body4.xhtml)

[What is Shell Scripting?](../Text/body5.xhtml)

[What is CronTab?](../Text/body6.xhtml)

[CronTab Usage and Format](../Text/body7.xhtml)

[Overview on Port Checking](../Text/body8.xhtml)

[IFTOP](../Text/body9.xhtml)

[ARP-SCAN](../Text/body10.xhtml)

[RKHUNTER](../Text/body11.xhtml)

[Overview of SSL Certificates](../Text/body12.xhtml)

[Concept and Usage of SSL](../Text/body13.xhtml)

[Types of Encryption Algorithm](../Text/body14.xhtml)

[Symmetric Sample Commands](../Text/body15.xhtml)

[DSA Sample Commands](../Text/body16.xhtml)

[RSA Sample Commands](../Text/body17.xhtml)

[Open SSL Certificates](../Text/body18.xhtml)

[What is SSL and TLS?](../Text/body19.xhtml)

[What is an X.509 Certificate?](../Text/body20.xhtml)

[Commands to Generate Certificates](../Text/body21.xhtml)

[Concept of Sniffing](../Text/body22.xhtml)

[Install and Command Usage for Wireshark](../Text/body23.xhtml)

[Overview of IPV6 vs IPV4](../Text/body24.xhtml)

[Recognizing Types of IPV6 Addresses](../Text/body25.xhtml)

[Resources](../Text/body26.xhtml)

About the Author

![ ](Images/author.png)

Mr Elaiya Iswera Lallan has been in the IT Industry for the past 12 years.He is Managing Director of Blue Micro Solutions ,which is based in SIRIM Bhd(Governmnet agency) .

Mr Lallan has extensive experience in the IT industry.He has recieved an award as a Federal Territory Entrepreneur.After obtaining his Bachelor Degree in Computers and Electronics Engineering from Kolej Bandar Utama (twinning program with University of Nottingham) year 2001,he joined the company called MIR as a Information Technology Consultant .

He was performing computer programming tasks,and then joined as a software engineer in a new company called Neural Manufacturing Sdn Bhd.He had his best of experiences here when he was creating software technologies for the company’s flagship product called e-Jari,which is a biometric security device.He created an enterprise time attendance system for this device that can be used by other companies ranging from SMEs to government offices. Some of the companies using this time attendance system are PejabatTanah & Galian in Kuala Lumpur, Koperasi Malaysia, Bernama and ITIS. He also created a Guard Patrol and Intruder Detection System using the e-Jari, and was involved in the ISO9000:2001certification for the company.With his extensive working experience and good track record of able to handle mega IT projects in government sector, Mr Lallan managed to join the incubatorship program under SIRIM Bhd in February 2010\. With this Mr Lallan moved Blue Micro Solutions’ operations into the SIRIM building. He obtained certification from Ministry of Finance in Malaysia in the software fields where he can participate in tenders for government IT projects. He also started employing staffs to do IT projects and ventured into IT trainings in private corporations, government institutions and polytechnics, such as SKALI Bhd, Kolej Komuniti in Klang, Politeknik Ungku Omar in Ipoh and Politeknik Kuching in Sarawak. He has made Blue Micro Solutions to be a certified Human Resource Development Funds (HRDF) training provider to companies in Malaysia. With his proven track record in both the industrial and education worlds in IT, Mr Lallan has been awarded collaboration with Open University Malaysia (OUM) to offer affordable IT degree program to the public recently. Currently Mr Lallan is pursuing MSC status for his company Blue Micro Solutions.

With his company Blue Micro Solutions growing in the right directions, Mr Lallan began to explore his opportunities to grow his business in overseas as well. Venturing into Canada, he successfully opened a branch called Blue Micro Canada Incorporated. He also successfully registered the company with the Canadian government in Toronto, whereby he received invitations

to participate in the government tenders for IT projects. He also saw the opportunity to conduct IT trainings over the internet through webinars. He obtained license from Adobe USA to use its tool Adobe Connect to conduct webinars in Canada and United States of America.

Foreword

This book is an introduction to writing Linux shell scripts and installation of certain important tools for industry usage.

Topics included are the use of commands and shortcuts in shell scripting, monitoring of memory and CPU usages, SSL implementation, packet tracing and webservers in linux environment.

This book was written based on real life industrial experience and practical usage. Plus before this book was produced a several advance linux trainings have been conducted by our experience linux practitioners to several organizations.

Chapter 1: Linux Basic Commands

The following commands are for new users or for beginners only. The purpose is you will become more familiar with your shell scripting and secondly, you need some of these command in your Shell script.

$ date --help

To see help or options related with ls command (Here you will screen by screen help, since help of ls command is quite big that can't fit on single screen )

$ ls --help | more

Syntax: command-name --help

Syntax: man command-name

Syntax: info command-name

See what happened when you type following

$ man ls

$ info bash

Linux Commands List

ls

list files and directories

ls -a

list all files and directories

mkdir

make a directory

cd directory

change to named directory

cd

change to home-directory

cd ~

change to home-directory

cd ..

change to parent directory

pwd

display the path of the current directory

cp file1 file2

copy file1 and call it file2

mv file1 file2

move or rename file1 to file2

rm file

remove a file

rmdir directory

remove a directory

cat file

display a file

less file

display a file a page at a time

head file

display the first few lines of a file

tail file

display the last few lines of a file

grep 'keyword' file

search a file for keywords

wc file

count number of lines/words/characters in file

command > file

redirect standard output to a file

command >> file

append standard output to a file

command < file

redirect standard input from a file

command1 | command2

pipe the output of command1 to the input of command2

cat file1 file2 > file0

concatenate file1 and file2 to file0

sort

sort data

who

list users currently logged in

HTOP Tool

This is htop, an interactive process viewer for Linux. It is a text-mode application (for console or X terminals) and requires ncurses.

![ ](Images/ClipboardImage_htop.png)

Comparison between htop and top

*   In 'htop' you can scroll the list vertically and horizontally to see all processes and complete command lines.
*   In 'top' you are subject to a delay for each

unassigned key you press (especially annoying when multi-key escape sequences are triggered by accident).

'htop' starts faster ('top' seems to collect data for a while before displaying anything).

In 'htop' you don't need to type the process number to kill a process, in 'top' you do.

In 'htop' you don't need to type the process number or the priority value to renice a process, in 'top' you do.

'htop' supports mouse operation, 'top' doesn't

'top' is older, hence, more used and tested.

You can interact with the htop using mouse. You can scroll vertically to view the full process list, and scroll horizontally to view the full command line of the process.

Installation command for HTOP tool:

wget http://packages.sw.be/rpmforge-release/rpmforge-

release-0.5.2-2.el5.rf.i386.rpm

rpm -Uhv rpmforge-release*.rf.i386.rpm

Chapter 2: Shell Scripting

Normally shells are interactive. It means shell accept command from user and execute them. But if user uses command one by one, then user can store this sequence of command to text file and tell the shell to execute this text file instead of entering the commands. This is known as shell script.

1\. Writing scripts and executing them

2\. Basic commands

3\. Shortcuts

Understanding Linux Kernel

Kernel is the main heart of Linux O/S. It handles resources of Linux O/S. The resources means are facilities available in Linux. For eg. Facility to store data, print data on printer,

memory, file management etc . Kernel allocates who will use this resource, for how long and when. It executes your programs and it's memory resident portion of Linux. It performance the following task:-

1) I/O management

2) Process management

3) Device management

4) File management

5) Memory management

Understanding Linux Shell

Computer understand the language of 0's and 1's called binary language, In early days of computing, instruction are provided using binary language, which is difficult for all of us, to read and write. So in O/s there is special program called Shell. Shell accepts your instruction or commands in English and translate it into computers native binary language.

You type your command and shell will convert it as it's environment provided for user interaction. Shell is an command language interpreter that executes commands read from the standard input device (keyboard) or from a file. Linux may use one of the following most popular shells (In MS-DOS, Shell name is COMMAND.COM which is also used for same purpose, but it's not as powerful as our Linux Shells are!)

How to Run Shell Scripts

Because of security of files, in Linux, the creator of Shell Script does not get execution permission by default. So if we wish to run shell script we have to do two things as follows:-

(1) Use chmod command as follows to give execution permission to our script

Syntax: chmod +x shell-script-name

OR Syntax: chmod 777 shell-script-name

(2) Run our script as

Syntax: ./your-shell-program-name

For e.g.

$ ./first

Here '.'(dot) is command, and used in conjunction with shell script. The dot(.) indicates to current shell that the command following the dot(.) has to be executed in the same shell i.e. without the loading of another shell in memory. Or you can also try following syntax to run Shell Script

Syntax: bash &nbsh;&nbsh; your-shell-program-name

OR /bin/sh &nbsh;&nbsh; your-shell-program-name

For e.g.

$ bash first

$ /bin/sh first

Note that to run script, you need to have in same directory where you created your script, if you are in different directory your script will not run (because of path settings), For eg. Your home directory is ( use $ pwd to see current working directory) /home/vivek. Then you created one script called 'first', after creation of this script you moved to some other directory lets say /home/vivek/Letters/Personal, Now if you try to execute your script it will not run, since script 'first' is in /home/vivek directory, to Overcome this problem there are two ways First, specify complete path of your script when ever you want to run it from other directories like giving following command

$ /bin/sh /home/vivek/first

Commands Related with Shell

(1) echo [options] [string, variables...]

Displays text or variables value on screen.

Options

-n Do not output the trailing new line.

-e Enable interpretation of the following backslash escaped characters in the strings:

\a alert (bell)

\b backspace

\c suppress trailing new line

\n new line

\r carriage return

\t horizontal tab

\\ backslash

For eg. $ echo -e "An apple a day keeps away \a\t\tdoctor\n"

(2) More about Quotes

There are three types of quotes

" i.e. Double Quotes

' i.e. Single quotes

` i.e. Back quote

1."Double Quotes" - Anything enclose in double quotes removed meaning of that characters (except

\ and $).

2\. 'Single quotes' - Enclosed in single quotes remains unchanged.

3\. `Back quote` - To execute command.

For eg.

$ echo "Today is date"

Can't print message with today's date.

$ echo "Today is `date`".

Now it will print today's date as, Today is Tue Jan ....,See the `date` statement uses back quote, (See also Shell Arithmetic NOTE).

(3) Shell Arithmetic

Linux Shell Script Tutorial

http://www.freeos.com/guides/lsst/shellprog.htm (5 of 19) [17/08/2001 17.42.21]

Use to perform arithmetic operations For e.g.

$ expr 1 + 3

$ expr 2 - 1

$ expr 10 / 2

$ expr 20 % 3 # remainder read as 20 mod 3 and remainder is 2)

$ expr 10 \* 3 # Multiplication use \* not * since its wild card)

$ echo `expr 6 + 3`

For the last statement not the following points

1) First, before expr keyword we used ` (back quote) sign not the (single quote i.e. ') sign. Back quote is generally found on the key under tilde (~) on PC keyboards OR To the above of TAB key.

2) Second, expr is also end with ` i.e. back quote.

3) Here expr 6 + 3 is evaluated to 9, then echo command prints 9 as sum

4) Here if you use double quote or single quote, it will NOT work, For eg.

$ echo "expr 6 + 3" # It will print expr 6 + 3

$ echo 'expr 6 + 3'

Local and Global Shell Variable

Normally all our variables are local. Local variable can be used in same shell, if you load another copy of shell (by typing the /bin/bash at the $ prompt) then new shell ignored all old shell's variable. For e.g.

Consider following example

$ vech=Bus

$ echo $vech

Bus

$ /bin/bash

$ echo $vech

NOTE:-Empty line printed

$ vech=Car

$ echo $vech

Car

$ exit

$ echo $vech

We can copy old shell's variable to new shell (i.e. first shells variable to seconds shell), such variable is know as Global Shell variable. To do this use export command

Syntax: export variable1, variable2,.....variableN

For e.g.

$ vech=Bus

$ echo $vech

Bus

$ export vech

$ /bin/bash

$ echo $vech

Bus

$ exit

$ echo $vech

Operators

Type bc at $ prompt to start Linux calculator program

$ bc

After this command bc is started and waiting for you commands, i.e. give it some calculation as follows type 5 + 2 as

5 + 2

7

7 is response of bc i.e. addition of 5 + 2 you can even try

5 - 2

5 / 2

Now what happened if you type 5 > 2 as follows

5 > 2

0

0 (Zero) is response of bc, How? Here it compare 5 with 2 as, Is 5 is greater then 2, (If I ask same question to you, your answer will be YES) In Linux (bc) gives this 'YES' answer by showing 0 (Zero) value. It means when ever there is any type of comparison in Linux Shell It gives only two answer one is YES and NO is other.

To preserve sanity it is better to use only "double round bracket comparison" without using dollar sign prefix before variables. This flavor of the "double round bracket" construct is supported in bash and all implementations of ksh in major Unixes so it is perfectly portable. Here is short summary of operators for "double round bracket comparison"

*   < is less than (within double parentheses). For example, (( a < b ))

*   <= is less than or equal to (within double parentheses) (( a <= b ))

*   > is greater than (within double parentheses)(( a > b ))

*   >= is greater than or equal to (within double parentheses) (( a >= b ))

Decision Statements

If you use bash for scripting you will undoubtedly have to use decision statements a lot, for example for an if ... then construct or a while loop. The syntax of these conditions can seem a bit daunting to learn and use. This tutorial aims to help you understanding conditions in bash, and provides a comprehensive list of the possibilities. A small amount of general shell knowledge is assumed.

While Loop Statements

While Loop is executed as long as given condition is true. For eg. Above for loop program can be written using while loop as

while [ condition ]

do

command1

command2

command3

..

....

done

Type the script below at Linux shell terminal

$cat > nt1

#!/bin/sh

#

#Script to test while statement

##

if [ $# -eq 0 ]

then

echo "Error - Number missing form command line argument"

echo "Syntax : $0 number"

echo " Use to print multiplication table for given number"

exit 1

fi

n=$1

i=1

while [ $i -le 10 ]

do

echo "$n * $i = `expr $i \* $n`"

i=`expr $i + 1`

done

Save it and try as

$ chmod +x nt1

$./nt1 7

Case Statements

The case statement is good alternative to Multilevel if-then-else-fi statement. It enable you to match several values against one variable. Its easier to read and write.

Syntax:

case $variable-name in

pattern1) command

...

..

command;;

pattern2) command

...

..

command;;

patternN) command

...

..

command;;

*) command

...

..

command;;

esac

The $variable-name is compared against the patterns until a match is found. The shell then executes all the statements up to the two semicolons that are next to each other. The default is *) and its executed if no match is found. For eg. Create script as follows

$ cat > car

#

# if no vehicle name is given

# i.e. -z $1 is defined and it is NULL

#

# if no command line arg

if [ -z $1 ]

then

rental="*** Unknown vehicle ***"

elif [ -n $1 ]

then

# otherwise make first arg as rental

rental=$1

fi

case $rental in

"car") echo "For $rental Rs.20 per k/m";;

"van") echo "For $rental Rs.10 per k/m";;

"jeep") echo "For $rental Rs.5 per k/m";;

"bicycle") echo "For $rental 20 paisa per k/m";;

*) echo "Sorry, I can not gat a $rental for you";;

esac

Save it by pressing CTRL+D

$ chmod +x car

$ car van

$ car car

$ car Maruti-800

If Statements

Now you will see, if condition which is used for decision making in shell script, If given condition is true then command1 is executed.

Syntax:

if condition

then

command1 if condition is true or if exit status

of condition is 0 (zero)

...

...

fi

Here condition is nothing but comparison between two values, for compression we can use test or [expr ] statements or even exist status can be also used. An expression is nothing but combination of values, relational operator (such as >,<, <> etc) and mathematical operators (such as +, -, / etc ).

Following are all examples of expression:

5 > 2

3 + 6

3 * 65

a < b

c > 5

c > 5 + 30 -1

Type following command (assumes you have file called foo)

$ cat foo

$ echo $?

The cat command return zero(0) on successful, this can be used in if condition as follows, Write shell script as:

$ cat > showfile

#!/bin/sh

#

#Script to print file

#

if cat $1

then

echo -e "\n\nFile $1, found and successfully echoed"

fi

Now run it.

$ chmod +x showfile

$./showfile foo

Here

$ ./showfile foo

Conditional Execution

The control operators are && (read as AND) and || (read as OR). An AND list has the

Syntax: command1 && command2

Here command2 is executed if, and only if, command1 returns an exit status of zero. An OR list has the

Syntax: command1 || command2

Here command2 is executed if and only if command1 returns a non-zero exit status. You can use both as follows

command1 && comamnd2 if exist status is zero || command3 if exit status is non-zero

Here if command1 is executed successfully then shell will run command2 and if command1 is not successful then command3 is executed. For e.g.

$ rm myf && echo File is removed successfully || echo File is not removed

If file (myf) is removed successful (exist status is zero) then "echo File is removed successfully" statement is executed, otherwise "echo File is not removed" statement is executed (since exist status is non-zero)

I/O Redirection and FIle Descriptors

As you know I/O redirectors are used to send output of command to file or to read input from file. (See Input/Output redirection). Now consider following examples

$ cat > myf

This is my file

^D

Above command send output of cat command to myf file

$ cal

Above command prints calendar on screen, but if you wish to store this calendar to file then give

command

$ cal > mycal

Here sort command takes input from keyboard and then sorts the number, If we wish to take input from file give command as follows

$ cat > nos

10

-20

11

2

^D

$ sort < nos

-20

2

10

11

First we have created the file nos, then we have taken input from this file and sort command prints sorted numbers. This is called input redirection.

User Interface and Dialog Utility

Good program/shell script must interact with users. There are two ways to this one is use command line to script when you want input, second use statement like echo and read to read input into variable from the prompt. For e.g. Write script as

$ cat > userinte

#

# Script to demo echo and read command for user interaction

#

echo "Your good name please :"

read na

echo "Your age please :"

read age

neyr=`expr $age + 1`

echo "Hello $na, next year you will be $neyr yrs old."

Save it and run as

$ chmod +x userinte

$ ./userinte

Your good name please :

Vivek

Your age please :

25

Hello Vivek, next year you will be 26 yrs old.

User interface usually includes, menus, different type of boxes like info box, message box, Input box etc. In Linux shell there is no built-in facility available to create such user interface, But there is one utility supplied with Red Hat Linux version 6.0 called dialog, which is used to create different type of boxes like info box, message box, menu box, Input box etc. Now try dialog utility as follows :

$ cat > dia1

dialog --title "Linux Dialog Utility Infobox" --backtitle "Linux Shell Script\

Tutorial" --infobox "This is dialog box called infobox, which is used\

to show some information on screen, Thanks to Savio Lam and\

Stuart Herbert to give us this utility. Press any key. . . " 7 50 ; read

Save the shell script and run as

$ chmod +x dia1

$ ./dia1

Chapter 3: Task Automation

CronTab is a Linux system process that will execute a program at a preset time. To use cron the user must prepare a text file that describes the program that you want executed and the times that cron should execute them.

*   What is a cron job?

*   How to create a cron job?

*   Executing cron job command

*   Testing the cron job scripts

Linux Crontab Format

MIN HOUR DOM MON DOW CMD

Table: Crontab Fields and Allowed Ranges (Linux Crontab Syntax)

| Field | Description | Allowed Value |
| MIN | Minute field | 0 to 59 |
| HOUR | Hour field | 0 to 23 |
| DOM | Day of Month | 1-31 |
| MON | Month field | 1-12 |
| DOW | Day Of Week | 0-6 |
| CMD | Command | Any command to be executed. |

Scheduling a Job For a Specific Time

The basic usage of cron is to execute a job in a specific time as shown below. This will execute the Full backup shell script (full-backup) on 10th June 08:30 AM.

Please note that the time field uses 24 hours format. So, for 8 AM use 8, and for 8 PM use 20.30 08 10 06 * /home/ramesh/full-backup

30 – 30th Minute

08 – 08 AM

10 – 10th Day

06 – 6th Month (June)

* – Every day of the week

Schedule a Job For More Than One Instance (e.g. Twice a Day)

The following script take a incremental backup twice a day every day. This example executes the specified incremental backup shell script (incremental-backup) at 11:00 and 16:00 on every day. The comma separated value in a field specifies that the command needs to be executed in all the mentioned time.

00 11,16 * * * /home/ramesh/bin/incremental-backup

00 – 0th Minute (Top of the hour)

11,16 – 11 AM and 4 PM

* – Every day

* – Every month

* – Every day of the week

Schedule a Job for Specific Range of Time (e.g. Only on Weekdays)

If you wanted a job to be scheduled for every hour with in a specific range of time then use the following.

Cron Job everyday during working hours

This example checks the status of the database everyday (including weekends) during the working hours 9 a.m – 6 p.m

00 09-18 * * * /home/ramesh/bin/check-db-status

00 – 0th Minute (Top of the hour)

09-18 – 9 am, 10 am,11 am, 12 am, 1 pm, 2 pm, 3 pm, 4 pm, 5 pm, 6 pm

* – Every day

* – Every month

* – Every day of the week

Cron Job every weekday during working hours

This example checks the status of the database every weekday (i.e excluding Sat and Sun) during the working hours 9 a.m – 6 p.m.

00 09-18 * * 1-5 /home/ramesh/bin/check-db-status

00 – 0th Minute (Top of the hour)

09-18 – 9 am, 10 am,11 am, 12 am, 1 pm, 2 pm, 3 pm, 4 pm, 5 pm, 6 pm

* – Every day

* – Every month

1-5 -Mon, Tue, Wed, Thu and Fri (Every Weekday)

How to View Crontab Entries?

View Current Logged-In User’s Crontab entries

To view your crontab entries type crontab -l from your linux shell terminal as shown below.

Chapter 4: Port Checking

Linux has a lot of tools to check which ports are open, the most common is nmap which is a command line tool, but also exist a Graphical frontEnd for it if the user prefer that way.

1)Basic understanding of TCP and UDP protocol

2)Techniques to find out which process uses which port number, directory, owner, etc

3)Overview of rootkits to find out the processes that are really running

Understanding of TCP and UDP Ports

As you know every computer or device on the Internet must have a unique number assigned to it called the IP address. This IP address is used to recognize your particular computer out of the millions of other computers connected to the Internet. When information is sent over the Internet to your computer how does your computer accept that information? It accepts that information by using TCP or UDP ports.

An easy way to understand ports is to imagine your IP address is a cable box and the ports are the different channels on that cable box. The cable company knows how to send cable to your cable box based upon a unique serial number associated with that box (IP Address), and then you receive the individual shows on different channels (Ports).

Ports work the same way. You have an IP address, and then many ports on that IP address. You can have a total of 65,535 TCP Ports and another 65,535 UDP ports. When a program on your computer sends or receives data over the Internet it sends that data to an ip address and a specific port on the remote computer, and receives the data on a usually random port on its own computer. If it uses the TCP protocol to send and receive the data then it will connect and bind itself to a TCP port. If it uses the UDP protocol to send and receive data, it will use a UDP port. Figure 1, below, is a represenation of an IP address split into its many TCP and UDP ports. Note that once an application binds itself to a particular port, that port can not be used by any other application. It is first come, first served.

Network Mapper(NMAP)

NMAP ("Network Mapper") is a free and open source (license) utility for network discovery and security auditing. Many systems and network administrators also find it useful for tasks such as network inventory, managing service upgrade schedules, and monitoring host or service uptime. NMAP uses raw IP packets in novel ways to determine what hosts are available on the network, what services (application name and version) those hosts are offering, what operating systems (and OS versions) they are running, what type of packet filters/firewalls are in use, and dozens of other characteristics. It was designed to rapidly scan large networks, but works fine against single hosts. NMAP runs on all major computer operating systems, and official binary packages are available for Linux, Windows, and Mac OS X.

Installation steps for NMAP

1) Install libpcap library

wget http://www.tcpdump.org/release/libpcap-0.9.4.tar.gz

./configure --prefix=/usr && make

make install &&

What is libpcap?

Monitoring software may use libpcap to capture packets travelling over a network and, in newer versions, to transmit packets on a network at the link layer, as well as to get a list of network interfaces for possible use with libpcap.

2) Install NMAP and command usage

rpm -vhU http://nmap.org/dist/nmap-4.68-1.i386.rpm

nmap -sS 127.0.0.1

Type of NMAP Scan Commands

-sS (TCP SYN scan)

-sT (TCP connect scan)

-sU (UDP scans)

-sY (SCTP INIT scan)

-sN; -sF; -sX (TCP NULL, FIN, and Xmas scans)

-sA (TCP ACK scan)

-sW (TCP Window scan)

-sM (TCP Maimon scan)

-sZ (SCTP COOKIE ECHO scan)

-sI <zombie host>[:<probeport>] (idle scan)

-sO (IP protocol scan)

-b <FTP relay host> (FTP bounce scan)

Sample Output from NMAP Tool

[root]# nmap -sS 127.0.0.1

Starting Nmap 4.01 at 2006-07-06 17:23 BST

Interesting ports on chaos (127.0.0.1):

(The 1668 ports scanned but not shown below are in state: closed)

PORT STATE SERVICE

21/tcp open ftp

22/tcp open ssh

631/tcp open ipp

6000/tcp open X11

IFTOP

IFTOP listens to network traffic on a named interface, or on the first interface it can find which looks like an external interface if none is specified, and displays a table of current bandwidth usage by pairs of hosts. IFTOP must be run with sufficient permissions to monitor all network traffic on the interface.

By default, IFTOP will look up the hostnames associated with addresses it finds in packets. This can cause substantial traffic of itself, and may result in a confusing display. You may wish to suppress display of DNS traffic by using filter code such as not port domain, or switch it off entirely, by using the -n option or by pressing n when the program is running.

By default, IFTOP counts all IP packets that pass through the filter, and the direction of the packet is determined according to the direction the packet is moving across the interface. Using the -F option it is possible to get IFTOP to show packets entering and leaving a given network. For example, iftop -F 10.0.0.0/255.0.0.0 will analyze packets flowing in and out of the 10.* network.

Installation steps for IFTOP

$ wget http://packages.sw.be/rpmforge-release/rpmforge-release-0.5.2-2.el5.rf.i386.rpm (32-bit system)

$ sudo rpm -ivh rpmforge-release-0.5.2-2.el5.rf.i386.rpm

$ sudo yum install iftop

If you would like to build and install the latest version of iftop manually, do the following.

$ yum -y install ncurses-devel libpcap-devel

$ wget http://www.ex-parrot.com/~pdw/iftop/download/iftop-0.17.tar.gz

$ tar xvfvz iftop-0.17.tar.gz

$ cd iftop-0.17

$ ./configure

$ make

$ sudo make install

Just type iftop at your terminal.

Sample Output from IFTOP

![ ](Images/ClipboardImage1.png)

ARP -SCAN

arp-scan is a command-line tool for system discovery and fingerprinting. It constructs and sends ARP requests to the specified IP addresses, and displays any responses that are received. arp-scan allows you to:

*   Send ARP packets to any number of destination hosts, using a configurable output bandwidth or packet rate. This is useful for system discovery, where you may need to scan large address spaces.

*   Construct the outgoing ARP packet in a flexible way.arp-scan gives control of all of the fields in the ARP packet and the fields in the Ethernet frame header.

*   Decode and display any returned packets.arp-scan will decode and display any received ARP packets and lookup the vendor using the MAC address.

*   Fingerprint IP hosts using the arp-fingerprint tool.

Installation steps for ARP-SCAN

Type the commands below at Linux terminal:

wget http://www.nta-monitor.com/files/arp-scan/arp-scan-1.8.tar.gz

./configure

make install

Finally execute the arp-scan tool by typing the below:

arp-scan --interface=eth1 192.168.1.0/24

Sample Output from ARP-SCAN

![ ](Images/ClipboardImage2.png)

CHKROOTKIT

The chkrootkit security scanner searches the local system for signs that it is infected with a 'rootkit'. Rootkits are set of programs and hacks designed to take control of a target machine by using known security flaws.

Please note that chkrootkit detects no intrusions, this does not guarantee that the system is uncompromised. In addition to running chkrootkit, more specific tests should always be performed.

Installation steps for CHKROOTKIT

Type the commands below at Linux terminal:

sudo yum install chkrootkit

Finally execute the arp-scan tool by typing the below:

chkrootkit -x | less- Look for suspicious strings

sudo chkrootkit -p /mnt/safe

Sample Output from CHKROOTKIT

![ ](Images/ClipboardImage3.png)

RKHUNTER

RKHunter is a shell script which carries out various checks on the local system to try and detect known rootkits and malware. It also performs checks to see if commands have been modified, if the system startup files have been modified, and various checks on the network interfaces, including checks for listening applications.

Installation steps for RKHUNTER

Type the commands below at Linux terminal:

sudo yum install rkhunter

Finally execute the arp-scan tool by typing the below:

sudo rkhunter --check

Sample Output from RKHUNTER

![ ](Images/ClipboardImage4.png)

Chapter 5: Handling of SSL Certificates

OpenSSL for TLS/SSL usage and implementations. The OpenSSL ssl library implements the Secure Sockets Layer (SSL v2/v3) and Transport Layer Security (TLS v1) protocols.

*   What is SSL and TLS?

*   Installing OpenSSL packages in Linux

*   General OpenSSL Commands

These commands allow to generate CSRs, Certificates,

Private Keys and do other miscellaneous tasks.

1)Checking Using Open SSL

Use these commands, if the need to check the information within a Certificate, CSR or Private Key and It can also check CSRs and check certificates using online tools.

2)Debugging Using OpenSSL

If an error is received that the private key doesn't match the certificate or

that a certificate that is installed to a site is not trusted, use these open ssl

commands to debug.

What OpenSSL ?

OpenSSL is a cryptography toolkit implementing the Secure Sockets Layer (SSL v2/v3) and Transport Layer Security (TLS v1) network protocols and related cryptography standards required by them.

OpenSSL Usage

*   Creation and management of private keys,public keys and parameters

*   Public key cryptographic operations

*   Creation of X.509 certificates, CSRs and CRLs

*   Encryption and Decryption with Ciphers

*   SSL/TLS Client and Server Tests

Types of Encryption Algorithm

AES

AES has been adopted by the U.S. government and is now used worldwide. It supersedes the Data Encryption Standard (DES). The algorithm described by AES is a symmetric-key algorithm, meaning the same key is used for both encrypting and decrypting the data.

DSA

The DSA is used by a signatory to generate a digital signature on data and by a verifier to verify the authenticity of the signature. Each signatory has a public and private key. The private key is used in the signature generation process and the public key is used in the signature verification process. For both signature generation and verification, the data (which is referred to as a message) is reduced by means of the Secure Hash Algorithm (SHA)

RSA

RSA involves a public key and a private key. The public key can be known to everyone and is used for encrypting messages. Messages encrypted with the public key can only be decrypted using the private key.

What is Symmetric Key Encryption?

Symmetric-key algorithms are a class of algorithms for cryptography that use the same cryptographic keys for both encryption of plaintext and decryption of ciphertext.

Below is the diagram of Symmetric-key encryption:

![ ](Images/ClipboardImage.png)

Symmetric Sample Commands

Installation commands for Open SSL tool

wget http://www.openssl.org/source/openssl-fips-ecp-2.0.1.tar.gz

./config

make

make install

Note:Dont have to repeat the steps above if you have OpenSSL tool installed.

For symmetic encryption, you can type the following command at the Linux Terminal

To encrypt:

openssl aes-256-cbc -salt -a -e -in plaintext.txt -out encrypted.txt

To decrypt this, you can use the following.

openssl aes-256-cbc -salt -a -d -in encrypted.txt -out plaintext.txt

What is Asymmetric Key Encryption

In an asymmetric key encryption scheme, anyone can encrypt messages using the public key, but only the holder of the paired private key can decrypt. Security depends on the secrecy of the private key.

Below is the diagram of asymmetric key encryption:

![ ](Images/ClipboardImage_ssl1.png)

DSA SAmple Commands

Installation commands for Open SSL tool

wget http://www.openssl.org/source/openssl-fips-ecp-2.0.1.tar.gz

./config

make

make install

Note:Dont have to repeat the steps above if you have OpenSSL tool installed.

Now, for Asymmetric encryption you must first generate your private key and extract the public key. The below commands are utilizing DSA concepts of encryption.

openssl dsaparam 1024 < /dev/random > dsaparam.pem

Generate private key:

openssl gendsa dsaparam.pem -out dsa_priv.pem

Generate public key:

openssl dsa -in dsa_priv.pem -pubout -out dsa_pub.pem

Insert text into foo.txt:

echo "foobar" > foo.txt

Encrypt the foo.txt:

sha1sum < foo.txt | awk '{print $1}' > foo.sha1

Generate signature file:

openssl dgst -dss1 -sign dsa_priv.pem foo.sha1 > sigfile.bin

Verify the signature file:

openssl dgst -dss1 -verify dsa_pub.pem -signature sigfile.bin foo.sha1

DSA Signing Procedure

![ ](Images/ClipboardImage_ssl5.png)

RSA Sample Commands

Installation commands for Open SSL tool

wget http://www.openssl.org/source/openssl-fips-ecp-2.0.1.tar.gz

./config

make

make install

Note:Dont have to repeat the steps above if you have OpenSSL tool installed.

Now, for Asymmetric encryption you must first generate your private key and extract the public key. The below commands are utilizing RSA concepts of encryption.

openssl genrsa -des3 -out private123.key 4096

openssl rsa private123.key -pubout > public123.key

openssl genrsa -out mykey.pem 4096

openssl rsa -in mykey.pem -pubout > mykey.pub

Once the private and public key is generated, then only the encryption and decryption command can be utilized.

To encrypt:

openssl rsautl -encrypt -pubin -inkey mykey.pub -in plaintext.txt -out encrypted.txt

To decrypt:

openssl rsautl -decrypt -inkey mykey.pem -in encrypted.txt -out plaintext1.txt

What is OpenSSL Tool?

The OpenSSL Project is a collaborative effort to develop a robust, commercial-grade, full-featured, and Open Source toolkit implementing the Secure Sockets Layer (SSL v2/v3) and Transport Layer Security (TLS v1) protocols as well as a full-strength general purpose cryptography library. The project is managed by a worldwide community of volunteers that use the Internet to communicate, plan, and develop the OpenSSL toolkit and its related documentation.

Below is the Open SSL diagram for certificate management:

![ ](Images/ClipboardImage_ssl2.png)

What is SSL and TLS?

SSL (Secure Sockets Layer) is the standard security technology for establishing an encrypted link between a web server and a browser. This link ensures that all data passed between the web server and browsers remain private and integral. SSL is an industry standard and is used by millions of websites in the protection of their online transactions with their customers.

To be able to create an SSL connection a web server requires an SSL Certificate. When you choose to activate SSL on your web server you will be prompted to complete a number of questions about the identity of your website and your company. Your web server then creates two cryptographic keys which known as Private Key and Public Key.

Differences between TLS and SSL

Although there are some slight differences between SSL 3.0 and TLS 1.0, this reference refers to the protocol as TLS/SSL.

Note

Although their differences are minor, TLS 1.0 and SSL 3.0 are not interchangeable. If the same protocol is not supported by both parties, the parties must negotiate a common protocol to communicate successfully.

TLS Structure Diagram

![ ](Images/ClipboardImage_ssl3.png)

SSL Structure Diagram

![ ](Images/ClipboardImage_ssl4.png)

What is an X.509 Certificate?

Role of certificates

An X.509 certificate binds a name to a public key value. The role of the certificate is to associate a public key with the identity contained in the X.509 certificate.

Integrity of the public key

Authentication of a secure application depends on the integrity of the public key value in the application’s certificate. If an impostor replaces the public key with its own public key, it can impersonate the true application and gain access to secure data.

To prevent this type of attack, all certificates must be signed by a certification authority (CA). A CA is a trusted node that confirms the integrity of the public key value in a certificate.

Digital signatures

A CA signs a certificate by adding its digital signature to the certificate. A digital signature is a message encoded with the CA’s private key. The CA’s public key is made available to applications by distributing a certificate for the CA. Applications verify that certificates are validly signed by decoding the CA’s digital signature with the CA’s public key.

Commands to Generate Certificates

Below are step and commands to produce and practice open ssl tool for producing certificates.

Step 1: Generate a Private Key

openssl genrsa -des3 -out server.key 1024

Step 2: Generate a CSR (Certificate Signing Request)

openssl req -new -key server.key -out server.csr

Step 3: Generating a Self-Signed Certificate

openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

How do I verify that a private key matches a certificate?

To verify that a private key matches its certificate you need to compare the modulus of the certificate against the modulus of the private key.

Please follow the below command to view the modulus of the certificate:

openssl x509 -noout -modulus -in server.crt | openssl md5

Please follow the below command to view the modulus of the private key:

openssl rsa -noout -modulus -in server.key | openssl md5

Remove Passphrase from Key:

cp server.key server.key.org

openssl rsa -in server.key.org -out server.key

Chapter 6: Network Packet Tracing

Packet sniffing is a process of acquiring any data passed over the local network and looking for any information that may be useful for spying. Mostly system administrators use packet sniffing to troubleshoot network problems (Eg. finding out why traffic is so slow in the network) or to detect intrusions or compromised password hacked workstations (Eg. A workstation that is connected to a remote machine on port 6667continuously when there is no IRC clients connected), and that is why this type of analysis originally was designed for network scanning.

What is Wireshark

Wireshark is a network packet analyzer. A network packet analyzer will try to capture network packets and tries to display that packet data as detailed as possible.You could think of a network packet analyzer as a measuring device used to examine what's going on inside a network cable, just like a voltmeter is used by an electrician to examine what's going on inside an electric cable.

In the past, such tools were either very expensive, proprietary, or both. However, with the advent of Wireshark, all that has changed. Wireshark is perhaps one of the best open source packet analyzers available today.

Some intended purposes

Here are some examples people use Wireshark for:

*   network administrators use it to troubleshoot network problems

*   network security engineers use it to examine security problems

*   developers use it to debug protocol implementations

*   people use it to learn network protocol internals

Installation steps for Wireshark

Type the commands below at Linux terminal:

wget http://sourceforge.net/projects/wireshark/files/src/all -versions/wireshark-1.0.3.tar.gz/download

gunzip -d wireshark-1.0.3.tar.gz

tar -xvf wireshark-1.0.3.tar.gz

Finally execute the wireshark tool by typing the below:

tcpdump -i eth1

Chapter 7: Overview of IPV6 vs IPV4

The Internet has run out of Internet addresses. Perhaps you’ve heard the news: the last blocks of IPv4 Internet addresses have been allocated. The fundamental underlying technology that has powered Internet Protocol addresses since the Internet’s inception will soon be exhausted.

A new technology will take its place, though. IPv4′s successor is IPv6, a system that will not only offer far more numerical addresses, but will simplify address assignments and additional network security features.

The transition from IPv4 to IPv6 is likely to be rough, though. Most people are unfamiliar with IPv4 and IPv6, much less the potential impact the switch to IPv6 may have on their lives.

Introducing IPV6

Here is a typical IPv4 address:

192.168.0.1

IPv4 address as a 32-bit value (2 power 4)

And here is a IPv6 address format:

2001:0db8:0000:0000:a526:2962:3960:c0e1

IPv6 addresses have a size of 128 bits

to 512 bits (2 power 8)

IPv6 Zero-Compression

Suppressing the leading zeros, the following IPv6 address:

2001:0db8:0000:0000:0007:0062:0060:00e1

becomes:

2001:db8:0:0:7:62:60:e1

To further shorten the address, we can also compress the largest "group" of all zeros to an empty group.

2001:db8:0:0:7:62:60:e1

becomes:

2001:db8::7:62:60:e1

IPv6 Network Prefixes

In your dealings with IPv6 addresses, you will probably encounter what is known as the network prefix. A network prefix denotes how many leading bits (those nerdy 1s and

0s) are set aside for identifying the network for which the address is a member. This number is specified at the end of the textual representation of an address by "/n" where n is the number of bits.

So for the address:

2001:0db8:0000:0000:a526:2962:3960:c0e1/32

we know from the "/32" that this address is a member of the 2001:0db8

IPv6 Addresses as URLs

To open a http connection to the host identified by 2001:db8::1234, we would type:

http://[2001:db8::1234]/ or

http://[2001:db8::1234]:3011/

Recognizing Types of IPV6 Adresses

The beginning of an address provides useful information. Apart from the link local prefixes, here are a few others :

*   3FFE is the prefix of a 6Bone address. The 6Bone provides addresses and connectivity to whoever wants to experiment with IPv6.

*   2002 is the prefix of a 6-to-4 address. 6to4 is an optional method of connecting IPv6 domains via IPv4 clouds. It provides a mechanism for assigning of an IPv6 address prefix to a machine that has a global IPv4 address.

*   2001 is the prefix of the first block of production addresses. http://www.dfn.de/service/ipv6/ipv6aggis.html lists block assignations.

*   FEC0 is the prefix of a site local address. Site local addresses are the equivalent of a private IPv4 address.

*   FF02::1 is address that multicasts to all nodes on the LAN.

*   FF02::2 is address that multicasts to all routers on the LAN.

IPV6 Commands in Linux

Type the following command below at putty tool:

ping6 -I eth0 fe80::21b:63ff:feab:e6a6

![ ](Images/ip61.png)

Below are some basic commands to test IPV6:

cat /proc/net/if_inet6

route -A inet6

ping6 -c4 -I eth0 ff02::1 - check all ipv6 available machine around ip -6 neigh show - check arp table

IPV4 to IPV6 Convertor Tools

Converting values from IPV4 to IPV6 can be very completed. It is best to use online tools to help to get quick results on acquiring accurate IPV6 values. It would be best to start to convert a simple IPV4 value like 192.168.1.99 as shown below.

Goto website below:

http://www.subnetonline.com/pages/subnet-calculators/ipv4-to-ipv6-converter.php

![ ](Images/ipv62.png)

IPV6 Prefix Tools

Goto website below :

http://www.dnskey.net/Main.html

![ ](Images/ipv63.png)

Resources

10 July 2012 http://www.ruwenzori.net/ipv6/Jims_LAN_IPv6_global_connectivity_howto.html

23 Aug. 2012

http://www.subnetonline.com/pages/subnet-calculators/ipv4-to-ipv6-converter.php All

17 Jan. 2011

http://wls.wwco.com/security/myopenssl.html

6 Feb. 2010

http://www.flatmtn.com/article/setting-ssl-certificates-apache

4 Apr. 2012

http://www.linuxquestions.org/questions/linux-networking-3/trouble-generating-ssl-certificates-116973/

19 May 2012

http://blog.didierstevens.com/2008/12/30/howto-make-your-own-cert-with-openssl/

15 Mar. 2012

http://www.devco.net/archives/2006/02/13/public_-_private_key_encryption_using_openssl.php

14 Sept. 2012

http://bsdsupport.org/2007/01/q-how-do-i-use-openssl-to-encrypt-files/

Logo on cover by Larry Ewing
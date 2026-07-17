![](images/00067.jpeg)

Index

[Linux Basics](#part0000_split_002.html__Toc48980319)

[Logs and monitoring](#part0000_split_003.html__Toc48980320)

[Managing Users and Groups](#part0000_split_004.html__Toc48980321)

[Performing a General System Health Check](#part0000_split_005.html__Toc48980322)

[Managing Processes and Services](#part0000_split_006.html__Toc48980323)

[How to Create Scheduled Tasks](#part0000_split_007.html__Toc48980324)

[Managing the Network](#part0000_split_008.html__Toc48980325)

1HourToStart

# Linux Basics

In this guide we are going to work with the command line. Though it may result so unfamiliar at the beginning, you will learn how important is for an aspirant administrator to be knowledgeable of the operations available only through the terminal. The modern practice, even for learners, is going toward this direction with cloud servers that offer operating systems available through the terminal. Amazon AWS is an example of cloud servers where you find a large number of machines free to be explored, just enabling the services, setting up your settings and ready to go with the ISO you prefer.

In this guide we use Linux distribution Ubuntu 18.04\. You will be able to operate exclusively through the command line to install excellent tools to monitor services and processes, control users, network management, logs, and more.

One of the most frequent command repeated in the book is “cd”. This command is used to move from one directory to another, followed then by the directory you want to move to. The path of the directory is separated by “/” that indicates to specify the name of the folder.

cd desktop/folder1

With the following syntax instead, you are able to go back to a previous path. The two dots refers to the structure and indicate the hierarchy of folders.

cd ..

Permissions

A reminder for the next chapter is the importance of permissions. Taking as an assumption that you can always use the current user in your machine, some operations may not be allowed to all users. That’s why it is important to keep an eye on the user you are working with. Sometimes it is necessary to run commands with “sudo” in front of the command itself to be able to properly execute an operation.

The Man command

When information about one command is not exhaustive, you may find handful to use the “man” command. Each command has a “man” available to show information about the command such as:

man kill

Kill is the command that kills processes. With man you can find out all possible options for this command.

What is the Kernel?

In this guide there are many references about the Kernel. If you have not never heard about this term, you may find interesting to have a full understanding of what it is and how it works.

With Kernel we mean the level that works in cooperation between the software and the hardware and it allows the communication between these two through drivers. Though a variety of distributions, there is always a Kernel for the same purpose.

When any application needs to apply changes to the hardware, it transfers the request to the Kernel which translates this request and communicates directly with the driver to accept or refuse requests.

The Kernel is one of the main components of an operating system that connects to the resources. This is why it also takes care of the management of the resources in an operating system.

The Linux Kernel is monolithic which means that is able to run complex operations applying exactly the concept we talked about earlier in this section. So, it takes care of the resources such as CPU, memory, hard drives, I/O devices, while it manages file systems, drivers, etc…

While on one hand this type of kernel is able to work appropriately with more precautions on all tasks because all the requests are handled directly by the kernel, on the other hand, this method require to accept all the requests each time. And this process may result in critical issues, when there is a request that still needs to be approved. Some of the advantages of this communication are the access from software to hardware, simple method to speak with each side, no additional drivers may be required, quick response from both sides. It is also true that there are negative aspects of using a Kernel. For instance, it requires memory, and it is not so much a safe choice.

Where are the files?

The Kernel files in Ubuntu are collected under the folder /boot.

What are deamons?

A specific section of this guide is about how to manage processes, but even in others you always find the term “deamons”. Processes are instances of programs that run to complete tasks. Processes are managed by the Kernel that gives them an identification number (PID). As we will see the PID is essential to work with processes as well as monitor the activities.

Some specific processes run and complete the requests on background while users are working. An example is the mail server that receives and forwards emails while you are working. These processes are not activated by the user but usually they start on their own when as soon as the operating system is booted. Some famous examples of deamons are httpd, Apache, MySQL that are available while you work on different activities.

# Logs and monitoring

While exploring one of the most used operating system as Linux, it is also fundamental to keep track of the execution of processes including applications and services that are running at the same time. Whether you are a developer or just a user with strong interest toward the topic, having a clear understanding of logs in Linux will be useful to have a comprehensive knowledge of the logics of the operating system no matter what distribution you are working on.

Whatever error is occurring, such as a crash in your operating system, all the events and applications running are recorded in specific files named log files. These files trace a list of the past events registered in the lifetime of an operating system. Are you the administrator of the OS? Through the log files you will be able to troubleshoot the issue and be able then to find the appropriate solution. Also, log files will result a great resource to monitor activities and be able to translate what they say.

In Linux, all the log files are stored in the path /var/log. Under this directory there all the logs that refer to processes related to the operating system itself. Then, depending for each application you’ll be able to identify the log files under separate folders in the same directory. Use the command line from any Linux distribution to complete this operation.

The logs are standard plain ASCII text files displayed as a list under the subdirectory /var/log. Their names change accordingly to their purpose such as auth.log or kern.log.

In this guide we are going use Ubuntu 18.04 as reference for almost all the tasks.

Categories of files

The main categories for these log files are:

*   System logs
*   Application logs
*   Event logs
*   Service Logs

They are critical files that has to be monitored to take care of centralized activities based also on the needs of the developer or administrator of the system.

System Logs

One of the main groups of log files is the system logs. To this category belongs all the logs that are essentially based on activities executed directly on the operating system and not log files created by other applications. The origin of the syslog can depend on syslog service, syslog protocol or syslog message. Syslog service addresses to receiving or forwarding messages. Based on a listener that then translates messages that are written or sent out to a remote server. Through the protocol log it is possible to figure the structure of messages and see how they are transmitted to another server. And finally, the syslog message is any message which has a standard header and a content that includes the timestamp, the application, the location in the system, and the priority.

Some examples of these files are:

*   System Log
*   Authorization Log
*   Deamon Log
*   Kernel Log
*   Debug Log

System Log Files

The System Log is the file that includes the majority of information related to the operating system.

The path for the System log file is: /var/log/syslog

In Ubuntu as well as other Debian-based systems all the files related to the system are stored under the syslog directory. While with some Linux distributions there is an exception for the messages which are available in a separate folder under the directory  /var/log/messages. These are generic files that describe who logged in when starting the machine such as any hardware issues that has to be identified at the reboot.

Authorization Log Files

This category of log files refers to a record with all the authentications including attempts which can be successful or failed accesses, the sudo command, passwords, management of users also through the Pluggable Authentication Module (PAM) system, and remote accesses through SSH (sshd logins).

The path for the Authorization log file is:  /var/log/auth.log

Other Linux distributions such as Redhat and CentrOS save the authorization logs in    /var/log/secure.

Through the use of these files you will be able to keep track of vulnerable methods and possible unauthorized accesses from not listed users. As an administrator you will need a further investigation to track these activities.

Deamon Log Files

This group relates to all the services and application deamons that run on background with no direct intervention from the user and no output shown. Some examples are printing services, Bluetooth applications, Gnome Display Manager, MySQL database (mysqld), etc…

The path for the Deamon log file is:  /var/log/daemon.log

Kernel Log Files

They give all the information about the Linux kernel such as who has logged in through the kernel. These logs provide warning and other messages that are really helpful for troubleshooting, such as for example a custom-built kernel as well as issues on hardware or network.

The path for the Deamon log file is:  /var/log/kern.log

Kernel Ring Buffer

Using the utility dmesg utility you are able to access to messages that describe any related issues with hardware at the boot. The Kernel Ring Buffer messages provide information that are effectively useful to detect and solve any critical problem of communication between a device and its driver.

The path for the Kernel Ring Buffer messages is:  /var/log/dmesg

Kernel Log Files

It provides information about the debug messages of the operating system.

The path for the Debug log files is:  /var/log/debug

Application Logs

Applications may create the log files under the directory  /var/log/. They are usually well recognizable because you can find exactly the name of the application they refer to.

Apache server log files

In Ubuntu all the log files of apache are located under the subdirectory  /var/log/apache2/. Other Linux distributions contain the Apache log files under  var/log/httpd/.

Here there are all the files used and loaded by Apache. This also means including in the list the IP address, user id all clients that are sending a request to the web server, time, date, HTTP resulting from a query.

All accesses to the Apache server are stored separately in two files: the access_log and error_log. The access log refers to issues with the memory as well as the request sent to the web server in order to access. Whereas the error_log reports all errors related to the web server which means issues occurred over the httpd requests.

In addition to these two files, the Apache server also has a different file for the attempts and accesses which is the access_log file.

Whether the attempts are successfully finalized or not, all the logs are anyway registered. And this information is clearly resourceful to reiterate critical bugs.

MySQL Log Files

For some Linux distributions, the MySQL Log files are placed in the directory  /var/log/mysqld.log or  /var/log/mysql.log. The error logs for the newer versions of Linux Ubuntu can be found in  /var/log/mysql/error.log.

While the location of the file can be different according to the Linux versions that you are using, the activity of monitoring is almost the same. You may use the file to trace unexpected behaviors of MySQL daemon mysqld such as starting while running or completing operations. A closer diagnosis on behaviors of the client with connections to a MySQL and requests of queries are examples of issues that may impact performances. Being knowledgeable of the content of a log file, you will be able to solve problems, crashes, and delays related to your database.

CUPS Print System Logs (Ubuntu versions)

The term CUPS stands for Common Unix Printing System and the error_log contains all the error related to printing issues on Ubuntu versions.

The path for the CUPS Print System Log files is:  /var/log/cups/error_log

Rootkit Hunter Log (Ubuntu versions)

The Rootkit Hunter is a utility that has the goal to look for possible backdoors, sniffers and rootkits that may constitute a thread for your operating system. The Rootkit Hunter is available in the latest versions of Linux Ubuntu.

The path for the Rootkit Hunter  Log files is:  /var/log/rkhunter.log

Samba (SMB) Server

SMB which stands for Server Message Block is a protocol used to share and transfer files between the same version of operating system as well as a variety of distributions or operating systems. That’s why it is so important as an administrator to be confident with these category of log files. Some attacks could come from a connection to another computer, and it is therefore a priority to be aware about how to face problems with the SMB protocol.

The path for the Samba Server Log files is:  /var/log/samba

Under the directory “samba” for the latest Ubuntu versions, you fill other categories which are the log.nmbd, log.smbd, and log.[IP_ADDRESS]. The first group named log.nmbd identifies with operations on the network which means Samba's NETBIOS over IP adresses. The log.smbd provides information on the activities of sharing files, also known as Samba's SMB/CIFS. The last typology, log.[IP_ADDRESS], contains information on requests for specific services sent by IP addresses.

X11 Server Log (Ubuntu versions)

In case you need solving issues with the X11 environment, you can look for the specific log files.

The path for the X11 Server Log files is:  /var/log/Xorg.0.log

If you are using an Ubuntu version, Xorg X11 is the default server used to run X11 Windowing Server.

Other services and events logs

Kernel

The information is about connections through the kernel. This type of log is useful to retrieve any issues such as warnings related to the kernel.

Login History

Keeping track of the history of the logins, you are able to parse incoming external attacks that attempted to enter a username and password to log on your operating system. Having access to this information you are conscious about who are other users who tried to access to your personal data. In this category you will find records on the last login sessions, current logins, and login failure.

Last Logins

In this list you will find the last logins to your system, meaning records on user that logged in and logged out.

The path for the Last Logins  Log files is:  /var/log/ lastlog

In the Ubuntu versions, you can use the following command from terminal to show a list of accesses. The less command will just help you to list this information in each page. You will be able to review the content in a more manageable way instead of scrolling down an endless list.

lastlog | less

The result on the output will be a list with username, IP address, date and time of access, pts/0 (which shows that the server has been accessed via SSH connection), date of creation of the folder.

Current Logins

You can check the current users logged in to your operating system.

The path for the Current Logins Log files is:  /var/log/wtmp

In addition to the folder wtmp that stores the information, using the command below you are also able to list the names of the users currently logged in:

who

![](images/00001.jpeg)

Login Failures

Under the same directory /var/log reside other log files including the failog. As suggested by the name, this log file is used to monitor information on the failures on login sessions.

The path for the Login Failog Log files is:  /var/log/faillog

In Ubuntu versions as well as other distributions, the faillog log files are placed in the directory /var/log/faillog. In order to display the failure on logins on Ubuntu, execute the following command from the terminal:

faillog

The syslogd (System Logging Daemon)

Both used for Linux and Unix operating systems make use of the syslogd also known as System Logging Daemon. It handles messages from different sources putting them in communication with the final destination. The syslogd works through the configuration file, reading information reported and forwarding the messages to the specified recipient.

The path of the configuration file is:  /etc/syslog.conf.

Each life of this file contains the selector and the action, which respectively is identified with the facility that matches with the recipient. The facility is meant as the process that triggers an event.

Taking the example here below, the line of that will be forwarded to the configuration file is made of the facility “mail” and the action “/var/log/mail” which is the file of destination.

Defining the priorities

Also, the line consists in a priority assigned to the facility. The level of priority varies each time separated by “.”.

mail.emerg /var/log/mail

Some examples of facilities are auth, daemon, and more. Priorities are listed from the lowest in terms of importance like “debug, info, notice, warning, err, crit, alert” to the highest level “emerg”.

As shown in the example, “mail” is the facility while “emerg” is the priority.

You can also use the @ to redirect the message to a hostname.

*.emerg     @mail.domain.com

The message will be interpreted by the system taking all messages with priority “emerg” and sending them to the user with the hostname mail.domain.com.

In fact, the symbol “*” means all the facilities. Typing as it follows here below you will refer to all the facilities and all levels of priority:

*.*     @mail.domain.com

Then, the “=” indicates messages with similar priority, while usually it is applied to the ones which have the same level or an increasing number.

As opposite to the equal sign, the “!” sign is used to apply the rules of message and exclude the ones with certain priorities.

In the configuration file, in the same line with the action that has to be sent, more selectors can be added using the “;” symbol. Moreover, also facilities can be added using the “,” symbol that separates one from each other.  

What does a log file contains?

Open the terminal and execute the following command to move to the folder containing the logs:

cd /var/log

“cd” is the command used in the Unix operating systems to move from the current position to another folder separated by “/”.

Then type the following command to see the content listed under the folder “log”:

ls

![A screenshot of a cell phone Description automatically generated](images/00002.jpeg)

The example above shown a screenshot from the console using Amazon AWS. Some of the directories listed are the same took in exam at the beginning of this guide.

When displaying this information, you may find some sort of duplicates such as “daemon.log.0” reported in sequence with different numbers. Don’t panic. These files are generated by the system copying and pasting the initial file to generate new ones. The starting files are not completely deleted from your operating system, but they are compressed separately. This utility known as log rotation works efficiently to save some space. As a result, you may find in your list of files something similar to daemon.log.0.gz that indicates the files compressed in the .gz archive.

One of the easiest ways to edit files with no issues is just using the “nano” command in the console. Typing the example below you are able to read the content of the kernel.log file:

nano kernel.log

Once you finished with your edits, you can simply close it using the combination CTRL + C.

Other two helpful features to edit the log files are “head” and “tail”. These two commands are used to show the head of the file, and the content at the bottom.

head file.log

Using the command “head” you will be able to view the first lines at the top of the file file.log.

If you need to display an amount of lines at 15 from the beginning, just type:

head -n 15 file.log

As a consequence, the command “tail” works as the opposite to the head command. This command shows exactly the content at the bottom:

tail file.log

Like the head command also tail has the same functionalities. Specifying the number of lines, it shows 15 lines instead of the fixed number of 10 lines:

tail -n 10 file.log

If you need to monitor at the same time a file and see edits on the file you can use the command line “tail -f”:

tail -f file.log

Another command you may perform is any search of the log files in terms of content. You may want to use the command here below to seek the word “mail” in the file file.log:

grep "mail" file.log

Also, you can use grep with “^” to look for words repeated in each line:

grep "^mail" file.log

# Managing Users and Groups

Knowing how to manage users and groups is a critical task for any user or administrator. One of the main reasons is because good practices on the management can be effective on the security of the network and the system. Also, it is essential to be confident about this topic to protect your data from external sources.

Before starting to mention any command used to these procedures you should be aware of how users and groups work. 

Each user is separated from others and under its account there are folders, files, and applications that are being used while in action. So, once the session is active with the specific user the operations are completed with a profile. Also, the user has a home directory assigned to it with the same name.

By default, a new operating system that is installed has a username defined as “root user”.

Type the following command to work as the root administrator:

su

However, this operation requires to apply a password which is not usually available on the system. So, one of the common practices to avoid any issue is just using the sudu word in front of any command. This method authorizes automatically to run a command with the root permissions. If you are enabled to work as a root user, you’ll be able to apply any edit.

Through the use of the sudo command you are able to run commands and apply changes on files such as the configuration file, applications common to all users, edit the permissions on folders and files for all the users. Not having access to the root user may prevent you from installing or editing settings on the system. All the root privileges are added to the file “sudoers” available under /etc/sudoers.

sudo cat /etc/sudoers

Running the command above you are able to see the content of the folder /etc which is not otherwise available.

The following command shows the list of users available on the current operating system:

cut -d: -f1 /etc/passwd

In addition to this, you can take a look to the user you are using right now:

whoami

![](images/00003.jpeg)

The next step to manage users is also how to create groups. The main goal of this operation is creating groups that have the same rules and functionalities. This task is very useful because all the users that belong to the same group are then able to work with the same set of folders, files, and they are allowed to execute certain applications.

Applying changes on users:

Adding a new user

One of the common operations is about adding a new user. To perform this task, you just need to type as here below with the command “adduser” followed by the name of the new user:

sudo adduser user1

![A picture containing holding, bird Description automatically generated](images/00004.jpeg)

First of all, the password as administrator is required to run the command adduser.

Then, it asks to enter the password associated to the new user and renter it again.

Also, another requirement is the full name of the user which is “User1” in our example.

After that, the operating system also requires information such as the room number, the work phone, home phone, and other. All of this information is optional. At the end, it asks if the information is correct. Just type:

Y

The new user is now added to your list.

Verifying if a user is a member

Run the command “id” to see if the user is a member:

id user1

Deleting a user

You can delete a user using he command “deluser” attached then to the name of the user you are going to delete:

sudo deluser user1

Locking and Unlocking specific users

Each user can be locked or unlocked with the following commands:

sudo passwd -l user1

sudo passwd -u user1

The options -l and -u work in this sense to respectively lock and unlock the users.

View all the processes related to a user

If you want to find details about the processes that involve one user like “user1”, type the command “ps”:

ps -u user1

Applying changes to the groups

How to see if you belong to a group

Run the command below to see what group you belong to:

groups

![](images/00005.jpeg)

The groups reported in the example are ubuntu, adm, dialout, cdrom, floppy, sudo, audio, dip, video, plugdev, lxd, netdev.

Also, you can use the following command to revise what groups your user is part of. You can display a list of the services and what permissions you need such as root.

sudo cat /etc/group

Adding a user to a group

The command used to add a user to a known group is “usermod”. You need to specify as arguments the name of the user and then the group that has to be associated to.

sudo usermod -a -G user1 ubuntu

In the example above, the “user1” is added to the group “ubuntu”.

Running again the command to see the list of users, you are able to check if the user has been added:

sudo cat /etc/group

As shown here below the user has been successfully added and displayed under “ubuntu”.

user1:x:1001:ubuntu

![](images/00006.gif)

Creating a new group

When you need to create a new group that it does not exist you can intervein with the command “groupadd” and the name of the group which can be “usergroup1”.

sudo groupadd usergroup1

Deleting a user from a group

Like we have previously seen in this section for the users, also the user can be removed from the groups. To apply these changes, use the command “deluser” followed then by the name of the user and then the group.

sudo deluser user1 usergroup1

If you want to review what groups a user belongs to, just use the following command:

sudo groups user1

Then, press the combination CTRL + X in order to exit from the file and enter “Y” to save the changes. It is asked to save the file with the same name “visudo” to override it. To proceed press “enter”.

The new “user1” is now able to perform any command with the root privileges.

Permissions

A useful operation for users is about permissions. In this case you need to enter a list of information:

*   The first one is the type which can be a file (-), directory (d), or symlink (l)
*   The user permissions, group permission, and other permissions are then divided in:
    *   read (r)
    *   write (w)
    *   execute (x)

For each of the operations read, write, and execute has been assigned a number depending on the role.

Giving privileges to a user

One of the operations that may result handful is editing the privileges of a specific user. This action requires to revise the file “visudo” that contains all the information about users.

First of all, open the file visudo with the following command:

sudo nano visudo

Now, type as follows here and replace “user1” with the name of the user you need to give the root privileges:

user1 ALL=(ALL) ALL

Also, you can give the permissions to the user1 as it follows here:

User_Alias ADMINS = user1

Cmnd_Alias HTTPD = /etc/init.d/httpd

ADMINS ALL = HTTPD

How to add permissions to a directory

Here below you find a way to add permissions to read and write to the folder “NewFolder”:

sudo chmod -R g+w $HOME/Documents/NewFolder

Similarly, permissions can also be denied to users that want to access to the folder “NewFolder”:

sudo chmod -R o-x NewFolder

With this procedure you are able to give the permissions to only one group of users and multiple groups at the same time. To overcome this limitation, you can use the access control lists. The command that follows here below enables the permissions to “read” the folder “NewFolder”. This means that the folder is now accessible even to a group named “users3” without involving any permissions for other users.

setfacl -m g:usergroup3:rx -R $HOME/Documents/NewFolder

To allow the same group of users to write the folder “NewFolder” use the following command:

setfacl -m g:auditors:rwx -R $HOME/Documents/NewFolder

# Performing a General System Health Check

A good practice to keep steady the performances of your system is checking and running a checkup of the entire system. The reliability of the operating system depends on the status of the virtual memory that can be accessed through the vmstat system utility, the CPU usage, the hard drives usage, devices in input and output, an analysis of the network, and processes currently running. All these operations are fundamental for a Linux server administrator.

To perform a health check of the system, we are going to use different sets of commands. Also, running commands includes using utilities that are handful for this purpose.

The command Top – Monitoring the tasks

One of the main steps that is very important to keep in mind is monitoring sources and what hardware are using in real-time. While it may seem useless, you may find that this method helps to supervise all the activities and make decisions on where to intervein. The command shows the CPU usage, memory status, swap memory, cache size, suffer size, process PID, etc…

The command “top”

Run the following command “top” to see all services running:

top

![A screenshot of a cell phone Description automatically generated](images/00007.jpeg)

As displayed above, you have a complete report of what are services running at this time. You can quit the utility, just pressing “q” from your keyboard.

You can also quit after showing 10 results with the following command:

top -n 10 

More in details the terms listed are:

*   PID: The process id
*   PR: It identifies the priority of the task
*   SHR: The shared memory usage for each activity
*   VIRT: The virtual memory usage for each activity
*   USER: User who is running the task
*   %CPU: The CPU usage.
*   TIME+: CPU Time expressed in seconds
*   SHR: The Shared Memory size (kb) usage for each activity
*   NI: The Nice Value of an activity. The priority can be positive or negative, meaning a lower level of priority or higher
*   %MEM: The Memory usage for each activity

Sorting information with different orders

The command “top” allows to list information with different orders. Here you may see some examples of how to sort tasks.

Sorting by process PID

For instance, you may want to sort of the statistics with the PID of process. To add a filter to sort data, press the combination of SHIFT + O. You are now able to decide how to filter your information. Press “a” to view the process PID.

After pressing SHIFT + O from the keyboard, type the following:

a

The option -k – kill process

Now that you know the name of a PID process, you can kill a process with the option “k”:

top -k

Then, press any key to come back to the top of the screen. After that, if you want to exit from the report, just press:

q

Sorting by CPU Usage

The combination SHIFT + P allows you to sort the tasks by CPU usage.

The option -u - User

Type the following option if you need to display the report of a known user:

top -u user1

As shown in the example the command top if followed then by the option “u” and the “user1” which is currently the user who is performing the operations.

![A close up of a street Description automatically generated](images/00008.jpeg)

The -b option - Batch mode

Use the option -b to display the output to a file or any other application:

top -b

The option -s – Secure mode

The option top -s enables the secure mode:

top -s

The option -d – Delay time

While the default settings for the delay time is 3s, you are able to edit this setting, just using the option -d as reported here below:

top -d 2

Passing as argument “-d” and “2”, it sets the delay time to 2 seconds.

The option -c - Absolute path

Press the option “c” to list the absolute path of running process.

![A screenshot of a cell phone Description automatically generated](images/00009.jpeg)

Again, press “q” to leave the terminal open without showing the list of tasks.

The option -h – Help

If you need a summarize of all commands available, press the following:

top -h

Now, you can see options you can use for your Linux distributions.

Monitoring the Memory

With the first step, you took a look to the general performances of your system. Now you can dig into some more details about the memory usage. Why is so important?

A higher load of tasks and size of data at the same time can imply an increase in use of memory. As a result, when memory is not enough, the system may occur in decreasing the performances and using other resources, such as the CPU, that usually should be regularly used without overcoming a certain level.

One of the main activities that you would like to approach is checking the free space available in your operating system.

Type the following command to see the space currently available in your memory:

watch free -m

![A screenshot of a cell phone Description automatically generated](images/00010.jpeg)

By default, every two seconds the memory usage is updated. You can update this setting, adding “-n 10” to set up a refresh every 10 seconds:

watch -n 5 free -m

![A screenshot of a cell phone Description automatically generated](images/00011.jpeg)

The amount of memory used is expressed in MB. This means that the total physical memory in the machine is 978 MB, with 114 MB used, 310 MB free, with no space shared. The buff cache is 553MB with still 718 MB available. Instead, the swap space is 0.

To exit, just press CTRL + X.

The VmStat (virtual memory statics)

VmStat is an essential utility that provides information about the virtual memory statistics. This means that it shows a summarize with memory usage, paging, hard drives status and CPU usage, and more.

Run the command here below to see the information from the last reboot:

vmstat

![A picture containing screenshot, clock Description automatically generated](images/00012.jpeg)

More in details you find a report about processes, memory, swap, io, system and CPU:

*   Procs
    *   r: The number of processes waiting for run time.
    *   b: The number of processes in uninterruptible sleep.
*   Memory
    *   swpd: the amount of virtual memory used.
    *   free: the amount of idle memory.
    *   buff: the amount of memory used as buffers.
    *   cache: the amount of memory used as cache.
    *   inact: the amount of inactive memory. (-a option)
    *   active: the amount of active memory. (-a option)
*   Swap
    *   si: the amount of memory swapped in from disk (/s).
    *   so: the amount of memory swapped to disk (/s).
*   IO
    *   bi: blocks received from a block device (blocks/s).
    *   bo: blocks sent to a block device (blocks/s).
*   System
    *   in: the number of interrupts per second, including the clock.
    *   cs: the number of context switches per second.
*   CPU

These are percentages of total CPU time.

*   us: time spent running non-kernel code. (user time, including nice time)
*   sy: time spent running kernel code. (system time)
*   id: time spent idle. Prior to Linux 2.5.41, this includes IO-wait time.
*   wa: time spent waiting for IO. Prior to Linux 2.5.41, included in idle.
*   st: time stolen from a virtual machine. Prior to Linux 2.6.11, unknown.

All the information reported above are accessible typing:

man vmstat

Why is so crucial to check the VmStat?

One of the columns you should focus your attention is the “swap”. It is significant important to assure that this data is set to 0 or close to. A higher value indicates there are considerable issues. Some causes for swapping may include an application that impacted the memory causing an exceed of usage, some problems in the configurations, or a low amount of memory installed in the machine.

Whatever is the case, trying to identify the problem is always positive to contain any issue in the future. As seen earlier, the command “top” is able to help you to monitor the activities on processes.

Executing the VmStat for a specific number of seconds

Type the following command:

vmstat 2 4

Executing this command, the report will be updated every 2 seconds for 4 times before stopping. As mentioned earlier in this section, data refer to the updated values from the last time of the reboot.

![A screen shot of a computer Description automatically generated](images/00013.jpeg)

As also illustrated with a recap from “man vmstat”, the “r” addresses to the run queue, which refers to the queue that each application has to wait in order to be executed.

Some options you can see more details about the information.

The option -a – active and inactive memory

The option -a also specifies the status active and inactive of the memory.

The option -t – timestamp

Use the option -t to view the timestamps in each line.

vmstat -t

![A picture containing orange, room Description automatically generated](images/00014.jpeg)

The option -d – Disk

With the option -d, you can view the disk status like here below:

![A screenshot of a cell phone Description automatically generated](images/00015.jpeg)

The data about the hard drives provides three columns with reads, writes, IO. In the summarize there is a full list of written sectors, readable sectors, and the time to access this information.

The option -s – switch

With the option -s, you are able to see the events and memory statics.

![A screenshot of text Description automatically generated](images/00016.jpeg)

The iostat command – CPU and I/O statistics

Iostat is a tool that monitors data about input and output devices and the CPU. In order to optimize all sources, it is essential to have a clear idea of the loading time of each device, the average to transfer files, etc.

Attempting to execute the command iostat you may find a similar output that asks to install systat:

iostat

![A screenshot of a social media post Description automatically generated](images/00017.jpeg)

Type the following command as it follows:

sudo apt install sysstat

![A picture containing indoor, bird Description automatically generated](images/00018.jpeg)

Just type “y” to continue with the systat installation.

![A picture containing indoor, bird Description automatically generated](images/00018.jpeg)

Once that the installation is completed type again:

iostat

You are then able to display the information as it follows:

![A screenshot of a cell phone Description automatically generated](images/00019.jpeg)

The option -c – CPU statistics

The option -c is used to display only the statistics related to CPU:

iostat -c

Statistics on the CPU usage are useful to identify how to figure the slowdowns of the machine, especially if it only has one instead of two.

The option -d – Disk I/O statistics

The option -d is used to display only the partitions of the disk showing the devices such as sda. Information includes the time of response to write on disks displayed in disk.

iostat -d

![A screenshot of a cell phone Description automatically generated](images/00020.jpeg)

The operating system stores all the information on the memory. The best way to perform successfully this activity is saving data on a temporary memory instead of just using the physical memory. Accessing to what is called “cache”, your information can be delivered more quickly.

The option -p – Disk I/O statistics

Once that you know the disk you would like to take in exam, you can further investigate about it, using the option -p as it follows here:

iostat -p loop0

![A screenshot of a cell phone Description automatically generated](images/00021.jpeg)

As shown above, there is specific information about the device “loop0” that describes the speed rate on writing, reading, etc.

The option -N – LVM statistics

The option -N offers information about the statisticd on LVM:

iostat -N

![A screenshot of a cell phone Description automatically generated](images/00022.jpeg)

The option -v –Iostat Version

Type the option -v to find out the iostat version.

The iotop command

Iotop is a utility that can be installed on the Ubuntu distributions to trace activities that use input and output devices. It makes use of the kernel and python to work.

In Ubuntu, the iotop utility can be easily installed through the apt command. Type the “iotop” command to see the results:

 ![A screenshot of a social media post Description automatically generated](images/00023.jpeg)

Then, when the installation is completed, run the command:

sudo iotop

The results of the command show a list with the columns TID PRIO USER, DISK READ DISK WRITE, SWAPIN, IO>, and COMMAND. The column “command” refers to the type of process or thread taken in exam, while the other columns just displays the time to read and write while waiting for a I/O. The “IO” command operates on the I/o usage for each process. “Swapin” works on the swap usage of each listed process.

You can also apply a filter to view only the processes that show more specific information toward the I/O:

![A screenshot of a cell phone Description automatically generated](images/00024.jpeg)

Some useful options for this command are:

*   Option -d SEC, --delay=SEC. It sets the delay between iterations in seconds (1 second by default).  It accepts non-integer values such as 1.1 seconds
*   Option -p PID, --pid=PID. It provides a list of processes/threads to monitor (all by default)
*   Option -u USER, --user=USER. It provides a list of users to monitor (all by default)
*   Option -P, --processes. It only shows processes. Normally iotop shows all threads.
*   Option -a, --accumulated. It shows accumulated I/O instead of bandwidth. In this mode, iotop  shows  the amount of I/O processes have done since iotop started.
*   Option -k, --kilobytes. It uses kilobytes instead  of a human friendly unit. This mode is useful when scripting the batch mode of iotop. Instead of choosing the most appropriate unit iotop will display all sizes in kilobytes.
*   Option -t, --time. It adds a timestamp on each line (implies --batch). Each line will be prefixed by the current time.
*   Option -q, --quiet. It suppresses some lines of header (implies --batch). This option can be specified up to three times to remove header lines.

Type “man iotop” to see all the options available as reported here above.

The htop command

The htop command is a tool available in Ubuntu with no installation required. It’s a good alternative to the top command and similarly it provides the real-time processes currently executing in the machine.

Type the command to see the results:

htop

![A screenshot of a cell phone Description automatically generated](images/00025.jpeg)

As shown above, you are able to scroll in vertical to see the list and then in horizontal to see the full overview. You can directly kill a process with no need to enter the PID, as instead required by the top command. Also, htop is more user friendly because you can use the pointer to select a process. Some of the main information highlighted is the CPU usage, Memory usage, and Time of delay.

Like shown in the example above, you should have a progress bar with different colors. Each color matches with a meaning:

*   Blue: CPU usage with low priority
*   Green: CPU usage with regular priority
*   Red: CPU usage with system processes
*   Orange: CPU usage through IRQ time
*   Magenta: CPU usage with regular priority through Soft IRQ time
*   Grey: CPU usage through IO Wait time
*   Cyan: DCPU usage through Steal time

What indicates the tabs in the columns? Here you can review more details about what each term stands for:

*   PID: Process ID
*   USER: The who is using the machine
*   PRI: The priority of a process in use
*   N: The priority of a process reset by the user or root.
*   VIR – Virtual memory in use
*   RES – Physical memory in use
*   SHR – Shared memory in use
*   S – The state of a process
*   CPU% – CPU usage by process
*   MEM% – Memory usage by process
*   TIME+: Time needed to execute a process Command: The process itself is referred to.

Below that, you find the statistics about the CPU, Memory, Swap and also shows tasks, load average, and Up-time.

All the processes are by default filtered according to the CPU usage.

Some additional functionalities can be tried using the keyboards:

Up and Down: Use the keyboard to see the processes

U: Use it to processes of a particular user

P: To filter the process with higher CPU usage

M: To filter the processes with higher memory usage

T: To filter the processes depending on the time

H: Use it for the htop help

At the bottom of htop command, you find the options you can access to using the commands from F1 to F10 (like help, setup, filter tree kill, nice, quit).

The /proc/meminfo file

The “meminfo” file under the directory /proc summarizes the memory used by the machine, which means the physical and virtual memory, the shared memory, and the buffers.

Type the following command to find out the ouput:

cat /proc/meminfo

Some important information is about MemTotal, MemFree, MemShared, MemShared, Buffers, SwapCache. The MemTotal is the memory available and part of this is used by the kernel. Buffers is the memory in buffer cache. Cached is the memory in the pagecache. SwapCache is the memory available in the swapfile.

![A screenshot of a cell phone Description automatically generated](images/00026.jpeg)

The VM Statistics provides details about the status “active” and “inactive” of the memory. When the load exceeds the unused part can be used for the purpose.

Other information is about HighTotal (memory in high regions), RAM, LowTotal, LowFree, SwapTotal (The physical swap memory), SwapFree (free wap memory), Dirty (memory where it can be written), Writeback Memory which is actively being written back to the, Mapped (files to be mapped), Slab, Committed_AS, PageTables, ReverseMaps (number of reverse mapping completed), VmallocTotal (vmalloc memory area), VmallocUsed (vmalloc area used), VmallocChunk.

Lsof – List Open files

As suggested by the name, Lsof stands for List of open files and refers to files such as disk files, network sockets, pipes, devices, and processes. The files are open which means that they are currently running.

![A screenshot of a cell phone Description automatically generated](images/00027.jpeg)

On top of the table reported you would have the values COMMAND, PID, TID, USER, FD, TYPE, DEVICE SIZE/OFF, and NODE NAME.

Digging into more information about it, FD means “File descriptor” and accepts the values:

*   Cwd: current directory
*   Rtd: root directory
*   Txt: text file
*   Mem: memory-mapped file

Then, the values are followed by:

*   R: Read
*   W: Write
*   U: Read and write

Other utilities for your health check

The Nmon Utility

The utility has the goal to analyze the performances of a system regarding the cpu, memory, network, disks, file systems, nfs, top processes, resources, and power micro-partition.

In the Ubuntu distributions you need to install the utility with the following command:

sudo apt install nmon

When the installation is completed, launch the command here below “nmon”:

nmon

As shown below all the statistics are shown. With the option “c” you are able to filter the information about the CPU.

Press CTRL + C to exit from the utility.

![A screenshot of a cell phone Description automatically generated](images/00028.jpeg)

The option “t” – Top processes

The option “t” shows the top processes listed:

nmon -t

![A screenshot of a cell phone Description automatically generated](images/00029.jpeg)

The option “r” – Resources

The option “r” displays information about the resources used which can be the CPU.

![A screen shot of a computer Description automatically generated](images/00030.jpeg)

The option “n” – Network

The option “n” shows the details about the network.

The option “d” – I/O Disks

The option “d” displays information about the I/O disks.

The option “k” – Kernel

The option “k” displays information about the kernel.

The option “n” – NFS

The option “n” displays information the data NFS.

The option “j” – File System

The option “j” displays information the file system.

The Collectl utility

An additional tool to “top” and “htop” commands is the Collectl utility. The name “Collectl” can give a hint about the purpose of this application. In fact, the utility is used to collect data about the status of the system such as cpu, disk, memory, network, sockets, tcp, inodes, etc.

Some of the main functionalities are the exportation of the output in a diversity of formats, the monitoring of the subsystem, the monitoring of the remote machines, the ability to write a file or a socket.

Typing “collectl” you see that the command is not found in Ubuntu:

collectl

![A screenshot of a social media post Description automatically generated](images/00031.jpeg)

Run the command to install “collectl”:

sudo apt install collect

It asks to confirm pressing “y” in order to continue the installation.

After this, it asks what kind of web server to use. The options are Apache2, Lighttpd, and more. Pressing the selection and then “ok”, the installation is then completed.

The information is about the subsystem which includes cpu, disks, and network.

![A screenshot of a cell phone Description automatically generated](images/00032.jpeg)

The option “--all” – File System

The option “--all” displays information all the subsystems.

The option “stc” – File System

The option “stc” displays information about the tcp and cpu.

Here below you find a detailed list of the options:

*   b – buddy info (memory fragmentation)
*   c – CPU
*   d – Disk
*   f – NFS V3 Data
*   i – Inode and File System
*   j – Interrupts
*   l – Lustre
*   m – Memory
*   n – Networks
*   s – Sockets
*   t – TCP
*   x – Interconnect
*   y – Slabs (system object caches)

# Managing Processes and Services

Before analyzing in depth handy commands to manage processes and services, we need to clarify what are processes and services.

What do we mean with “process”?

Process is an instance of a running program. As a consequence, all the times that an application is running, a process is initiated and an identification number called “PID”, that stands for Process ID, is attributed together with the group or the user. Processes are running at the same while the machine is working on different tasks using the same sources such the memory and the CPU. This means that whereas there is a variety of tasks completed at the same time, the number or sources is still the same. That’s why as an administrator you should be able to maximize the performances of your machine.

Processes can be divided in two major groups which are the background processes and the interactive processes. With the first group we mean all the processes that are not started directly by the user, but they are working automatically on the background. One of the most famous processes is the Deamons. This category of processes runs on the background and with no input by the user, though they can be managed directly if needed. In the second case, the interactive group identifies the processes that are started by the user, recalling a command from the command line. Therefore, the user is in complete control of these processes.

A new process

Creating a new process for the Linux distributions means copying and then pasting the current process. The PID is changed to a new one as seen earlier is a different ID.

In addition to the PID that identifies the process itself, each process can be recognized through the PPID which is the parent process ID. Executing the tasks, parent processes activate other processes which are the child processes that complete their operations at the same time.

One of the most famous processes is the init process. This process is so important because is executed at the boot while still other processes are not running. For this reason, its ID is always 1, as it is the first process to be run. To find the PID of a process you can use the command “pidof”. So, if you would like to know the PID of system, you can use:

pidof system

What are the states of processes in Linux?

A process can change the state on the run. Each process is created, then accepted and when is ready to be used it can be finally executed through the schedule dispatch. Also, a process may be put a waiting status if there are I/O sources needed or an event that requires the attention. The event then can change status once that the waiting time is completed. If there is a no hardware request, the process can be interrupted before being able to run. At the end of the steps, the execution is stopped. 

Here below you find some examples:

*   Running: In this state, processes are running which means that the process has been created and it is active
*   Waiting: The process is waiting for an answer from a program or some resource which is fundamental to the process in order to accomplish the directions. Some processes may be interrupted if they are waiting for some services or not physical sources. If they are waiting to use for example the hard drive, processes cannot be interrupted.
*   Stopped: The process stopped to work for some reasons such as the debug mode.
*   Zombie: The process is listed but it does not work anymore.

Some of the most useful commands in Linux to manage operations with processes are “ps” and “top” commands.

The command ps

The word “ps” stands for process status. Executing this command, you can see the processes currently active:

![A screenshot of a cell phone Description automatically generated](images/00033.jpeg)

If you want to list all the processes use one of the two choices:

ps -a

ps -e

Monitoring processes through kill, pkill and killall

The Kill command

Knowing what is the PID of a process is essential to act and kill it. In case you want to kill the Chrome process you need to know the name of the process:

pidof chrome

Now that you have the PID, you can directly kill the process:

kill PID_NUMBER

After that, you can check to see if the Chrome process is still active:

pidof chrome

Another useful option is applying the kill command to delete multiple processes at the same time with only one command like here:

kill PID_NUMBER1 PID_NUMBER2

Always keep in mind that each user is able to kill its own processes but not the ones belonging to another user as well as the System processes. Only a user with the root privileges is allowed to kill processes from any user or System processes.

The Pkill command

Instead of using the PID which is the number that identifies the process, you can apply the same concept to delete a process by name. In the example that follows here you are going to use the “pkill” command to kills the MySQL process.

pkill mysqld

The killall command

As you can imagine from the name, the “killall” command is able to kill all processes related to a main process. For example, if you have a parent process with child processes and other instances, it will take time to figure with what processes to act. While using the killall command is much easier.

Repeating similarly the example seen previously, you can kill the MySQL process like here below, deleting all the instances linked to it:

killall mysqld

Finally, always check if the process is still running or not using the “pidof” command:

pidof mysqld

The pgrep utility

Pgrep is a valid alternative utility used for a similar purpose to what we have seen earlier. Pgrep is a command that allows to find the ID of a process. Executing this command from the command line, it returns the numeric values.

For instance, if you want to find the PID of the SSH server, you can type the following command:

pgrep ssh

The output should show something similar to here. If nothing matches with the name of the program requested, it should report a “0” value meaning that there are no entries with what you are looking for.

![A screenshot of a cell phone Description automatically generated](images/00034.jpeg)

After identifying the PID, you are able to use the same command “kill” followed by the name ID.

If you would like to know the name too for each entry listed, you apply the option “-l” as here below:

pgrep ssh -l

The command shown displays the name sshd so that you are to see to what each PID matches with.

![A screenshot of a cell phone Description automatically generated](images/00035.jpeg)

Monitoring Tools

Glances tool

Glances is a cross-platform tool that works on a variety of operating systems and Linux distributions. Written in Python this tool operates on real-time and monitors the performances of these resources:

*   CPU
*   Memory
*   Load
*   Process list
*   Network interface
*   Disk I/O
*   IRQ / Raid
*   Sensors
*   Filesystem
*   Docker
*   Monitor
*   Alert
*   System info
*   Uptime
*   Quicklook (CPU, MEM, LOAD)

Glances can be used as a replacement to the “top” command because it works with more precision providing detailed data about each resource, its usage in the system, and evidencing which resources are making more use.

Installing Glances

Glances is not a native application in Linux Ubuntu. Running the command “glances” Ubuntu requires to install the application through the APT:

glances

![A screenshot of a cell phone Description automatically generated](images/00036.jpeg)

Then, start the installation of glances with the command:

sudo apt install glances

The command line asks if you want to continue because installing the software requires around 100MB of additional space. Type “Y” to complete the installation.

 ![](images/00037.jpeg)

All the packages would be download and installed.

Now, run again the command:

glances

The new utility installed should show something similar to this here below:

![A screenshot of a cell phone Description automatically generated](images/00038.jpeg)

In this utility you find a summary section with all information about the system that can be scrolled horizontally. 

From the top, in the first row you find hostname, the Linux distribution, the kernel version, and the system uptime.

In the next row, there is a list of data reported about CPU, memory usage, swap, and load statistics. All information is shown in percentage with a short summarize at the beginning of the row on the left.

For what concerns the CPU, Glances offers many details about:

*   CPU: CPU usage in percentage
*   User: Applications available in the user environment
*   System: Kernel applications running
*   Idle: Idle time
*   Nice: This value defines the priority of processes
*   Irq: Requests that interrupts the CPU
*   Iowait: Waiting state for I/O inputs before running again a process
*   Steal: The virtual CPU is waiting for the physical CPU which is working on other processes
*   Ctx-sw: Context switches per second
*   Inter: “Inter” stands for interruptions and it means the time needed to interrupt the use of the CPU from working on a device
*   Sw_int: Interruptions related to the software

For what concerns instead the memory you find more details here below:

MEM: Memory usage expressed in percentage

Total: The total amount of RAM physically installed on the machine

Used: The amount of memory excluding cache or buffers

Free: The memory still available

Active: The current actively used memory

Inactive: The current not actively used memory

Buffers: Buffer space usually used to connect with the input or output devices

Cached: The memory used to temporarily save date before moving them to a physical memory

In the process section you find information about the processes currently running on the machine:

*   CPU%: The CPU for each core expressed in percentage
*   MEM%: The RAM memory used by each process while running
*   VIRT: The virtual memory used by each process expressed in Megabytes
*   RES: “RES” refers to resident, which means the physical memory used by each process expressed in kilobytes, megabytes, and gigabytes depending on the amount of space available
*   PID: ID number that identifies each process
*   USER: The name of the user who is running the process
*   TIME+: Cumulative amount of CPU time used by each process since the beginning
*   THR: Threads running for the process
*   NI: The nice number of the process
*   S: “S” stands for status; it can be R - running, S - sleeping, I - Idle, T or t - stopped during a debug mode, or Z – Zombie when the process died, and it is not anymore available but still visible in the list of processes
*   R/s and W/s: Rate time to read and write the disks
*   Command: The command that activated the process currently under analysis

In another section you can identify the warnings and the alerts which are helpful in case you need further investigation about a few sections of the utility.

The colors change then the importance to where to look at first glance. With the green color, we know that everything is fine. A blue color instead requires our attention to figure what is going on. A violet indicates a warning, while the red points out a critical issue that requires a quick action.

Options in Glances

Here you also find some options to evidence particular details:

*   a: It lists processes automatically
*   c: It lists processes by amount of CPU
*   m: It lists processes by amount of memory
*   p: It lists processes by name
*   i: It lists processes by I/O rate
*   d: it shows or hides disk I/O stats ols
*   f: it shows or hides file system statshddtemp
*   n: it shows or hides network stats
*   s: it shows or hides sensors stats
*   y: it shows or hides hddtemp stats
*   l: it shows or hides logs
*   b: Bytes or bits for network I/Oools
*   w: it removes warning logs
*   x: it removes warning and critical logs
*   t: To review settings on network and I/O devices
*   u: To review cumulative network I/O

This utility also allows to monitor local machine with the web interface (Web UI) or export stats to a CSV file.

You can view all the information about Glances from the help option “-h” or typing “man glances”.

To leave the utility press quit:

q

What are services?

When an application is running tasks are executed on the machine. A service waits for a request and it gives an answer.

The question you may have is about what services are available in your operating system. To answer to this question, you can list here below the services available:

service --status-all

![A screenshot of a cell phone Description automatically generated](images/00039.jpeg)

The Systemd Utility

The Systemd is a system and service manager that traces processese while they are running. You can use this useful utility to run, stop, or restart services. In the Systemd, units are the blocks that can be identified with services such as (.service), devices (.device), sockets (.sockets), slice, etc…

Services can run in parallel taking advantage of a new way to show services.

At the boot, the system is loaded after the BIOS recalled it through the boot loader. After that, the Kernel loads the systemd and processes are run. At this point the user is loaded and its environment is loaded through the systemd.

These are some important directories to remember where to find unit files:

*   /usr/lib/systemd/user/: Under the folder of created for each user, you find all files
*   /run/systemd/system/: Location runtime for unit files
*   /etc/systemd/system/: Unit files can be extended storing them in this folder.

Running the command “systemctl” you can retrieve a list of all units available under the Systemd:

systemctl

![A picture containing text, newspaper Description automatically generated](images/00040.jpeg)

In this list you can see the same of the “Unit”, the status for “Load”, “Active”, “Sub”, and the “Description” that summarizes what type of unit is for each row.

Run then the following command to see the list of unit files with the current state for each unit:

systemctl list-unit-files

![A screenshot of a cell phone Description automatically generated](images/00041.jpeg)

You can also display units which are failed to be initialized:

systemctl –failed

To restrict the analysis to only the services instead of a list of all services, you may want to use the following command:

systemctl list-unit-files –type=service

To restart a service, you type the word “start” and then the name of the service followed by the extension “.service”:

systemctl start name.service

To restart a service, you type the word “stop” and then the name of the service followed by the extension “.service”:

systemctl stop name.service

To restart a service, you type the word “restart” and then the name of the service followed by the extension “.service”:

systemctl restart name.service

To restart a service, you type the word “reload” and then the name of the service followed by the extension “.service”:

systemctl reload name.service

To restart a service, you type the word “status” and then the name of the service followed by the extension “.service”:

systemctl status name.service

Enable and Disable a service

Services can be enabled and disabled accordingly using the Systemctl. The following command is used to enable a service:

systemctl enable name.service

This command here below is used to disable a service:

systemctl disable name.service

Mask or unmask a service

Each service can be masked or unmasked to avoid that all units are running at the same time.

This is the command to run to mask the service:

systemctl mask name.service

This is the command to run to unmask the service:

systemctl unmask name.service

The Acct tool

The Acct tool is an application running on background to monitor activities run by users. The goal of the tool is checking the amount of resources used for tasks. As a developer or administrator, you constantly need to assure that the usage does not overcome the threshold and performances are steady. Otherwise, major issues on services such as Apache Web Server may occur and lead to latency while loading important files. For this reason, having a tool like Acct is a great help to reduce time in using different commands to solve the same issues.

Some of the main features of this tool are:

*   Statistics of users that logged in and logged off
*   Statistics of users that accessed to the machine
*   Commands previously executed by a user are still available

To install the Acct utility, you can use the APT as shown here below:

sudo apt-get install acct

In this case, you need to run this command with the sudo at the beginning in order to have permission as root to run the command.

Type the following command to see the data collected from the wtmp file. They provide the time the user connected to the system:

ac

![](images/00042.jpeg)

The option -d

The “option -d” shows the time expressed in days:

ac -d

![A screen shot of a computer Description automatically generated](images/00043.jpeg)

The option -p

The “option -p” shows the total login time of each user:

ac -p

![](images/00044.jpeg)

The command “sa”

Executing the command “sa” you are able to see a summary of the commands available and recently executed:

sa

![A screenshot of a cell phone Description automatically generated](images/00045.jpeg)

Taking a closer analysis of the tabled collecting the data, you see to what each column corresponds to:

*   Column 2: 0.00re - time expressed in wall clock minutes
*   Column 3: 0.00cp - system/user time expressed in cp
*   Column 5: 1131k – time of CPU expressed for the numbers of units
*   Column 6: ac – the command it refers to

The option -u

The “option -u” shows information about the individual user:

sa -u

The option -m

The command “sa” attached to the “option -m” works to show the number of processes expressed in cpu minutes:

sa -m

![A screenshot of a cell phone Description automatically generated](images/00046.jpeg)

The option -c

The command “sa” attached to the “option -c” works to show the percentage of users:

sa -c

![A screenshot of a cell phone Description automatically generated](images/00047.jpeg)

# How to Create Scheduled Tasks

A frequent operation in Linux requires to create scheduled tasks. To accomplish this activity, you may use Cron, a handful utility that can enable tasks that work on the background while you are working on other files. You can decide when to schedule these tasks so that they work at different times such as backup, notifications, cleanup system files, synchronize files, and more. All these operations are called “cron jobs” and they can be run with the “crontab” command. The “tab” refers to the tables where all the tasks are listed.

In this short introduction to this section, you may revise how to check if you already have a version of Cron installed in your system, then run the task through the command line.

Users can create their own cron jobs which are collected in the directory  /var/spool/cron/crontabs, although it is only accessible through the command line.

Permissions on crontabs

The file in the directory  /etc/cron.deny  can limit user to edit the crontab. If the file “cron.deny” exists, the name of the user is usually listed in this file and this means that the user is not able to apply changes to the cron jobs. On the other hand, if the file “cron.allow” is available under the same directory /etc/ it means that only the users listed are able to edit the scheduled jobs. When both the files exist at the same time, the “cron.allow” fiel is able to override the “cron.deny” file.

The information is usually available in these folders:

*   /etc/cron.allow
*   /etc/cron.deny (editing the file we may disable some users to the features)
*   /var/spool/cron/crontabs

Cron is usually already installed in the Linux distributions. Just in case you don’t have a version ready to be run, you may proceed with updating the APT:

sudo apt update

![A screenshot of a cell phone Description automatically generated](images/00048.jpeg)

After completing the update, you should have a similar screenshot showing the number of packages upgraded for the APT.

And then, you can go on installing Cron:

sudo apt install cron

When the installation is completed, you can start the Cron Service. You have to use the “sudo” before the command to run the commands as an administrator.

sudo service cron start

After that, you can check the status of the Cron Service. Here below you can see how it should look like. The service results to be enabled with the status “active (running)”.

![A close up of a newspaper Description automatically generated](images/00049.jpeg)

All the times that you would like to add a scheduled task, you open to edit the crontab file and edit it adding an expression.

Running the following command, you are able to edit the crontab file for the current user:

crontab -e

The expressions with the crontabs

To create the expressions there is a precise syntax that you could follow:

0 7 * * * /root/backup.sh

This example executes a backup at 7 am. No information has been provided for day of month, month of the year, and day of the week. This means that the con job is activated and repeated each day.

Here below a summarize of the expression:

*   First position: Minute with values between 0 and 59 – In the example the value is 0
*   Second position: Hour with values between 0 and 23 – In the example the value is 3
*   Third position: Day of Month with values between 1 and 31 – In the example the value is *
*   Fourth position: Month of the year with values between 1 and 12 or Jan through Dec – In the example the value is *
*   Fifth position: Day of week with values between 0 and 6 or Sun through Sat – In the example the value is *
*   Sixth position: Script or command (This includes the path to the command) – In the example the value is /root/backup.sh

The operators for the cron jobs are:

Asterisk (*): all values or any possible one for the field

Comma (,): refers to a list of different values

Dash (-): refers to a range of values

Separator (/): refers to 1/10 or increment of a range

Examples of use that combine an operator with the number shown in a position like here:

*   * * * * - Executes the operation every minute.

*   15 * * * * - Executes the operation 15 minutes after every hour.
*   0,15,30,45 * * * * - Executes the operation every 15 minutes.
*   */15 * * * * - Executes the operation every 15 minutes.
*   0 5 * * * - Executes the operation every day at 5:00 AM.
*   0 7 * * 2-4 - Executes the operation every Tuesday, Wednesday, and Thursday at 7:00 AM.
*   15,30 */7 * 7-12 * - Executes the operation on the 15th and 30rd minute of every 7th hour every day of the last 6 months of the year

Another example to clarify the use of expressions:

15 7 10 * * /root/backup.sh

With the command here above, the cron job has been setup to run a backup every 10 of the month at 7:15\.

An example with the day in letters:

30 2 * * mon /root/backup.sh

The task runs a backup every Monday at 2:30.

How to list the Cron jobs

As seen earlier, the cron jobs run on the background and the deamons is able to read the information. The option -e refers to the user.

crontab -e

Running the command, usually a list of choices for the text editor is presented to you. By default, the editor widely used is Nano if no option is listed:

*   /bin/nano
*   /usr/bin/vim.basic
*   /usr/bin/vim.tiny
*   /bin/ed

If you are able to decide the editor, you can just enter the option from 1 to 4\.

The “option -l” instead refers to the list. It allows to view the file without editing it:

sudo crontab -l

Even if you are running the command with sudo, you may not be able to execute the code if the file “cron.deny” exists or the “cron.allow”.

Or you can also use the command here below specifying the username:

sudo crontab -u user1 -l

Usually this command should be executed with the “sudo” because only the administrator has the privileges to the cron jobs of all the users.

How to delete the cron jobs

You can decide to delete all the cron jobs. The “option -r” stands for “erase” and it can be applied with the following command:

crontab -r

Also, you can delete the cron job for a specific user such as “user1”:

crontab -r -u user1

Another option also offers the chance to confirm before deleting the crontab:

crontab -i -r

The strings in Crontab

Another useful feature of the Cron Jobs is the use of the strings that allow to avoid a waste of time not repeating the same part of the expressions. Here there is a list:

@hourly: Performed once every hour i.e. “0 * * * *“

@midnight: Performed once every day i.e. “0 0 * * *“

@daily: Performed when is midnight

@weekly: Performed once every week, i.e. “0 0 * * 0“

@monthly: Performed once every month i.e. “0 0 1 * *“

@annually: Performed once every year i.e. “0 0 1 1 *“

@yearly or @annually: Performed once a year

@reboot: Performed once at startup

Other examples to schedule tasks

Though seems very simple at the beginning, it is obvious that there are commands that may result more complex when you try to manage the commands for specific tasks.

This is the syntax to create a log file:

0 * * * * /path/to/your/script >> /var/log/cron.log

Check out the execution of the cron job in the syslog:

grep 'CRON.*(yourusername)' /var/log/syslog

For more details about the “crontab” command in Linux Ubuntu, you can enter as it follows here:

man crontab

# Managing the Network

Whether you are working as an administrator or you are just operating on your desktop computer, managing the network results as an important activity to know about how to configure it. Also, these methods are particularly useful if are troubleshooting a network, understanding issues such as conflicts among IP addresses and more.

Here we start reviewing some common commands and specific use. All these commands combined together result as a powerful source to know how to manage the network.

The ping command

The ping command which stands for Packet Internet Groper is widely used to test the activity of a server providing the IP address. Through the ping command you are able to check out if the Ip you are looking for is currently active.

The command works sending the requests through the packages (Internet Control Message Protocol). At the same time, the recipient answers to the message with another Internet Control Message Protocol. The communication may result in problems such as delays that are evidenced launching the command ping. Also, some packages would result as lost during the transmission of data.

Once that the command ping has been typed, it will reiterate the same operation for an infinite time.

Type the command here below to ping google.com:

ping google.com

![A close up of a screen Description automatically generated](images/00050.jpeg)

In each line you can see the result of the ping command.

56 bytes is the default number of data bytes which then 64 bytes for the Internet Control Message Protocol. While the IP address is  ord30s31-in-f238.1e100.net 172.217.4.238. The sequence of consecutive packages is then generated from 1 to n, with the like it follows here below:

icmp_seq=1

Use the “option -c” to avoid repeating endlessly the same operation:

ping -c 4 google.com

The number “4” refers to the packages sent, so the ping command is able to interpret how many packages are expected to be sent and then stop the execution.

The ping command is so important because it allows to quickly check if the server you are trying to reach is working.

![A close up of a person Description automatically generated](images/00051.jpeg)

If you do not receive an answer typing the command “ping” there may be a problem on the network. In some cases, network issues also produce a loss of packages over the connection to the destination. One of the solutions that can be applied is just using the command here below to check the status of the lost packages and see what happens:

traceroute

Another useful option for the ping command, in addition to “-c”, is using the “-i” option. This rule can be used when there is another gateway source like here below:

ping -I eth0 www.yourdomain.com

Also, you can choose form which kind of internet protocol between IPv4 and IPv6 you want to send the ping. The IPv4 and IPv6 with respectively interpreted with -4 and -6.

![A picture containing table, bird Description automatically generated](images/00052.jpeg)

The Netstat command

The netstat command is a great source to figure the statistics of the network. This means checking the if the ports TCP and UDP are open and more. The netstat utility is usually already available in your system. 

Type the following command to see the current version of netstat:

netstat -v

Before digging in-depth the potentials of the netstat command, you should have a clear idea of how the ports TCP and UDP work. In fact, TCP and UDP are the two methods that can be chosen to send packets through a network. What you need to forward is the number of the port, the type of port, and the IP address of your destination.

Just to refresh your memory, TCP stands for Transmission Control protocol and it is the most reliable method between the two. It connects the sender with the receiver, and it waits for an answer from the second one. The connection is established directly between the two and it only stops at the end. On the other hand, UDP stands for User Datagram protocol is a less reliable transmission of data, but at the same time also requires a lower load of work though the network.

In order for a server to communicate with another machine, it needs a port that can be used as listener of incoming connections that have to be accepted from the server itself. Ports can be open or closed depending if there is a service such as a firewall that blocks the transmission of data. One of most common ports used by default for the TCP port is the port 80.

Type the following command to list the TCP ports available as listener which means they accept connections:

sudo netstat -t

![A screenshot of a cell phone Description automatically generated](images/00053.jpeg)

While the option “sudo netstat -u” shows the UDP ports they are listening:

sudo netstat -u

The command with the option “-l” shows the listening ports:

sudo netstat -l

![A close up of text on a white background Description automatically generated](images/00054.jpeg)

As listed in the example here above, there is some important information displayed by the command. Starting with “proto”, the ping command produced the protocol used by the socket, then “local address” which indicates the IP address as well as the port that is listening to, and finally the “state” that specifies “LISTEN”.

Other options that can be used:

*   -n shows the addresses separated by dots
*   -p displays PID (process identifier associated with a connection) and it has to be used with permissions as administrator.
*   -a shows the sockets available for incoming connections

All the options can be used at the same time all together to see the particular results.

To check the statics of a network interface “option  -I”  in the kernel “option -a” :

netstat -ai

With the following command you can check the services, their state and the PID:

sudo netstat -tunlp

Adding “grep” you can filter the ports and see what services are using the specified port 80:

sudo netstat -tnlp | grep :22

![](images/00055.jpeg)

The ifconfig command

Ifconfig is another of most widely used commands by an administrator to configure the network. As the name itself describes, ifconfig deals with the interface configuration, showing the network interfaces that can be used such as eth0, lo, etc.:

ifconfig

![A screenshot of text Description automatically generated](images/00056.jpeg)

As a consequence, using the following command, you are able to see the configuration on the interface eth0:

Ifconfig eth0

Each interface can also be activated or disabled according to your needs.

The commands ““ifconfig up” and ““ifup” work in this way to apply changes.

If the interface is already enabled, anything does not change:

ifconfig eth0 up

Similarly, to disable an interface such as eth0, use the commands “ifconfig down” or “ifdown eth0”:

ifconfig eth0 down

The same ifcong command is also used to assign an IP address to an interface like the wth0:

ifconfig eth0 192.16.20.120

Also, the ifconfig can be used with the command netmask to enable the network mask on a specific interface such as eth0:

ifconfig eth0 netmask 255.255.255.220

While the setting of the same command with “broadcast” sets the broadcast address on a specific interface:

ifconfig eth0 broadcast 192.16.20.120

The MUT, which stands for maximum transmission unit, is the largest part in a unit sent through a network interface. The attribution to the type of interface can be edited, also defining the threshold for the number of packets that can be sent each time.

The example below sets up the transmission to a limit of 800 packets:

ifconfig eth0 mtu 800

Whereas usually the regular process checks if the packets belong to the interface currently in use, there is also an option to activate or disable what it is defined as promiscuous mode. With this type of mode packets are anywhere accepted. The following command in then used for this purpose:

ifconfig eth0 promisc

In opposition to the “promisc” command used to enable the configuration of the of the promiscuous mode, the “promisc” command disables this setting:

ifconfig eth0 -promisc

Another interesting feature is the alias that can be assigned to the interface eth0\. The value is in the same range of the subnet mask. Adding the IP address to “ifconfig eth0:0” you give the alias, while just “ifconfig eth0:0” checks the alias itself.

ifconfig eth0:0 192.16.20.120

ifconfig eth0:0

The simple inclusion of “down” at the end of the command removes the alias assigned to the interface.

ifconfig eth0:0 down

From the command line you can find out what is your MAC address and edit it. MAC stands for Media Access Control and it is the identification number assigned to a network. Adding “hw ether” to ifconfig you are able to change the information.

ifconfig eth0 hw ether AA:BB:CC:DD:EE:FF

The Tcpdump tool

Tcpdump is a utility that works only from command line. It analyzes the TCP/IP packets that are received and sent through a network interface and it decides if they can be stored to be interpreted in the future.

Type the command to see the results:

sudo tcpdump

If you want to limit your search to just a specific type of interface, you can add to the command “-i” to the command “tcpdump”.

tcpdump -i eth0

Through your search you can also filter the number of packets to displayed as output just adding the option “-c”:

tcpdump -c 5 -i eth0

The Route command

Before digging into the command “route” is useful to have an overview of the concept of IP routing. With the term “IP routing” we mean a process where a host reaches another host before forwarding data to the final destination. With this method, the recipient works in between and takes care of the packets received deciding how to sort them before sending them to the final host. It is usually identified with a router that is used by the first host whether the final host is connected or not. In the main step the IP address is checked to see if it belongs to the same network or not. The TCP is then in charge of recreating the information collected over the transmission.

With this overall introduction, keep in mind what is the goal of the command you are learning. Typing the route command you are able to show or edit the routing tables.

The routing tables contain information about how the process of transmission of the packets sent and received, included the details of the network. One of the main features of this command is setting up static routes and interfaces in a network.

As shown in the example here below, you can type the command to access to the current routing tables:

route

![A screenshot of a cell phone Description automatically generated](images/00057.jpeg)

The data reported in the screenshot offer a preview of the routing tables. Following the columns, “Destination” indicates the IP address of the host of destination or the network.

Then, the “Gateway” is expressed as an IP address of the router that filters the data available at the destination. The router, which is the mediator of the transmission, takes decisions in terms of how to send the data received to the final host. “Flags” describes the type of host of the final recipient and it is useful to figure if it is a router or a different device. Also, “Iface” provides the interface that it is used in the network. In the example shown the interface is the common eth0\.

Through the process of routing table, the first host tries to reach the host of destination and names the router that handles the traffic. In this way, the communication can be performed even if the final host is not in the same network of the sender.

The route command has some options that can be added to display the information slightly differently. With the “option -n” you can see the list of the IP addresses in numbers:

route -n

![A screenshot of a cell phone Description automatically generated](images/00058.jpeg)

The IP address “ip-172-31-32-1” is now replaced with the digits “172.31.32.1”.

With the same command you can also set up a default gateway to use in case the final IP address does not belong to the same network:

route add default gw 172.31.32.3

Instead of the IP address the destination would have the word “gateway” displayed under “Destination”.

The following command is used to edit the host:

route add -host 172.31.32.3 reject

The Nslookup command

The command Nslookup, which stands for “name server lookup”, is another great utility to work with the network. You can simply use it to discover the IP address or the domain name.

The data provided by the DNS can be transferred through the interactive and noninteractive mode. While the interactive mode shows a list of the hosts belonging to the same domain, the noninteractive mode shows only the information for a specific host.

The command has the purpose to find problems linked to DNS configurations,

Just typing the command, you are able to use the interactive mode:

nslookup

![A screenshot of a cell phone Description automatically generated](images/00059.jpeg)

After typing “nslookup” it would be asked to enter other information starting with the domain like in the example reported is “google.com”. All the information is then displayed to you for what concerns the server and the IP address. All the time you enter an IP address or domain you request a query that will disclose the information of your search. When the IP address is provided instead of the domain, you are making use of a reverse DNS lookup.

The second method instead is more specific for users who already have knowledge about the topic and know what parameters to look for.

Similarly, you can also request to find information on the MX records. In this specific case you need to add “set type=mx”:

![A picture containing table Description automatically generated](images/00060.jpeg)

As shown in the preview, after entering:

nslookup

You have to enter the filter:

set type=mx

and then the domain:

google.com

In the same way you can find the information about the DNS server typing the type=”ns”:

set type=ns

Further options can be applied for example to see the SOA with the type=”soa”:

set type=soa

![A picture containing bird Description automatically generated](images/00061.jpeg)

As explained previousl, the second method that can be applied to the nslookup is the noninteractive mode. Instead of inserting the parameter separately, at the same time you type “nslookup” you also need to include the domain name as it follows here:

nslookup google.com

or you can ask for a query on the IP address:

nslookup 209.18.47.62

The host command

Given a domain name, the host command can be used to find the IP address or providing the IP address the associated IP address can be found. Just typing the command “host”, a list of options is available:

host

![A screenshot of text Description automatically generated](images/00062.jpeg)

As shown above, without no specific argument passed to the command, options are listed above.

Enter the following to see the IP address of google:

host google.com

![A picture containing table, photo, sitting, computer Description automatically generated](images/00063.jpeg)

As shown in the preview, the address 172.217.10.238 matches the domain name google.com.

Similarly, also the reverse can be found. This means retrieving the domain name of an IP address.

host 172.217.10.238

The “option -C” is able to compare the SOA records on authoritative nameservers:

host -C google.com

![A picture containing indoor, table, bird Description automatically generated](images/00064.jpeg)

The “option -a” stands for ANY and it means that it tries to find any information about the Google host:

host -a google.com

The “option -t” can be applied to look for a specific DNS like ns:

host -t ns google.com

![A screen shot of a computer Description automatically generated](images/00065.jpeg)

The whois command

The whois is able to find information about a registered domain name, IP address, and name servers.

The command whois is a utility used to find information about the whois server you are reaching out. It accepts the requests through the default port which is the 43 and it translates the data received so that can be read in a different format.

Using the command you can list all the information about the registrar of the domain, the domain status, the name servers, expiration date:

whois google.com

![A screenshot of a cell phone Description automatically generated](images/00066.jpeg)

Also, the same command can be used to get the information given an IP address:

whois 209.18.47.62

But how this information can be provided to you?

The ICANN is a non-profit organization that manages the IP address assigned to each domain name and they work with the registries. They are in charge of the domains such as .com. Below this level, registrars operate with the final customers such as GoDaddy, TuCows, and more. As a result, anyone who would like to register a new domain will apply for a registration to common registrars.

Using the command “whois google.com” you send a request for a query to the listening port 43 which provides a series of information collected from the registry. 

Additional information is provided to you if in the same query you also include the registrar where the domain is registered:

whois -h whois.markmonitor.com google.com
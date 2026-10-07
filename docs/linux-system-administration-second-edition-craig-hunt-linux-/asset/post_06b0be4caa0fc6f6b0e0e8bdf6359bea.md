
obtaining or creating the software to run the backups unattended. Added features, like a script that e-mails you when the backups finished, also provide some peace of mind. When the system crashes there is data that is not contained in a backup, other methods of data recovery are required. Your familiarity with these methods will help you get through troubled times with less frustration. Backups and disaster recovery are covered in Chapter 9, "Backing Up and Restoring."

## Capacity Planning

As a Linux system administrator, you'll need to be aware of the limitations imposed by the hardware and software installed in your system. You'll need to watch the network traffic to determine when high usage creates a need for new hardware/software to be added. You'll need to watch disk space usage to ensure that you have sufficient printing and backup resources for the number and type of users in the system. We'll discuss each of these elements in Chapters 6, "Filesystems and Disk Management," 10, "Printers and the Spooling Subsystem," and 12, "TCP/IP Linux Networking."

## Network Administration

Most companies that you work for have an internal network (intranet) and will want connection to the Internet. The system administrator is the person who sets up, maintains, and troubleshoots these networks. Chapter 12, "TCP/IP Linux Networking," deals with networking topics and Chapter 18, "Troubleshooting Your Linux System," contains tips for troubleshooting network problems.

## When You Have a Minute...

There are so many tasks that are performed by a system administrator that it is impossible to mention them all. Our duties include building network clusters, installing a network, configuring routers, answering user questions, assembling tables upon which the system will sit, and almost anything else you can think of. A system administrator who appears to have free time is a game. Never mind that you are compiling a kernel on a remote machine while accidentally deleted files from a backup. Users, managers, salespeople—all they have the right to interrupt you and start you off on a wholly unexpected task if you're not obviously doing something already—and sometimes when you are able. Life for a system administrator is never boring.

## Tools of the Linux Administrator

Many tools and techniques are available to make the job of system administration less maddening, and seasoned administrators usually have a suite of them that have proven useful. Some of these are commonly used Linux commands, while others are scripting tools or methods that help to automate your tasks. Whatever they are will prove invaluable to you, as a system administrator. There is a number of Internet sites that allow you to download some of these software tools and try them yourself. A site that provides access to a number of tools specifically for Linux may be found at http://www.linuxapps.com/

Most Linux distributions contain some tools that the distributors have found to be both stable and useful. Unfortunately, each distribution of Linux has its own set of "essential" tools, making it more difficult to switch between distributions. Worse is the fact that Red Hat and some other distributions are in a state of flux, developing new system administration tools and potentially existing ones rather frequently. We escape this problem by using a tool called Webmin, which we'll discuss later in this chapter. However you get them, you will find that they are essential to happy system administration. Here is a brief list of tools that you shouldn't be without.

### Commands

There are hundreds of commands you can use to perform your administrative work. These commands may be compiled programs in C or some other language, programs written in an interpreted language such as Python or Perl, or shell scripts that exploit the shell's inherent capabilities to perform some task. Wherever you type the command represents, each command is executed by entering the command and any applicable parameters on the Linux command line or by clicking an icon which is mapped to that command. We will discuss specific commands in Chapter 4.

### Linuxconf

Practically every flavor of Unix has several individual tools that perform a single administrative task, but also have a general tool that combines many of the individual capabilities into a single interface. IBM has its utility; Solaris uses the adminintool. Until recently Red Hat Linux used Linuxconf as its primary system administration tool. A product of the GNOME project, Linuxconf was designed to perform many administrative duties. Few tools handled so many types of configuration tasks as the Linuxconf utility, but unfortunately, Linuxconf never reached the state of reliability needed by a do-it-all tool. We'll mention Linuxconf occasionally throughout this book since it is still in use, but our feeling is that there is a better do-it-all tool.

### Webmin

Webmin is a tool, owned by Caldera Corporation, which allows any system administration tasks to be performed within any browser that supports tables, forms, and Java. Available from http://www.webmin.com/, it is governed under the BSD license, which makes it freely obtainable and modifiable for commercial and noncommercial use. We prefer Webmin's consistent and reliable interface to manage user accounts, network and Domain Name Server configuration, PPP setup, mail server and client configuration, Samba, NFS, Apache configuration, and filesystem tool. The main screen of Webmin is shown in Figure 1.1.

| Action | Status | Description |
| :--- | :--- | :--- |
| access | Yes | Run cron jobs that leave alive or to exit |
| battery | Yes | battery is used for monitoring battery status and paging you via email. It can also be used for shutting down the machine when the battery is low |
| named | No | Restart service for Apache daemon [PID 1234] |
| restart | Yes | Restart based on configuration file of the time specified when ready or may, and match commands when the load is over limit |
| logout | Yes | Automate logouts on demand |
| cron | Yes | cron is a Unix program that runs specified programs at scheduled times, while cron add a number of features to the crontab file and allow for complex configurations |
| create | Yes | provide access to Dynamic Firewall |
| update | Yes | update the firewall rules via the Midnight Controller. It also moreover allow cut-and-paste operations, and support for multiple rules at once |
| delete | Yes | delete firewall rules |
| restart | Yes | restart the firewall |

Figure 1.1: The Webmin main screen (Linux Router)

As the name implies, Webmin is a web-based system administration tool that can be configured to be accessible from the localhost, within the local area network (LAN), or outside the LAN as well. We will demonstrate Webmin's many uses in various chapters throughout the book.

### Special-Purpose Shell Scripts

Many day-to-day tasks, whether simple or complex, are accomplished by a specially designed shell script. A shell script is a list of commands batched together in a file so they can be executed on demand. As Linux system administrators, we have written many shell scripts, and you will see Chapter 17, "Making Your Job Easier with Scripts," is dedicated to this topic.

### System Logbook

To maintain some semblance of sanity, you need to keep your network—and your administrative activities—organized. Many system administrators, at least ones who have learned from previous mistakes, keep a journal of the overall network configuration and the operating system and software configurations for each computer. The lack of such preparation makes an unexpected reinstall a painful experience. If you need to use your backup tapes to reinstall a system, it will be a critical factor, since you understand the time involved in such a process. You can minimize the time required by knowing exactly what you had up on that system. A journal of each change you made to the system is available at this point. You must keep the journal as closely as your backups, because it is the combination of the two that will allow you to reinstall and reconfigure quickly and efficiently.

We recommend that you buy several basic logbooks to be used exclusively for journal-keeping. The hard-backed composition books used for English classes are particularly good. They are available in most grocery stores and in any office supply store. For each one computer, or for a large network, for each class of computer. The books are cheap, and keeping one system’s journal separate from another system’s journal makes it much easier to keep track. Think about what separation makes sense in your system. If you can keep different categories of notes in

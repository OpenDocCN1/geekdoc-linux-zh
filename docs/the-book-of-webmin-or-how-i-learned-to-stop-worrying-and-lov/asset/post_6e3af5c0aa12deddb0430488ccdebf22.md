
![](img/d84604054810a13cacfdac212ebee2f7_89_0.png)

Figure 5-7. Create Cron Job

In Figure 5-7, I've created a cron job that is run as a user named backup (a user I've created just for such tasks). The job is Active, so it will run at the specified times. The command that is being run is a simple tar command line to back up my complete /etc directory to a tarball in /home/backup. While this is not a terribly sophisticated backup system, it gets the job done without much complexity. Furthermore, a simple periodic backup of important files is far better than no backup at all. In this case, it is made slightly more effective by the fact that /etc and /home are partitions on two different hard disks.

## Software Packages

The Software Packages module allows an administrator to perform software upgrades and package maintenance via a quite friendly interface. Although the actual implementation can vary quite a lot depending on which software packaging system your operating environment uses, Webmin masks most differences, and the overall usage of each is very similar.

### Introduction to Package Managers

Most modern UNIX systems feature a package manager. The concept of a package manager may be foreign to new users migrating from Windows operating systems, in which software is installed by one of a number of installation processes. There is usually no record kept of the locations of installed files and no easy way to remove all of them if the software is no longer needed. While some installation utilities are more effective and reliable than others, all of them have difficulty making wise decisions about software dependencies and available library versions. The lack of a unified package manager has led to an entire product category devoted to removing old software installations because of these problems.

A package manager solves this problem, and quite a few other problems that aren't obvious until you've lived with one for a while. With a package managed system, you never have to wonder where a given file originated, or whether a given library or system component is installed. Finding the version of any installed package is quick and easy, and upgrading old packages to new versions can usually be done without fear of overwriting configuration details. So, now that it is clear why package managers are great, it is a good time to talk about how you can use your package manager from Webmin.

### Supported Operating Systems

Webmin provides a mostly consistent frontend to most major OS package managers. The supported operating systems include RPM-based Linux distributions, like Red Hat, SuSE, and Mandrake; deb-based systems like Debian; systems using the pkg-style tools like Solaris, Slackware Linux, and SCO Unixware and OpenServer; and the HP/UX and IBM AIX package managers. A notable exception to the list of supported operating systems is Irix. Though it has a package manager, it is not currently supported by Webmin.

### Using the Package Manager

Webmin presents a simple interface that provides the ability to install packages, search currently installed packages, view the installed packages, and remove packages (Figure 5-8). Additionally, it is possible to identify the package from which a specified file was installed.

### Installed Packages

To search for a package, enter the package name here. A package name is the name of the file that was installed, without the version number or file name extension. For example, on a Red Hat system, the Postfix mail server package is simply called postfix. When searching, Webmin will return all packages that have the search term as part of the package name or as part of the package description. This usually makes it easy to find what you're looking for even if you don't know the exact package name.

To view a list of all installed packages, click the Package Tree button. When applicable, packages will be divided into their appropriate categories as designated by the packager.

![](img/d84604054810a13cacfdac212ebee2f7_91_0.png)

Figure 5-8: Software package management on Solaris

### Install a New Package

To install a new package (Figure 5-9), specify its location, either a local file path or a URL, or by uploading it from your local machine using the Browse option. The package will be identified, the title and description will be displayed, and the installation path may be specified for relocatable packages.

![](img/d84604054810a13cacfdac212ebee2f7_91_1.png)

Figure 5-9: Install package

It may also be possible to specify options regarding dependencies, installation scripts, documentation, filesystem size, and so on. Generally, the default options will work fine.

### Identify a File

Often it is useful to know which package provided a particular file on the filesystem. Simply enter the path to the file you would like to find information about into the text field and click the Search for button.

### Edit Package

Clicking a package name provides access to the **Edit Package** page (Figure 5-10). This page includes package details such as the description, the category or class of the package, the date of installation, and so on. Here you can list the files contained in the package as well as uninstall the package.

![](img/d84604054810a13cacfdac212ebee2f7_92_0.png)

Figure 5-10: Edit Package

## System Logs

System Logs provides a method for controlling the syslogd daemon used on most UNIX system to provide standard logging functions. The module opens with a list of all currently existing logs. By clicking the **Log destination** of a log file, you can edit the logging properties, as shown in Figure 5-11. On the editing page there is also a **View log** button that allows you to view a configurable number of lines from the end of the log file. It also allows a constantly refreshing log view if selected.

This module edits the `/etc/syslog.conf` file and provides a pretty easy way to check up on your logs remotely. And even though the module is designed primarily for syslog logs only, it is flexible enough to allow you to view other types of logs as well. For example, the web-caching proxy Squid doesn't use standard **syslog** facilities, so doesn't fall under the control of syslogd. Nonetheless, I like to be able to check up on a running Squid, so I add an entry on all of the boxes I administer to allow me to watch those logs in Webmin. To create a new syslog entry, click the **Add a new system log** link.

![](img/d84604054810a13cacfdac212ebee2f7_93_0.png)

Figure 5-11: System Logs

### Adding a System Log

The Add System Log page is divided into sections labeled **Log Destination** and **Message types to log**.

### Log Destination

The log destination options below specify where log entries will be written, and whether a particular log is active.

### Log to

This option configures the destination of the log file. Syslog can log to a file, a named pipe, a remote syslog server, or the console of some or all local users.

### File

The log entries will be appended to the file name specified. A complete path should be given. Historically, system logs are stored in `/var/log`. The **Sync after each message?** option will cause the syslog daemon to flush to disk after every entry, therefore overriding the disk I/O buffering provided by the operating system. This can be detrimental to performance in circumstances in which logging occurs at a very rapid rate, such as the mail log on a very busy mail server. In most circumstances, the integrity of the log is far more important than avoiding the small amount of disk activity system logs generate.

### Named pipe

The concept of pipes is fundamental to the UNIX Way, or the philosophy of combining small tools to perform large jobs efficiently and flexibly. Most UNIX users are familiar with the standard command-line pipe, which allows the output of one command to be the input of another command. A named pipe expands upon that and allows output to be sent to a pipe that is located within the normal filesystem under a normal file name. Or, to put it another way, the output of syslog will go to whatever program is accepting input from the named pipe. While named pipes and their usage is beyond the scope of this book, I will point out a few resources to get you started on the subject. Many modern UNIX

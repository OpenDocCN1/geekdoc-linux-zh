
# Graphics, Multimedia, and Productivity Tools
PART IV

Next, find out the structure of the table called names:

```
vegetable=> \d d names
```

| | Field | Type | Length |
|---|---|---|---|
| veggie_name | varchar() | 40 |
| quantity | int4 | 4 |

Now that you have created a database and a class, I will leave populating it with data to you.

Again, an Internet search will yield great results in searching for SQL tutorial or a similar phrase. The PostgreSQL documentation should also be found on your system (/usr/doc/) and is freely downloadable from http://www.postgresql.org.

# MySQL

In addition to the full-featured PostgreSQL, you might consider MySQL. MySQL is a robust, SQL-compliant database with lots of features. You can get it at http://www.mysql.org.

MySQL's best feature is its sheer speed. The database is designed to handle data quickly and efficiently and minimize overhead processing when possible.

Many Web sites use MySQL as a database back end, even the very popular http://slashdot.org. There are a number of modules available to directly embed SQL calls into popular programming languages such as Perl and C.

# Obtaining MySQL

MySQL should be downloaded directly from the http://www.mysql.org Web site. This will allow you to obtain the latest version of the database as well as a number of tools for managing and accessing the database. Along with the various tools, be sure to download the extensive documentation available on the site in a number of formats (HTML, PostScript and so on). The docs answer a lot of your basic questions and are the full key to the various APIs for the database.

# Productivity Clients and Office Suites for Linux
CHAPTER 28 897

There are links on the site to download the database and tools as source code, compiled binary, and also pointers to RPM format binaries. Choose the method of installation that best suits your abilities and situation. I have used the RPM installation and it works very nicely; however, compiling from source code gives you full control of all installation options.

Here are the pieces you will need:

- MySQL-3.xx
- MySQL-client-3.xx
- MySQL-devel-3.xx

The 3.xx is the version number, and may look something like MySQL-3.22.25-1. Follow the advice of the MySQL Web site and choose the version that suits your needs. Stable and development versions are both available and clearly marked.

# Using MySQL

MySQL follows the same client-server model as PostgreSQL. That is, you have a client process that makes database requests, and a server process running that handles these requests. These requests are not required to be on the same machine. Remote clients, with the correct permissions, can be located just anywhere.

![](img/cbac72550c7126a22162e94d91a0c360_932_0.png)

After the installation, make sure that the MySQL server process is running. Use a tool like to verify this.

MySQL has an interactive tool, like the PostgreSQL monitor, which you access by simply typing mysql.

Once in the monitor, you may use standard SQL statements to manipulate databases, tables, and data. If you get stuck for a command, type help.

# GnomeCard

GnomeCard is a basic, but rather handy, address book program that displays contact information in a configurable list format, with a sidebar showing detailed information about a highlighted item. It is provided as part of the GNOME desktop environment.

# Obtaining and Installing GnomeCard

You can find the latest release of GnomeCard on the GNOME Web site (http://www.gnome.org). Install the GnomeCard applicable to the format you obtained. If it is a packaged binary, such as RPM, use the Red Hat Package Manager.

# Configuration

GnomeCard is quite usable initially and provides little in the way of customization. The only real change you can make is the columnar display. Choose Settings, Preferences to make changes.

# Using GnomeCard

GnomeCard has a nice toolbar (see Figure 28.21) that controls most of its functions. The functions also have specific keystrokes, allowing you to speed up your use. The functions include opening and saving a GnomeCard file, adding, modifying, and deleting a card, and navigating through existing cards. A simple Find function provides a limited search capability.

**Figure 28.21**
The GnomeCard address book.

![](img/cbac72550c7126a22162e94d91a0c360_933_0.png)

# Appointments and Scheduling Clients

Even if you have great-looking reports and reliable data, you still have to make it to meetings on time. This section takes a look at a few appointment and scheduling tools available for Linux.

# KPilot

The PDA (Personal Digital Assistant) had quite a rocky start in corporate America. Hokey interfaces, tiny screens, and miniscale storage capacities all kept the PDA from realizing its true potential as a portable information tool.

# Enter the 3Com Palm Pilot.

The Palm Pilot has revolutionized the use of the PDA and made it almost as indispensable as the cellular telephone for busy people. Since the Palm Pilot is widely used and vastly popular, it only makes sense that there exist tools that allow you to back up the data on your PDA and synchronize its files with your laptop or desktop computer. KDE offers the KPilot utility to perform these functions.

# Obtaining KPilot

KPilot comes as part of the standard KDE distribution. You don't really have much to get it. Check out http://www.kde.org for new versions.

# Configuring KPilot

KPilot has two simple screens (see Figure 28.22) that are displayed during its use. The first tab, General, allows you to define who you are, what connection speed to use, and how to connect. The second tab may be ignored for now. It is mainly used for importing and exporting addresses from text files.

# FIGURE 28.22
The KPilot options.

![](img/cbac72550c7126a22162e94d91a0c360_934_0.png)

KPilot uses a daemon program that allows the KPilot GUI to be started by simply inserting it into its cradle and pressing the Hot Sync button. This synchronizes your files.

# Using KPilot

> Tip
> One important item that you want to think about: the Local Overrides option. When the same record has been modified on both the Palm Pilot and your desktop machine, only one version can be used when synchronizing. Choosing this option causes the local copy of the record to override the copy on the Palm Pilot.

Your Palm Pilot cradle should be attached to a serial port on your computer. As the root user, add a symbolic link called /dev/pilot; it points to your proper serial port. The permissions for the serial port should be read/write for all (666). Use the chmod command to do this.

Use this code to add a link. The Palm Pilot cradle is attached to /dev/cua:

```
# ln -s /dev/cua /dev/pilot
```

Use this code to change permissions:

```
# chmod 666 /dev/pilot
```

On your first use of KPilot, you should perform a full backup (File, Backup) of your Palm Pilot. This copies files into a directory on your local machine and provides a baseline of files for future synchronization. This may take some time, depending on the amount of data you have in your Palm Pilot.

KPilot also has a couple of application screens that allow you to move specific items between your local machine and the Palm Pilot. Choose the specific application from the list; files for the specific application are shown. You can then choose to import, export, delete, or edit records.

# KOrganizer

KOrganizer is the calendar and to-do list applet provided with KDE. It is rather simple and works like other calendars such as Gnome Calendar or Ical. KOrganizer uses the vCalendar file format as its native file format. This allows calendar interchange with other programs.

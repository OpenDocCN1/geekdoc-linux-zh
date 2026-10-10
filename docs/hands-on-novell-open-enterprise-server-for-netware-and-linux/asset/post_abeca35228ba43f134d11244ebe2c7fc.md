
![](img/840007e8f98ea6653e5877e945c27dc6_546_0.png)

Figure 13-9 The man section (1) page for the ls command

### Table 13-3 Section options for the man command

| Section Number | Description |
| :--- | :--- |
| 1 | Executable programs and user shell commands; the default section number |
| 2 | System calls |
| 3 | Functions and library routines |
| 4 | Device files |
| 5 | Configuration files and file formats |
| 6 | Games |
| 7 | Macro packages and file formats |
| 8 | System administration commands |

For example, to view the configuration files and file formats for the crontab command (see Figure 13-10), enter the command "man 5 crontab."

![](img/840007e8f98ea6653e5877e945c27dc6_546_1.png)

Figure 13-10 The man section (5) page for the crontab command

# Using Info Pages

Linux has another source of command documentation called **info pages**, which often provide a more current version of command documentation and can be read by using the info command, as shown in Figure 13-11. In SUSE Linux, info files are stored in the /usr/share/info directory and have the following advantages over man pages:

- Info files use a standard structure in the documentation layout.
- Info files contain specific sections that can be accessed directly from the table of contents, compared to using section numbers with the man command.
- Info file sections can be linked to form a complete document.

![](img/840007e8f98ea6653e5877e945c27dc6_547_0.png)

You can use several command keys, listed in Table 13-4, to move around info pages.

### Table 13-4 Common info command keys

| Command Key | Description |
| :--- | :--- |
| Spacebar, Page Down | Page down one screen |
| Backspace, Page Up | Page up one screen |
| b | Move cursor to the beginning of the info page |
| t | Move cursor to the next reference |
| h | Display help |
| q | Exit the info page |

# Creating Users and Groups from the Command Line

Most network administrators find it more convenient to create and manage user and group accounts with YaST, but the Certified Linux Professional (CLP) certification requires creating user and group accounts from the command line with the useradd and groupadd commands. Being able to use command-line utilities has certain advantages, such as creating users from script files and working on other Linux systems that don’t have the YaST utility installed. Command-line utilities use parameters to specify additional information and options. Parameters usually take the form of a letter preceded by a hyphen. To learn more about parameters for command-line utilities, use the man command. For example, Figure 13-12 shows an example of using the man command to view information about parameters for the useradd command. In the following activity, you learn how to use the adduser and addgroup commands to create new local users and groups on your SUSE Linux server.

![](img/840007e8f98ea6653e5877e945c27dc6_548_0.png)

## Activity 13-3: Creating User and Group Accounts from the Command Line

**Time Required:** 10 minutes

**Objective:** Create local user and group accounts with command-line utilities.

**Requirements:** Completion of Activity 12-1 (Linux installation), a local Linux user account created during Activity 12-1, and access to the root user password

**Description:** Eric Kenton wants you to show him how to create user and group accounts with the Linux command-line utilities. In this activity, you use man and info pages to look up documentation on the useradd and groupadd commands, and then use them to create an ITMgrs group and user accounts for the IT Department.

- 1. If necessary, log in to your SUSE Linux server with the user name you created for yourself during Activity 12-1.
- 2. Open a terminal session.
- 3. Switch to the root user by typing **su**, pressing **Enter**, typing the password for your root user account, and pressing **Enter** again.
- 4. Type **man groupadd** and press **Enter** to display a man page on the groupadd command. Read the man page, and then type **q** to quit and return to the command prompt.
- 5. Enter a groupadd command to create a group named **ITMgrs** with the default options. Record the command you used: _________________________
- 6. Type **info useradd** and press **Enter** to display information on the useradd command. Read the info page, and then type **q** to quit and return to the command prompt.
- 7. Enter a useradd command to create a user account named **ekenton** that belongs to the ITMgrs group and has a home directory in the /home path. Include the -m parameter to create the home directory and the -c parameter to enter **Eric Kenton** as the full name. Record the command you used: _________________________
- 8. Type **cat /etc/passwd** and press **Enter** to display the contents of the passwd file. Notice that information for each user account is stored on a separate line. Record the line in the passwd file that shows the account for your ekenston user: _________________________
- 9. Type **exit** and press **Enter** to exit the su shell, and then type **exit** and press **Enter** again to return to the command prompt.
- 10. Use the procedure in Step 11 of Activity 13-1 to change Eric Kenton’s password restriction to 90 days.
- 11. Exit YaST and log out. Leave your system running for the next activity.

# Using Linux Online Help

Sometimes you need more detailed information about a command or procedure than the *man* or *info* command provides, or you want to learn how to perform an administrative task or solve a technical problem. The developers of Linux and other open-source software have always shared software documentation online for everyone’s use. You can find a wealth of useful information online, but remember that software documentation is often written by developers who assume that you’re familiar with the documentation available for other Linux commands. As a new Linux administrator, you should expect to see many details that you don’t understand at first. Going through this chapter and reading additional material will help you clear up many of these details, however.

Matt Welsh started the Linux Documentation Project (LDP) in the early 1990s. The LDP was the first major effort to offer Linux documentation in a variety of formats. Currently, it has more than 6000 pages of information available free on the Internet. Many network administrators find the HOWTO documents to be the most helpful part of the LDP. These documents cover topics such as sharing files between Linux and Windows XP or accessing network printers. In addition, mini-HOWTO documents focus on narrower subjects, such as configuring a DHCP server. A good place to begin researching the LDP documentation is at www.tldp.org.

When you have a challenging Linux question, such as configuring a Linux driver, you can also try searching for the answer at the Google site. Entering “Linux driver Intel(R) PRO/1000 MT Mobil,” for example, might return several messages from Linux administrators discussing how to use this network card driver. Table 13–5 lists some Web sites that you might find useful in learning more about the world of Linux. In the following activity, you investigate some of these sites to learn more about accessing online help with Linux.

### Table 13-5 Linux documentation Web sites

| Site | Description |
| :--- | :--- |
| www.linuxjournal.com | A companion Web site for the monthly magazine *Linux Journal* with additional Linux links and information |
| www.linuxmagazine.com | A technical companion Web site for the monthly *Linux* magazine |
| www.linux.sys-con.com | A business-oriented online magazine with interviews, links, and technical information |
| www.lwn.net | A collection of weekly news articles |
| www.linuxtoday.com | Recent Linux news items |

## Activity 13-4: Accessing Online Help

**Time Required:** 10 minutes
**Objective:** Find online help information.
**Requirements:** Access to the Internet

**Description:** Linux online documentation is a great resource for learning and working with the Linux OS. In this activity, you practice using some online sites to find information.

- 1. If necessary, log in to your SUSE Linux server with your user name and password.
- 2. Start your Web browser and explore the URLs listed in Table 13-5. Record your favorite site:
- 3. Exit your Web browser and log out. Leave your system running for the next activity.

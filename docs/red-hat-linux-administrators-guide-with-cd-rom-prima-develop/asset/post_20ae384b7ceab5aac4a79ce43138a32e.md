
Linux software program; third, to spread my directories across separate partitions. Fortunately, I had all my important documents and programs located in both the `/home` and `/usr/local` directories, each in their own respective partition. During the reinstall process, I was able to choose these directories that I wanted to reformat and reinstall. For the average user, only the `/`, `/usr`, and `/var` directories need to be reinstalled. The other directories can be left untouched. Linux simply overwrites the chosen partitions and reinstalls the binary files.

Linux takes great pains to make installation and reinstallation as easy as possible. Unlike other proprietary operating systems, Linux allows you to reinstall the complete operating system directly from the CD without compromising existing software. Some believe a good cleanup and periodic reinstall helps to keep disk use down. These activities flush out older links and update the system to the latest compilers and libraries. Careful planning before installing Linux can help circumvent later problems and make the system run more efficiently.

## Installing the Software

You have now familiarized yourself with the hardware and learned what Linux supports. Now, after you have partitioned the drives acceptably, Linux will prompt you to begin the install routine. Red Hat offers you several choices, even before the partitioning process, to choose a Workstation, Server, or Custom option. The first two options are fairly standard, though they can install up to 600 megabytes of programs.

### Defining the Installation Type

The first option, or what is called the Workstation installation, will automatically erase all Linux partitions from the hard drive(s), while the second option, Server, will erase *all* partitions from the computer’s hard drive(s). Users should select the third option, Custom, even if they consider themselves Linux neophytes. This option allows for better management and control over the creation of partitions and the selection of programs. There really is no difference between this and the other two alternatives except that with Custom you can choose any and all of the packages that you want.

From here you will be prompted to create partitions and to set the mount points for each. In other words, you need to ensure that each partition has its own distinct directory, as was demonstrated earlier. Red Hat will offer several different choices as to the directories or partitions you can install. The amount of disk space that each partition requires depends upon the computer's function. If you are installing for the first time, you should probably opt for creating only two partitions: root (/) and swap. Once you have decided on the partitions, you can select which partitions to format. If this is a new installation, all partitions should be wiped clean and formatted for the Linux native file system. However, if this is a reinstallation or if you wish to retain the information on existing partitions, then only /, /usr, and /var need to be reformatted. You can choose additional points to format, but this is entirely up to you. Perhaps the best teacher, in this case, is experience. (Besides, I consider installing Linux one of the more enjoyable tasks working with computers.)

### Choosing Your Packages

Once you are ready to install the programs and begin formatting, you will be prompted to choose the packages you want to install. Red Hat is the leader in precompiled source code or binary packages known as *RPMS*. RPM stands for Red Hat Package Manager. The Package Manager portion allows a Linux user to automate the installation of each program fully along with documentation and supporting libraries. The package side of RPMs have doubtless made Linux simpler to install and easier to configure. Not only do they make installing programs simpler, but removing or upgrading them is even less a chore. No longer do you have to worry about leftover files or broken links when you remove or upgrade a file. The RPMs take care of all that for you. Again, unlike proprietary software, Red Hat does not require that you step through a series of wizards or consult a database to remove a program. A simple one-line command does it all for you. A more complete explanation of RPMs is covered in Chapter 11, “Installing Additional Programs.”

Red Hat has carefully divided all the available packages into marked categories or divisions such as Networking, Development Programs, and Daemons. This helps you to define the role of your Linux machine (or Linux box as many advocates like to term their computers running Linux). Depending on the type of interface that you select when installing Linux, whether it be a full GUI or a more DOS-like install, you may be able to select an entire range of programs rather than having to select each program individually or tediously scroll through a list of options that you may or may not want.

What you choose depends again entirely on the purpose of the machine. If the Linux box is dedicated to functioning as a web server, you can quickly and easily install many of the programs necessary by selecting the appropriate category. By the same token, if you opt for a more complete range of programs, you can easily do so by choosing the requested category either at the outset or after paging through each subtopic.

- **TIP**

  Be sure to read the description of each package before installing. Many programs might be completely superfluous to your needs and will only take up unnecessary space. Games are one category that can quickly eat up more space than necessary. Calculate available space and the amount consumed by the packages if drive space is at a premium and only a limited install will work. The latest Red Hat will display the amount of drive space needed for all packages before installing.

Choosing what packages to install is not always so intuitive. Red Hat offers explanations of what each program does and where how it functions in terms of category; whether it is a utility, a game, a library, or developmental program. However, as also seen in the *man*, or manual pages, a concise overview of how each program operates and the command-line options, the explanations provided can prove cryptic. For the novice user, this can be rather frustrating. Often, new users opt for a minimal install and then are unable to compile certain programs afterward because the necessary libraries or dependent programs were unavailable. Understanding each program's function is extremely useful.

There are a couple ways new users can familiarize themselves with the available packages. Red Hat allows you the option of highlighting the binary package and then either clicking the Help button or pressing the F1 key to bring up an explanation. The latest GUI install will display the program's function in a caption below the package names and groupings. If you read the caption carefully, it usually will state not only the package's purpose but what other packages may also be dependent and what other packages this binary either supports or complements. When installing, it is always better to err on the side of installing too many programs rather than installing too few, if you have sufficient drive space not only to install the desired programs but also to do work on the machine afterward. You can always uninstall programs later, but it can sometimes prove difficult to determine what programs require installation later.

If disk space is not in short supply, choose a full install. This way you are guaranteed to have all the needed libraries for most any program that you choose to install later. One comforting thought is that even if you choose the most minimal install, Linux will run on the machine. It will boot up, display a prompt, and allow for some very basic functions. If you purchased a release that came with a manual, either on disk or in hard copy format, you should read the distributor's full description as well.

## Exploring the Installation Packages

Table 1.4 shows some of the possible package categories available in the latest Red Hat release along with a brief description of each. The more substantial sections of the install are divided into larger units and then into subcategories.

### Table 1.4 Installation Packages

| Category | Description |
|---|---|
| Applications | These are the main applications that will be needed by Linux. |
| Communications | This section has fax, IRC, and modem programs. |
| Databases | This section includes, postgresql, one of the better open-sourced database programs available. |
| Editors | This section includes various text editors such as emacs, vim, joe, and jed. These are extremely useful for editing text documents on the server itself. |
| Emulators | This section includes dosemu and related programs will allow you to run DOS-based programs under Linux. |
| Engineering | This smaller section deals with scientific applications. |
| Graphics | These programs assist in editing and manipulating images via the command line. |
| Mail | This section features simple mail clients for checking and managing mail from a terminal window. |
| Math | These programs handle mathematics. |
| Networking | This section features tools for managing network resources. |
| News | This section includes various programs for reading and circulating newsfeeds and groups. |

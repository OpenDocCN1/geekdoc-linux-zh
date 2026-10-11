
## 10 Linux Boot Process and Runlevels

- **Terms you'll need to understand:**
  - Boot process
  - Master boot record
  - Runlevel
  - Sector
  - Signal
  - System initialization
- **Techniques you'll need to master:**
  - Understanding the boot process
  - Booting into various runlevels
  - Understanding runlevels
  - Configuring runlevels
  - Shutting down a system
  - Making a boot disk

> This is the formal beginning of the material for Exam 117-102.

In this chapter we'll discuss the Linux boot process, the runlevels, and how to configure your system to boot the correct level with the correct services running.

### The Linux Boot Process

The Linux system's boot steps are similar across distributions, except maybe for Slackware and the BSD variants. In the following list I walk you through the boot steps and give some exam tips you can use during this process:

1. Turn on the system power.
2. The basic input/output system (BIOS) code loads and looks for a valid boot sector.
3. The BIOS loads the boot sector from a floppy disk, HD, or CD-ROM according to the seek order.
4. The master boot record (MBR) is read; it's contained in the first 512 bytes of the first sector of the first or active hard disk.
5. Any boot loader code found is executed.
6. If using LILO (Linux Loader), the menu code (usually in /boot/boot.b) is shown. The prompt for LILO is either `lilo:` in text mode or a graphical menu of choices.
7. The user selects or types in a choice, or the boot loader times out and begins to load the default entry.
8. If you select a Linux image, the path to load the Linux kernel is read and the compressed kernel is executed.
   > If another image type is selected, such as a dual-boot to Windows, the first 512 bytes of that partition are read for the NTLDR or whatever that OS uses to initiate the system.
9. When the Linux kernel is loading, it initializes the devices, loads any necessary modules, looks for the initial RAM disk (initrd), and loads

## Exam Prep Questions

1. Which of the following steps is most likely to require a user to be the root when installing software from a source tarball? (Choose the best answer.)
   - A. `make dep`
   - B. `make clean`
   - C. `make install`
   - D. `make mrproper`

   Answer C is correct because the `make install` operation typically attempts to write software to directories writable only by the root user. Answers A, B, and D are correct steps of compiling software but access only the local directories and can be performed by any user.

2. In the blank below, enter the full path of the directory in which a package is placed when it has been built with the `rpm -b` process on a default Red Hat Linux machine:

   The correct answer is `/usr/src/redhat/RPMS/i386`. There are no alternative answers.

3. Which of the following commands shows the revision history for a software application from the package file on disk?
   - A. `rpm --revision tree-1.2-7.i386.rpm`
   - B. `rpm -qp tree-1.2-7.i386.rpm --changelog`
   - C. `rpm -qc tree-1.2-7.i386.rpm`
   - D. `rpm -qlp tree-1.2-7.i386.rpm --showrev`

   Answer B is correct because the combination of the `-qp` and `--changelog` options shows the changelog or revision history for a package that's on disk. Answer A is incorrect because there is no such thing as a `--revision` option for the `rpm` command. Answer C is incorrect because there isn't a `-p` option to query the package on disk, nor does `-qc` show the required information. Answer D is incorrect because the `-qlp` option shows the files in the package, not the revision history and there isn't a `--showrev` option to the `rpm` command.

4. In the blank below, enter the full path and filename to the file that's produced by the lccnf program after it's run and has processed all the library files on the machine:

   The correct answer is `/etc/ld.so.cache`. There are no alternative answers.

5. What is the purpose of running the **ldd** program?
   - A. Rebuilding links to library files
   - B. Creating a link to a library file
   - C. Displaying a program's required libraries
   - D. Reading a program's library capabilities

   Answer C is correct because the **ldd** program, when used with a program name as the argument, shows the necessary libraries for the program's functionality. Answer A is incorrect because **ldconfig** is used to rebuild links to library files, not **ldd**. Answer B is incorrect because creating a link to a library file is done by the **ldconfig** or **ln** command, not **ldd**. Answer D is incorrect because the **ldd** command does not read a program's library capabilities; instead it reads its dependencies.

6. Which variable is used to provide additional library support and is also considered to be a security risk? Please enter the variable name only in the blank below:

   `LD_LIBRARY_PATH`

   The correct answer is **LD_LIBRARY_PATH**. There are no alternative answers.

7. Which of the following is a valid cause to receive the error message `error: cannot get exclusive lock on /var/lib/rpm/Packages`? (Choose all that apply.)
   - A. Attempting an **rpm** install command as non-root
   - B. Performing multiple remove commands simultaneously
   - C. Performing multiple verification commands simultaneously
   - D. Performing multiple install commands simultaneously

   Answers A, B, and D are correct because they cannot be performed in any way except singly at any given time because the database is locked or because normal users cannot perform the action. Answer C is incorrect because multiple verification commands can be performed simultaneously because the operation is a read, not a read-write.

8. You need to remove all instances of the package **woohoo**, regardless of the version, with a single command. Which of the following accomplishes this task? (Choose all that apply.)
   - A. **rpm -o woohoo\***
   - B. **rpm -ea woohoo**
   - C. **rpm -a woohoo --remove**
   - D. **rpm -o woohoo --allmatches**

   Answer D is correct because the command is the only one that removes all instances of the package **woohoo** with a single command. Answer A is incorrect because asterisks do not invoke multiple removals and can be used only in installation situations for multiple packages on disk. Answer B is incorrect because the **-ea** option does not allow for multiple removals and works only in queries. Answer C is incorrect because there is no **--remove** option for the **rpm** command.

9. You are the system administrator of two firewalls and want to apply updates from a set of packages in the current directory, but you don't want to install any new packages on the systems. In the blank below, enter the exact command with any options and arguments to accomplish this:

   `rpm -F *.rpm`

   The correct answer is **rpm -F \*.rpm**. An alternative answer is **rpm --freshen \*.rpm**.

10. To view the list of required capabilities that a package needs to function properly, which command and options display this for an installed package? Enter only the command and options in the blank below:

    `rpm -qR`

    The correct answer is **rpm -qR**. An alternative answer is **rpm -q --requires**.

## PART II
LPIC Exam 102

- 10 Linux Boot Process and Runlevels
- 11 Using Linux and GNU Documentation
- 12 Managing Users and Groups
- 13 System Administration
- 14 Kernel Configuration and Custom Compilation
- 15 Linux Shells and Scripting
- 16 Linux Printing
- 17 Basic Networking
- 18 Network Services
- 19 Security
- 20 Practice Exam 101
- 21 Answer Key 101
- 22 Practice Exam 102
- 23 Answer Key 102
- A Debian Package Management
- B What’s on the CD-ROM
- Glossary

![](img/49f4f38f3aec011238fa50f89e643db3_294_0.png)

+ %clean—This section cleans up after the file is built, removing all the temporary files created in the make process.
+ %files—This is the complete list of files that are in or are to be included in the package. If it’s not in this list by its full path and filename, it won’t be in the package.
+ %doc—Files marked with this section header are places in the /usr/share/doc directory with a name set to the package name, such as /usr/share/doc/blah-woof-1.0.
+ %changelog—This is a listing in reverse chronological order of the changes to the package, including convention date, name of the main-tainer, and what happened.

Next, you change directories to the /usr/src/redhat/SPECS directory and issue this command:

```bash
rpm -ba blah-woof-1.0.spec
```

> NOTE
> This command produces output that's too voluminous to show here. Suffice it to say it's similar to running **make** on a source tarball.

This builds the package and places a copy of it in the /usr/src/redhat/RPMS/i386 directory as the blah-woof-1.0-33.i386.rpm package file.

A source package is also built (that contains the spec file and all files considered necessary to rebuild this package) and places it in the /usr/src/redhat/SRPMS directory with the name blah-woof-1.0-33.src.rpm.

> ALERT
> Take heed: you will see questions about the steps of the RPM build process on the exam. I recommend that you look closely at Chapters 10 and 11 of the book Maximum RPM (information on where to find this book is included in the "Need to Know More" file on the CD-ROM included with this book).

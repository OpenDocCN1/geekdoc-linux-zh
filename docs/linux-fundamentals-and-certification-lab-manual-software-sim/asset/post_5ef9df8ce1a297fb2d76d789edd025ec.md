
## ADMINISTRATIVE TASKS

### FIGURE 6–13
/proc/scsi/scsi file.

```bash
root@Styx (/proc/scsi)
[root@Styx scsi]# cd /proc/scsi
[root@Styx scsi]# cat scsi
Attached devices:
Host: scsi0 Channel: 00 Id: 06 Lun: 00
  Vendor: QUANTUM Model: DLX7000  Rev: 2150
  Type:  Sequential-Access
Host: scsi2 Channel: 00 Id: 06 Lun: 00
  Vendor: NEC  Model: CD-ROM DRIVE:466 Rev: 1.06
  Type:  CD-ROM
Host: scsi3 Channel: 00 Id: 00 Lun: 00
  Vendor: DELL  Model: PERC/RAID RAID5  Rev: V1.0
  Type:  Direct-Access
[root@Styx scsi]# 
```

```bash
mt -f /dev/st0 rewind
# Perform an incremental backup of the /home directory.
tar cvglpf /dev/st0 /home
# Unload the tape
mt -f /dev/st0 offline
```

On Tuesday do the following commands:

```bash
# Tuesday's backup
# Rewind the tape
mt -f /dev/st0 rewind
# Skip the first file on the tape. (Skip over Monday's backup.)
mt -f /dev/st0 fsf 1
tar cvglpf /dev/st0 /home
mt -f /dev/st0 offline
```

On Wednesday do the following commands:

```bash
# Wednesday's backup
# Rewind the tape
mt -f /dev/st0 rewind
# Skip the first two files on the tape. (Skip over Monday's and Tuesday's backups.)
mt -f /dev/st0 fsf 2
tar cvglpf /dev/st0 /home
mt -f /dev/st0 offline
```

On Thursday do the following commands:

```bash
# Thursday's backup
# Rewind the tape
mt -f /dev/st0 rewind
# Skip the first three files on the tape. (Skip over Monday's through
# Wednesday's backup)
mt -f /dev/st0 fsf 3
tar cvglpf /dev/st0 /home
mt -f /dev/st0 offline
```

On Friday do the following commands to perform a full backup:

```bash
# Friday's backup - Use a new tape or an old tape to overwrite.
# Rewind the tape
mt -f /dev/st0 rewind

# Perform a full backup.
tar cvglpf /dev/st0 /home
mt -f /dev/st0 offline
```

## SHELL PROGRAMMING

You have two choices for entering information into the computer—the command line or the graphical user interface. The GUI is much easier for novice users to use, but it doesn't have the power of the command-line interface. Shell programming brings out the real power of the command-line interface.

Imagine using the GUI or the useradd command to enter several hundred new users. That could be a very time-consuming and tedious task for an administrator. Shell programming makes this task much easier.

Shell programming is accomplished through shell scripts. As its name implies, a shell script is a list of shell commands. Other shells, such as csh and korn, are available for Linux but the default shell is bash. Each shell has its own scripting language, and yet these different shells are very similar. In many cases, a shell script written for one shell will run in another shell.

Many of the Linux startup scripts are actually shell scripts. For this reason, understanding shell scripts is necessary if modifications to Linux are needed.

### Constructing a Shell Script

The structure of a bash shell script is very simple. Only three things are needed for a shell script.

- 1. A shell script needs a first line that identifies the shell name used to run it. By default Linux uses bash, so the first line is **#!/bin/bash**
  The characters #! are special characters that let the kernel know that this a shell script. The /bin/bash entry tells the kernel where the shell program is located. If the shell program is not where indicated, a **Command not found** error will be displayed when the script is run. In this case, issue the command **whereis bash** to find bash. This command will return every location of the bash command.
- 2. The second thing needed for a successful script is something for the script to do. This can be almost any command-line statement; for example, **echo Hello World**. In this case the echo command displays a line of text, Hello World.
- 3. The last step needed to make a script is to change the permissions on the created file to allow execution. If the file created is called **hello**, the command to set the execute permission is **chmod +x hello**.

To create this script, use the vi editor to enter the lines described in steps 1 and 2; then save the file with the name of **hello**. Exit the editor and then execute the command in step 3 to change the permissions of the file.

To run the script, type the **./hello** command from the directory the hello file is in.

Figure 6–14 shows the vi screen with the script entered.

### FIGURE 6-14
Use vi to create script.

```bash
#!/bin/bash
echo Hello World
```

Figure 6-15 shows the commands used to change permissions and then execute the hello script.

### FIGURE 6-15
Change permissions and run script.

```bash
[root@localhost root]# ls -l
total 104
-rw-r--r-- 1 root root 1544 Aug 22 23:29 anaconda-ks.cfg
-rw-r--r-- 1 root root 30 Oct 6 21:00 hello
-rw-r--r-- 1 root root 20654 Aug 22 23:21 install.log
-rw-r--r-- 1 root root 4223 Aug 22 23:21 install.log.syslog
-rw-r--r-- 1 root root 53760 Oct 5 22:57 jsmith-backup.cpio
drwxr-xr-x 2 root root 4096 Sep 11 21:10 screenshots

[root@localhost root]# chmod +x hello

[root@localhost root]# ls -l
total 104
-rw-r--r-- 1 root root 1544 Aug 22 23:29 anaconda-ks.cfg
-rwxr-xr-x 1 root root 30 Oct 6 21:00 hello
-rw-r--r-- 1 root root 20654 Aug 22 23:21 install.log
-rw-r--r-- 1 root root 4223 Aug 22 23:21 install.log.syslog
-rw-r--r-- 1 root root 53760 Oct 5 22:57 jsmith-backup.cpio
drwxr-xr-x 2 root root 4096 Sep 11 21:10 screenshots

[root@localhost root]# ./hello
Hello World
[root@localhost root]#
```

### Shell Script Variables and Arguments

One of the advantages of using a script is that you can pass values to the script before it executes. For example, if you wanted the hello script to display "Hello" and a name, you could change the script and execute it as follows:

```bash
./hello Jeff
```

The name Jeff would be an **argument** for the hello script.

A **variable** in a script is a token that has an assigned value. For example, the message of the hello script could be assigned to the variable MSG, and then MSG could be used with any command within the script.

**Arguments** Command-line arguments are passed to a script when executed. The value of an argument is retrieved with the argument symbol $ (dollar sign) and a number indicating where the argument is on the line. For example, if a name is passed to the hello script as described previously, the value is assigned to the argument variable $1.

- To change the hello program to use an argument, follow these steps:
  1. Copy the file hello to hello2 so you don’t have to change your original file.
     ```bash
     cp hello hello2
     ```
     The hello2 script will have the same permissions as the hello script.
  2. Edit the hello2 script to reflect the following changes:
     ```bash
     #!/bin/bash
     echo Hello $1
     ```
     The $1 will be replaced with the value of the argument used on the command line.
  3. Execute the script, passing the command line argument *Jeff* to the script. For example, if you type `/hello2 Jeff`, "Hello Jeff" will be displayed.

Multiple arguments are allowed on the command line. For example, if you wanted to pass four arguments to a script called args, you would use the following syntax: *args arg1 arg2 arg3 arg4*. To pass four names to a hello script, you might type in /hello3 Jeff Jones Sally Smith.

- To change the hello program to use four arguments, follow these steps:
  1. Copy the file hello to hello3 so you don’t have to change your original file.
     ```bash
     cp hello hello3
     ```
  2. Edit the hello3 script to reflect the following changes:
     ```bash
     #!/bin/bash
     echo Hello $2, $1
     echo Hello $4, $3
     ```
  3. Execute the script to pass the four arguments *Jeff*, *Jones*, *Sally*, and *Smith* to the hello3 script. For example:
     ```bash
     ./hello3 Jeff Jones Sally Smith
     ```
     The result should be:
     ```bash
     Hello Jones, Jeff
     Hello Smith, Sally
     ```

Notice that the *literal* values Hello and the comma (,) are displayed where indicated in the script.

### Variables

All programming languages and most script languages support variables. A variable is a token within a script that is assigned a value. The difference in variables and arguments can be seen in the way values are assigned. An argument is assigned a value from the command line, based on its position on the line. After the value is assigned, it can be changed only by rerunning the script. A variable is assigned its value within the script with an assign symbol. Variables can change within the script programmatically.

To replace the literal "Hello World" with the variable HW in the hello script, you could do the following:

- 1. Copy the file hello to hello4 so you don’t have to change your original file.
  ```bash
  cp hello hello4
  ```
- 2. Make the following changes to the hello4 script.
  ```bash
  #!/bin/bash
  HW = "Hello World"
  echo $HW
  ```
  "Hello World" is assigned to the variable HW using the assignment symbol = (equals sign). Variables in scripts are generally in all caps by convention, but this is not mandatory. When you reference a variable, place a $ (dollar sign) in front of it to indicate that it is a variable and not a literal value.

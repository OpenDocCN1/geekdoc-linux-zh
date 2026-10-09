Configuration files can be edited and changes made that affect the system or users. Every configuration file is a standard text file that can be easily manipulated. Most entries are in the form of a name/value pair, where an entry such as path is assigned a value such as /tmp as in PATH=/tmp.

After configuration files are changed, the services to which they apply must be restarted. In the case of a system file, you may need to restart the server. For user-related entries, logging off and then logging back on will reread the configuration information.

Services can be restarted with the `service service_name restart` command. GUI programs are available that make restarting services easier for novice users.

Two methods of sharing resources on Linux machines are Network File System (NFS) and Samba. NFS is the oldest method and the one most widely used in purely Linux environments. Samba uses the Microsoft Windows protocol SMB. Samba-shared resources can be used by Linux and Windows clients.

# SELF-TEST Home Work

+   1. Where are user configuration files located?
   a. The user's home space
   b. The root directory
   c. The current directory
   d. The /etc/config directory
2. True or False: Many Linux operating system functions are controlled through configuration files.
3. User files have the following characteristics.
   a. They begin with a dot (.)
   b. They are contained within the user's home directory.
   c. They are hidden by default for security reasons.
   d. All of the above
4. Which file contains common shell information for all users?
   a. ~/.bash_profile
   b. ~/.bashrc
   c. /etc/profile
   d. /etc/users
5. What is the correct sequence of system startup with the SysV startup process in the Linux operating system?
   a. init process, boot, bootwait, run start scripts
   b. bootwait, boot, init process, run start scripts
   c. boot, bootwait, init process, run start scripts
   d. run start scripts, init process, boot, bootwait
6. Which of the following configuration files contains a list of drivers that are not designed into the Linux kernel?
   a. lilo.conf
   b. fstab
   c. modules.conf
   d. XF86Config
7. True or False: SysV and BSD are the two startup processes common to all Linux operating systems.
8. Which command correctly sets an environment variable called MYFILES with a value of /home/jsmith/myfiles?
   a. export MYFILES=/home/jsmith/myfiles
   b. echo $MYFILES=/home/jsmith/myfiles
   c. /home/jsmith/myfiles=EXPORT MYFILES
   d. export /home/jsmith/myfiles=MYFILES
9. Which of the following commands can be used to display the value of the environment variable MYFILES?
   a. echo MYFILES
   b. export MYFILES
   c. print MYFILES
   d. echo $MYFILES
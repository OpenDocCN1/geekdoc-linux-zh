```
yum install make automake gcc gcc-c++ kernel-devel
```

The source code of most software is available as compressed tarballs. These are TAR files that have been compressed with Gzip and sport the .tar.gz extension. Download the source code into your home directory. You can uncompress it with the tar command:

```
tar zxvf softwaresource.tar.gz
```

Now move into the extracted directory and look for a file that's named Install or Readme or something along those lines. This text file contains specific instructions about how to compile that particular piece of software. The generic procedure to compile software begins by calling a configuration script with the /configure command, which checks whether or not your computer meets the specific requirements of the software. If you are missing any dependencies, the configure script will abort, telling you the name of the missing components. You can then install these via the package manager.

Once the configure script has run through its checks successfully, you can compile the software by issuing the make command. This command will take some time, depending on the size of the software you are installing. When it's finished, round up the procedure by running the make install command as the root user.

# Navigate the file system

You should already be familiar with your user directory, which is under the /home directory. To be an effective Linux user, you should also familiarise yourself with the filesystem and its organisation.

The commands essential to keep the system up and running are kept under /bin. Unlike regular apps that are dynamically linked and depend on shared software libraries to run, the commands under /bin are statically linked and do not depend on software libraries residing elsewhere.

The /etc directory houses the system configuration files and directories. While some software packages such as Apache and OpenSSH have their own directories within /etc that contain their configuration files, others such as fstab only use one configuration file. An important directory under /etc is modprobe.d/ which contains instructions for loading kernel modules during system startup.

The /proc directory differs from the others in that its contents are created from memory and exist only while Linux is actually running. You can get information about the computer by reading the contents of files under this directory. This command, for instance, will display various details about the CPU:

# Quick tip

Ensure that you always make a backup of a configuration file before you start to edit it by using the cp command, such as cp configfile configfile.original.

![](bbox=[0.12, 0.71, 0.56, 0.9])

Some distros include a graphical tool for displaying logs.

the CPU:

```
cat /proc/cpuinfo
```

Then there's the /usr directory, which contains apps, libraries and other types of shared data for use by anyone on the system. The /var directory contains directories used by various system services for spooling and logging. Some of these, such as print spooler queues under /var/spool, only exist temporarily. Others, such as the logs under /var/log, are renamed and rotated regularly.

Talking of log files, checking on them is an essential admin task. The Linux kernel, critical network services and other important apps all record critical activity inside log files that are filed under the location /var/log. In particular, two important log files you should regularly look at are auth.log, which logs all authentication attempts made on the system, and boot.log, which records messages generated while the system boots and starts services.

Then there's that /home partition that you are already familiar with. It is very good practice to keep /home on a separate partition from the rest of the filesystem. This ensures that the data inside will survive any damage to other parts of the distribution.

# Monitor the system

Another important aspect of a system admin's job is to make sure the computer they are looking after continues to run smoothly. If you want to check how things are doing, you can use the ps -e command. This will print a long list of all the processes that are running on the system. You can truncate the list to display only processes that have the same UID as the current user by invoking the ps command without any switches. The output of the ps command includes the unique process ID (PID) along with the name of the running program.

It's more common to pipe the list to display information about a specific program, however. This command will show information only about the processes that are associated with LibreOffice:

```
ps aux | grep libreoffice
```

Once you know the PID of a process, you can terminate that process with the kill command. Assuming that LibreOffice has a PID of 8899, you can terminate an unresponsive session with this command:

```
kill 8899
```

You can use the top command to view a list of running tasks with the most CPU-intensive ones listed first. The top command displays various bits of information about the processes, including its PID. It also has a few interactive commands. For example, you can kill a process from within top by pressing the [K] key, which prompts you to enter the PID of the process you want to terminate.

If you have a process that's hogging the resources on your computer, the renice command will assign it a lower priority. Linux assigns a priority to each process, and the ones with higher priority are given access to the system's resources first, while others that have lower priority need to wait for their turn.

The renice command can assign a priority value between -20 and 19. The lower the number, the higher the priority. For example, if you wanted to take away resources from LibreOffice (PID: 8899) you could assign it a lower priority number with this command:

```
renice 15 8899
```

If the command line isn't really your cup of tea, the Gnome and KDE desktop environments also include their own system monitoring tools in your distro's official repository.
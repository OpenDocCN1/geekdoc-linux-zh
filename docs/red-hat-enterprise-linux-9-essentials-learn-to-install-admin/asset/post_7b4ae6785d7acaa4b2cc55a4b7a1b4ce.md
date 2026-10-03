
```
gnome-terminal-serv
demo        9814  0.0  0.1 224108  5664 pts/2    Ss   15:05   0:00 bash
demo        9849  0.0  0.0 222412  3588 pts/2    S+   15:06   0:00 nano
demo        9873  0.0  0.1 233416  6280 pts/1    R+   15:08   0:00 ps -aux
```

A Linux process can start its own sub-processes (referred to as spawning), resulting in a hierarchical parent-child relationship between processes. To view the process tree, use the ps command and include the -H option. Below is part of the tree output for a ps -aH command execution:

```
$ ps -aH
    PID TTY      TIME CMD
    10036 pts/3  00:00:00 ps
      6350 pts/0  00:00:00 sudo
      6354 pts/0  00:00:00 su
      6355 pts/0  00:00:00 bash
      5442 tty2   00:00:00 gnome-session-b
```

Process information may also be viewed via the System Monitor tool from the GNOME desktop. This tool can either be launched by searching for “System Monitor” within the desktop environment or from the command line as follows:

```
$ gnome-system-monitor
```

Once the System Monitor has launched, select the Processes button located in the toolbar to list the processes running on the system, as shown in Figure 34-1 below:

![](img/be1f159c3cc937d7b264dc5b134856dc_277_0.png)

Figure 34-1

To change the processes listed (for example, to list all processes or just your own processes), use the menu as illustrated in Figure 34-2:

## RHEL 9 System and Process Monitoring

![](img/be1f159c3cc937d7b264dc5b134856dc_278_0.png)

Figure 34-2

To filter the list of processes, click on the search button in the title bar and enter the process name into the search field:

![](img/be1f159c3cc937d7b264dc5b134856dc_278_1.png)

Figure 34-3

To display additional information about a specific process, select it from the list and click on the button located in the bottom right-hand corner (marked A in Figure 34-4) of the dialog:

![](img/be1f159c3cc937d7b264dc5b134856dc_278_2.png)

Figure 34-4

A dialog similar to that marked B in the above figure will appear when the button is clicked. Select a process from the list and click the End Process button (C) to terminate it.

To monitor CPU, memory, swap, and network usage, click on the Resources button in the title bar to display the screen shown in Figure 34-5:

![](img/be1f159c3cc937d7b264dc5b134856dc_279_0.png)

Figure 34-5

Similarly, a summary of storage space used on the system can be viewed by selecting the File Systems toolbar button:

![](img/be1f159c3cc937d7b264dc5b134856dc_279_1.png)

Figure 34-6

### 34.2 Real-time System Monitoring with top

As the chapter “An Overview of the Cockpit Web Interface” outlined, the Cockpit web interface can perform basic system monitoring. The previous section also explained how the GNOME System Monitor tool could be used to monitor processes and system resources. This chapter also explored how the ps command can provide a snapshot of the processes running on a RHEL 9 system. However, the ps command does not provide a real-time view of the processes and resource usage on the system. The top command is an ideal tool for real-time monitoring of system resources and processes from the command prompt.

When running, top will list the processes running on the system ranked by system resource usage (with the most demanding process in the top position). The upper section of the screen displays memory and swap usage information together with CPU data for all CPU cores. All of this output is constantly updated, allowing the system to be monitored in real-time:

## RHEL 9 System and Process Monitoring

![](img/be1f159c3cc937d7b264dc5b134856dc_280_0.png)

Figure 34-7

To limit the information displayed to the processes belonging to a specific user, start top with the -u option followed by the user name:

```
$ top -u john
```

For a complete listing of the features available in top, press the keyboard ‘h’ key or refer to the man page:

```
$ man top
```

### 34.3 Command-Line Disk and Swap Space Monitoring

Disk space can be monitored from within Cockpit and using the GNOME System Monitor. To identify disk usage from the command line, however, the df command provides a helpful and quick overview:

```
# df -h
Filesystem      Size  Used Avail Use% Mounted on
devtmpfs        4.0M     0  4.0M   0% /dev
tmpfs           1.8G     0  1.8G   0% /dev/shm
tmpfs           704M  9.6M  694M   2% /run
/dev/mapper/rhel-root00  70G  6.3G   64G   9% /
/dev/mapper/rhel-home00 224G  1.8G  222G   1% /home
/dev/sda1       1014M  290M  725M  29% /boot
tmpfs           352M  144K  352M   1% /run/user/1000
```

To review current swap space and memory usage, run the free command:

```
# free
               total        used        free      shared  buff/cache   available
Mem:       3823720      879916     1561108      226220     1382696      2476300
```

To continuously monitor memory and swap levels, use the free command with the -s option, specifying the delay in seconds between each update (keeping in mind that the top tool may provide a better way to view this data in real time):

```
$ free -s 1
Mem:         3823720      879472     1561532     226220     1382716     2476744
Swap:        2097148           0     2097148

               total       used       free     shared buff/cache   available
Mem:         3823720      879140     1559940     228144     1384640     2475152
Swap:        2097148           0     2097148
.
.
```

To monitor disk I/O from the command line, consider using the iotop command, which can be installed as follows:

```
# dnf install iotop
```

Once installed and executed (iotop must be run with system administrator privileges), the tool will display a real-time list of disk I/O on a per-process basis:

![](img/be1f159c3cc937d7b264dc5b134856dc_281_0.png)

Figure 34-8

### 34.4 Summary

Even a system that appears to be doing nothing will have many system processes running in the background. Activities performed by users on the system will result in additional processes being started. Processes can also spawn their own child processes. Each process will use some system resources, including memory, swap space, processor cycles, disk storage, and network bandwidth. This chapter has explored a set of tools that can be used to monitor both process and system resources on a running system and, when necessary, kill errant processes that may be impacting the performance of a system.

## Index

## Index

### Symbols

- ! 63
- #! 67
- >> 65
- | 65
- $DISPLAY variable 138
- 50-redhat.conf 137
- .bashrc 67
- /etc/containers/networks 218
- /etc/default/grub 31
- /etc/exports 144
- /etc/fstab 33, 35, 145, 147, 243
- /etc/gdm/custom.conf 137
- /etc/group 71
- /etc/httpd 225
- /etc/passwd 71
- /etc/samba/smb.conf 150
- /etc/shadow 71
- /etc/ssh/sshd_config 137
- /etc/ssh/sshd_config.d 137
- /etc/sudoers 71
- /etc/systemd/system 88, 130
- /etc/yum.repos.d/ directory 78
- /home 69
- /proc/swaps 257
- .requires 89
- .ssh 118, 120
- /usr/lib/systemd/system 88
- /var/log/maillog 236
- .wants 88

### A

- ACC Corporation 8
- Activity Overview 42
- adduser 69
- AIX 7
- alias 65
- Aliases 65
- AMD-V 164
- Andrew S. Tanenbaum 7
- Apache
  - mod_ssl 227
- Apache web server 223
- Application Stream 77
- AppStream 77, 79
  - modules 79
  - packages 79
  - profiles 79
- AppStream repository 77
- authorized_keys file 122

### B

- BaseOS repository 77, 78
- Bash
  - scripts 67
- Bash shell 61
  - aliases 65
  - .bashrc 67
  - chmod 68
  - command-line editing 62
  - do loops 67
  - echo 66
  - environment variables 66
  - filename completion 64
  - Filename shorthand 64
  - for loop 67
  - history 63
  - HOME 66
  - input and output redirection 64
  - PATH 66
  - path completion 64
  - pipes 65
  - sh 68
  - stderr 65
- stdin 64
- stdout 64
- basic.target 84
- Bell Labs 61
- Bourne Again SHell 61
- Bourne shell 61
- Brian Fox 61
- buildah 207
  - containers 214
  - from registry 214
  - from scratch 214
  - installroot 215
  - run 215
  - umount 215
- Buildah 209
- CA 226
- cat 64
- certbot 227
- Certificate Authority 226
- change root 205
- chmod 68
- chroot 205
- cifs filesystem 159
- CNI 208, 215
- Cockpit 89
  - accessing 50
  - account management 54
  - applications 55
  - cockpit-machines 171
  - cockpit-storaged 146
  - create VM 171
  - Drives 244
  - enabling 50
  - extensions 49, 55
  - firewall management 114
  - installing 50
  - logs 52
  - Multiple Servers 57
  - networking 54
  - NFS 146
  - overview 49
  - persistent metrics 58
  - Podman Containers 218
  - port 50
  - select bridge 195
  - services 54, 89
  - storage 53, 243
  - system 51
  - systemd 89
  - terminal access 56
  - user management 71
  - virtual machines 55
  - volume groups 253
- cockpit-machines 171
- cockpit.socket 50
- cockpit-storaged 146, 253
- Compressed X11 Forwarding 138
- Connection Profiles 96
- containerd 205
- Container Networking Interface 208, 215
- Containers
  - attaching to an image 212
  - bridge networking 215
  - buildah 214
  - networking 215
  - Networking Interface 215
  - overview 205
  - pulling an image 209
  - removing an image 214
  - running an image 211
  - saving to an image 213
  - stopping 213
- context labels 153
- CRI-O 205
- C shell 61
- daemon 83
- dash 43
- David Korn 61

## Index

### C

### D


![](img/75f39fc91296b889c0653851accdfd46_1269_0.png)

**Figure 18-8** *SFU Mount Options*

We are using the default *Read Buffer Size* of 64,000 bytes. I like to keep this number large, because it is the data part of the packet used during NFS reads. In general, bigger is better. The same is true of the *Write Buffer Size*. The *Initial_Timeout* specifies the amount of time to wait for a response from the server before a retry. *Retries* specifies the number of times you'll attempt to access the server before dropping the operation altogether. I also use a *Mount Type* of *Soft*, as opposed to *Hard* and *Enable Caching*.

*File Access* allows you to specify privileges for users establishing NFS mounts. These are the privileges you're accustomed to seeing when working with files, as shown in Figure 18-9.

![](img/75f39fc91296b889c0653851accdfd46_1270_0.png)

**Figure 18-9** **SFU File Access**

By default, *User* will have unlimited access to files, and those in the *Group* and *Other* will have read (R) and execute (X) access only. These are common privilege assignments.

We can easily establish our NFS connection by selecting *OK* from the *Authentication* window shown in Figure 18-2. A box appears asking you to confirm the user name and other information, such as that shown in Figure 18-10.

![](img/75f39fc91296b889c0653851accdfd46_1271_0.png)

**Figure 18-10** **NFS Login Successful**

The Username, UID, and Primary GID correspond to those on the UNIX NFS server. If we view the passwd file on the UNIX NFS server system and look for our user, hp, we'll see the following entry:

```
hp:EkyXw/N.EwFNw:104:20::/home/hp:/sbin/sh
```

The information in this **passwd** entry corresponds to that shown in our NFS Login window.

After login takes place, we can view the file systems exported on the UNIX NFS server using Explorer on our Windows system. Figure 18-11 shows the *Manhattan* LAN, with a specific system selected.

![](img/75f39fc91296b889c0653851accdfd46_1272_0.png)

**Figure 18-11** **Viewing the NFS Mounted File System**

`/home/hp` is selected, and the right Explorer window shows the files in the `\home\hp` directory. We have permission to manipulate the files in the `hp` directory. We can check this by selecting a file, such as .cshrc, and viewing its properties. Figure 18-12 shows the *Properties* window.

![](img/75f39fc91296b889c0653851accdfd46_1273_0.png)

**Figure 18-12** **SFU *Properties***

The *Read-only* box in this window is not checked; therefore, we have full access to this file.

# Telnet Client

There is also a Telnet client loaded as part of SFU. Selecting *Telnet - Telnet Client* from the SFU menu produces the Telnet window shown in Figure 18-13.

![](img/75f39fc91296b889c0653851accdfd46_1274_0.png)

**Figure 18-13** **SFU Telnet Client**

I have created a long listing of the contents of **/home/hp** in this Telnet window.

![](img/75f39fc91296b889c0653851accdfd46_1274_1.png)

# Telnet Server

![](img/75f39fc91296b889c0653851accdfd46_1275_0.png)

There is also a Telnet server loaded as part of SFU. This means you can connect from a UNIX system, or any other system with a Telnet client, to a Windows NT system with the SFU Telnet server. Figure 18-14 shows accessing the Windows Telnet server from a UNIX system.

![](img/75f39fc91296b889c0653851accdfd46_1275_1.png)

![](img/75f39fc91296b889c0653851accdfd46_1275_2.png)

In Figure 18-14, I have initiated a Telnet session from my UNIX system to my Windows system. After receiving the welcome information from the Microsoft Telnet server, I can issue commands, such as the **dir** shown, exactly as I would from the prompt if I were working directly on the Windows system.

The Telnet server functionality of SFU gives some direct access from UNIX to Windows, which is a big help in mixed environments.

This functionality is further enhanced by many UNIX utilities that you can run on the Windows system through this Telnet connection or on the Windows system directly. The next section "UNIX Utilities" covers these utilities.

# UNIX Utilities

One highly desirable capability of SFU is a UNIX Command Shell invoked with *Unix Utilities - Unix Command Shell*. Figure 18-15 shows a window open with the UNIX utilities listed.

![](img/75f39fc91296b889c0653851accdfd46_1276_0.png)

The utilities listed in Figure 18-15 work in SFU just the way they work in UNIX. You also have access to these UNIX utilities through the Telnet session that you can establish from another system. To give you an idea how these utilities work, let's issue a few commands, as shown in Figure 18-16.

![](img/75f39fc91296b889c0653851accdfd46_1277_0.png)

![](img/75f39fc91296b889c0653851accdfd46_1277_1.png)

![](img/75f39fc91296b889c0653851accdfd46_1277_2.png)

**Figure 18-16** **SFU Example of Using Some UNIX Utilities**

![](img/75f39fc91296b889c0653851accdfd46_1277_3.png)

This window shows that when we invoke *Unix Utilities*, we are in the `C:/SFU/Shell` directory on our Windows system. We change directory to `C:/` by issuing `cd /`, as we would on a UNIX system. `pwd` confirms that we are at the `C:/` level. We then issue an `ls` to see the files in `C:/`.

Let's issue two more of the *Unix Utilities* to get a better feel for how these utilities perform in Windows, as shown in Figure 18-17.

```
C:\> Unix Command Shell
$ ls | grep -i s
CONFIG.SYS
FIRSTBOOT.TXT
IE401SP1
Internet Explorer 4.01 SP1 Setup
MOUSE
Multimedia Files
MSISF3
Program Files
SETUP
SFU
IT4S
ITHS
topools
pagefile.sys
$ ls | grep -i s | wc
    14    20   166
```

**Figure 18-17** **SFU Example of Using Some UNIX Utilities**

![](img/75f39fc91296b889c0653851accdfd46_1278_0.png)

In this window, we issued an **ls** and a **grep** command that ignored case (-i) and searched for *s*. Files that contained both upper- and lowercase *s* were listed. We then piped this same output to **wc** to get a word count.

![](img/75f39fc91296b889c0653851accdfd46_1278_1.png)

# NFS Server

Not only can the Windows system act as an NFS client, but it can also act as an NFS server with SFU. A system running NFS can mount a file system exported on the Windows system.

Under *Server for NFS Configuration*, you can configure all aspects of your NFS server setup. The defaults for most categories of configuration are fine for initial testing, which we'll perform here. You may want to later perform additional configuration to tune your NFS server.

For our example, I’ve created one *Share Name*, as shown in Figure 18-18.

![](img/75f39fc91296b889c0653851accdfd46_1279_0.png)

**Figure 18-18** **SFU Share Name**

By selecting **Server for NFS Configuration** from the menu and then *Share Options*, I entered the *Share Name* **C:\temp** shown in Figure 18-18.

We can view *Mount Information* to see what file systems we have exported, as shown in Figure 18-19.

![](img/75f39fc91296b889c0653851accdfd46_1280_0.png)

**Figure 18-19** **SFU Mount Information**

Our file system of **C:\temp** is indeed in the exported list with no restrictions on who may access it.
With this *Share Name* having been established, we can use the defaults for all other categories of NFS server configuration and mount **C:\temp** on a UNIX system. To mount **C:\temp**, you would issue the following command on your UNIX system:

![](img/75f39fc91296b889c0653851accdfd46_1281_0.png)

```
# mount 19.32.23.112:C:\temp /ntmount
```

This command will work on most UNIX systems. We have first specified the mount command, which you would normally issue as root. Next is the name of the Windows system that has the file system we wish to mount on it; in this case, I have used the IP address rather than the system name. The system name, or IP address, is followed by a colon (:). Next is the name of the file system we wish to mount, as it appears on the Windows system, in this case **C:\temp**. Last is the name of the directory on the UNIX system under which we’ll mount **C:\temp**, in this case `/ntmount`. You can also add a variety of different options with the **mount** command, but we’ll use all defaults in our example.

Let’s now check to see whether indeed the NFS mount we specified has been established on the UNIX system. The following example shows issuing the **bdf** command, which is somewhat similar to the **df** command covered earlier in the book, on the UNIX system to see whether the mount has been established, then a **cd** to the **ntmount** directory, and finally an **ls** of the files in this directory:

![](img/75f39fc91296b889c0653851accdfd46_1281_1.png)

```
# bdf
Filesystem      kbytes    used    avail %used Mounted on
/dev/vg00/1vol3  151552   53165   92162   37%   /
/dev/vg00/1vol1   47829   14324   28722   33%   /stand
/dev/vg00/1vol8  163840   87595   71039   55%   /var
/dev/vg00/1vol7  339968  314984  23189   93%   /usr
/dev/vg00/1vol6  102400   62284   37607   62%   /tmp
/dev/vg00/1vol5  1048576  656649  367439  64%   /opt
```

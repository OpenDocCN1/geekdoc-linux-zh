![](Image00003.jpg)

![](Image00003.jpg)

Linux FAQS

Intermediate Users

By

Liza Noble

Copyright © sujatabiswas.click Publications

 All rights reserved.

Content

[Dedication](#text00004.html__Toc88252416)

[Interactive Book](#text00004.html__Toc88252417)

[Introduction](#text00004.html__Toc88252418)

[How do I create SUDO users on Linux?](#text00004.html__Toc88252419)

[How to use ssh without a password?](#text00004.html__Toc88252420)

[How to create a directory structure in Linux?](#text00004.html__Toc88252421)

[How do I work with compressed files?](#text00004.html__Toc88252422)

[Can you explain about file/directory permissions?](#text00004.html__Toc88252423)

[What are symbolic links?](#text00004.html__Toc88252424)

[What is a Linux BASH shell environment?](#text00004.html__Toc88252425)

[How to create an alias in the Linux Bash Shell environment? Or how to create my own Linux command?](#text00004.html__Toc88252426)

[How to create a simple function on the Linux Bash shell environment?](#text00004.html__Toc88252427)

[How I do collect the IP address, gateway, subnet mask and DNS servers from a system?](#text00004.html__Toc88252428)

[What do I do with DNS on Linux?](#text00005.html__Toc88252429)

[How do I monitor network access on my environment?](#text00005.html__Toc88252430)

[How to work with text files on Linux?](#text00005.html__Toc88252431)

[Can you provide an example of regular expressions?](#text00005.html__Toc88252432)

[How to set a Static IP address on Linux?](#text00005.html__Toc88252433)

[How do I see the status of the TCP port?](#text00005.html__Toc88252434)

[How to see the firewall status on Linux?](#text00005.html__Toc88252435)

[How do I check local resolution on my Linux machine?](#text00005.html__Toc88252436)

# Dedication

This book is dedicated to Ms. Sujata Biswas who passed because of Covid. Each day that passes without her is a torture. She remains an inspiration behind this fledging publishing house.

# Interactive Book

This is an on-going project and if you wish to add any questions to this FAQ, we will add your content and republish the book repeatedly. You can send your queries/questions/suggestions to [bookreviewer25@gmail.com](mailto:bookreviewer25@gmail.com)

# Introduction

The method used is unique and favored in the corporate world. Instead of long chapters and sections with information that is useless at critical times, you have access to pertinent questions - collected over 3 decades of IT experience and gives you immediate answers.

# How do I create SUDO users on Linux?

Before learning how to create SUDO users, why do not we revise concepts of creating ordinary users and groups.

Your task to create new users on recently procured Linux box. The users that would access the system are Helen, Leena, and Tony – who belong to the DevOps group. You need to create a group as well, which would name, most imaginatively, as devops. The users would be the members of the devops group.

Step1:

Adding users –

# useradd helen

# useradd leena

# useradd tony

Note:

Login as ROOT.

Step 2:

Creating a group called devops –

# groupadd devops

When you create the users, they are members of their groups. We can add devops as a supplementary group.

Step 3:

The command you use is usermod –

# usermod -aG devops helen

# usermod -aG devops leena

# usermod -aG devops tony

Step 4:

To check the group memberships of each user, use the command id –

# id leena

uid=1003(leena) gid=1003(leena) groups=1003(leena),1005(devops)

# id tony

uid=1004(tony) gid=1004(tony) groups=1004(tony),1005(devops)

# id helen

uid=1002(helen) gid=1002(helen) groups=1002(helen),1005(devops)

As you can each user is a member of the supplementary group devops .

If you want to LOCK a particular user - he is on leave/or left the organziation. You can use the command:

# usermod -L tony

All users must NOT be given elevated privileges; however, you cannot do all the tasks yourself so you must delegate some work to chosen users to perform some jobs. If such users need to perform tasks that require administrative privileges, then they can use the SUDO command. And you should create SUDO users.

To check the SUDO configuration file using the command visudo and look at a particular line. It is a long file.

This line means that members of the group wheel can run all commands.

| ## Allows people in group wheel to run all commands%wheel  ALL=(ALL)       ALL |

Create a user called rosie –

# useradd rosie

Login as rosie using the command to access her shell :

$ su – rosie

Try to read the shadow file in the /etc directory. The shadow files contain the encrypted passwords.

$ cat /etc/shadow

cat: /etc/shadow: Permission denied

But rosie cannot read the shadow file.

Recall that from the SUDO configuration file, that members of the wheel group can run all commands. Let us make rosie a member of the wheel group. You need to be root again.

Making rosie a member of the wheel group.

# usermod -aG wheel  rosie

Checking if the rosie is indeed the member of the wheel group.

# id rosie

uid=1005(rosie) gid=1006(rosie) groups=1006(rosie),10(wheel)

Remember to set rosie a password using the command –

#passwd rosie

Login as rosie –

#su – rosie

Now, rosie can read the shadow file.

$ sudo cat /etc/shadow

# How to use ssh without a password?

The system lx-centos is the remote system.

You are the user sujata (from the system centos8) want to connect ( ssh)  to the lx-centos without using a password.

On the system centos8 and login as sujata:

Step 1: Sanity check

$ whoami

sujata

You must have a username by sujata in the second system for this learning procedure.

Creating ssh key so that password is not required using ssh-keygen

$ ssh-keygen

Generating public/private rsa key pair.

Enter file in which to save the key (/home/sujata/.ssh/id_rsa):

Created directory '/home/sujata/.ssh'.

Enter passphrase (empty for no passphrase):

Enter same passphrase again:

Your identification has been saved in /home/sujata/.ssh/id_rsa.

Your public key has been saved in /home/sujata/.ssh/id_rsa.pub.

The key fingerprint is:

SHA256:LaJnCHz9UvwmV+2dfnjRWR5k4255ZM17YLnSpLKo+Uk sujata@lx-centos8

The key's randomart image is:

+---[RSA 3072]----+

|                 |

|               + |

|              +oo|

| .   . . .   .=o*|

|  o . o S . .=o*B|

|   o o + o..o.oO*|

|    o + E.+o .oo=|

|     o +.=.  o o|

|      ooo      o.|

+----[SHA256]-----+

Then use the ssh-copy-id to the remote system in the following manner

$ ssh-copy-id sujata@192.168.29.182

Where 192.168.29.182 is the IP address of the remote system. You would get the similar message. You need to provide the password for the first time.

$ ssh-copy-id sujata@192.168.29.182

/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/home/sujata/.ssh/id_rsa.pub"

The authenticity of host '192.168.29.182 (192.168.29.182)' can't be established.

ECDSA key fingerprint is SHA256:np80a07ru0Ll2CvH8cVcFtTXVLx1RnftoONS1OL0cJQ.

Are you sure you want to continue connecting (yes/no/[fingerprint])? yes

/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed

/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys

sujata@192.168.29.182's password:

Number of key(s) added: 1

Now try logging into the machine, with:   "ssh 'sujata@192.168.29.182'"

and check to make sure that only the key(s) you wanted were added.

Now, you can use ssh to the remote system without using any password:

$ ssh  sujata@192.168.29.182

Last login: Wed Nov 17 09:11:15 2021

$ hostname

lx-centos

# How to create a directory structure in Linux?

You would learn about BASH brace expansion. For instance, the following command is a quick method to create subdirectories under one base directory. Here the base directory is jupiter. Do not forget the slash, otherwise the result will be different.

$ mkdir -p jupiter/{Io,Europa,Ganymede,Callisto}

$ cd jupiter

$ ls -l

total 0

drwxrwxr-x. 2 liza liza 6 Nov 16 15:04 Callisto

drwxrwxr-x. 2 liza liza 6 Nov 16 15:04 Europa

drwxrwxr-x. 2 liza liza 6 Nov 16 15:04 Ganymede

drwxrwxr-x. 2 liza liza 6 Nov 16 15:04 Io

You should learn to create empty files using the touch command. It is a nice way to test for permission related errors.

$ touch hello123

# How do I work with compressed files?

The compressed files have common usage among the Linux users. If someone must send you a log for troubleshooting, she will invariably compress the logs using the tar command to decrease the byte size of the log. If she uses the tar command, the compressed file is called a tarball.

Let us look at the file fox.txt

$ ls -l fox.txt

-rw-rw-r--. 1 liza liza 14859 Nov 16 15:12 fox.txt

The size is 14859 bytes.

Using the gzip to compress the file.

$ gzip fox.txt

$ ls -l

total 4

-rw-rw-r--. 1 liza liza 139 Nov 16 15:12 fox.txt.gz

The file is now only 139 bytes. Wow!

To unzip, use the following command:

$ gunzip fox.txt.gz

There is another compression command that you can use, which is bzip2 .

$ bzip2 fox.txt

$ ls -l

total 4

-rw-rw-r--. 1 liza liza 149 Nov 16 15:12 fox.txt.bz2

To unzip the command is bunzip2 .

There is another newer compression command called xz .

$ xz fox.txt

$ ls -l

total 4

-rw-rw-r--. 1 liza liza 164 Nov 16 15:12 fox.txt.xz

The decompression command is unxz .

The compression is done by these three compromission algorithms and not by tar.

Creating a tarball with gunzip

tar -cvzf fox.tar.gz fox.txt

Creating a tarball with bzip2

tar -cvjf fox.tar.bz2 fox.txt

Creating a tarball with xz

tar -cvJf fox.tar.xz fox.txt

Note:

Please do not go by my compression results, as I have used a small sized file. Your results would be much better.

# Can you explain about file/directory permissions?

Many people leave their organizations but forget to disclose the directory and file permissions and group members would not be able to access those directories.

Please see the following example, the user prabal has left the organization but the common directory is owned by him. And there is no permission for the group or the world.

When the user liza tries to access the directory, she is not able to.

$ ls -l

total 0

drwx------. 2 prabal prabal 6 Nov 16 15:53 common

$ cd common

-bash: cd: common: Permission denied

What you need to do is give the directory 777 permission and liza will be able to access the directory.

As root:

# chmod 777 common/

As liza, as you can see she is able to access the directory.

$ pwd

/opt/common

$ id

uid=1001(liza) gid=1001(liza) groups=1001(liza) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023

For file permission, make sure you give 666 permissions for all files in the common directory, but there is no executable permission.

# chmod 666 * -R common

See the content of common .

# ls -l

total 0

drwxr-xr-x. 2 root root 6 Nov 16 16:11 hello123

The executable permission should be removed using the following command:

# chmod -x * -R

# ls -l

total 0

drw-r--r--. 2 root root 6 Nov 16 16:11 hello123

# What are symbolic links?

Symbolic errors are common and can confuse even experienced system administrators.

There are two kinds of symbolic links in Linux:

1)      Soft links

2)      Hard Links

When you create a softlink to an existing file, you create a different file.

When you create a hardlink to an existing, you create an exact clone of the file.

Both the softlinks and hardlinks are created using the ln command.

Creating a softlink using the lm command with -s flag

$ ln -s /etc/hosts hosts

Now, perform a ls -l command.

$ ls -l

total 0

lrwxrwxrwx. 1 liza liza 10 Nov 16 16:30 hosts -> /etc/hosts

The l in the permission stack represents that it is symbolic LINK file. And there is the arrow pointing to the location of the real file.

Yet, both the files whose contents are same, are also different. If you see the inode number ( a system that uniquely identifies a file on the file system – sort of a social security number).

$ ls -i hosts

4525881 hosts

$ ls -i /etc/hosts

4358377 /etc/hosts

When you create a hard link, you create an exact replica of the file. The symbolic had link is created without the -s flag. Please note that a hard symbolic link cannot TRAVERSE a different file system on the same system. While a soft symbolic link CAN.

# ln /etc/passwd passwd

# ls -i passwd

4527544 passwd

# ls -i /etc/passwd

4527544 /etc/passwd

As you can see both share the same inode number of 4527544.

What is a Linux BASH shell environment?

The shell is an interface between you and the system. It is a black hole of information that may take a lifetime to master as the changes are rapid. In the Linux world everything is a file. Which means a hardware device such as a Tape Drive to Linux it is a merely a file to write to or perform other actions.

The BASH or (Bourne Again Shell) is the default shell in many Linux distributions (like different Windows editions).

How to create an alias in the Linux Bash Shell environment? Or how to create my own Linux command?

An alias can be defined as a DOS batch file method to a command. Or creating a new personalized command for yourself. Let us create a command for the Squid Proxy server running on the system. We would call this alias as proxystat .

$ echo alias 'proxystat="service squid status"' >> ~/.bashrc

The command alias is used to create a new command called proxystat that means service squid status and is appended to the .bashrc file. This file should be present in your home directory and is one of the files to help create a personalized environment for you. If you do not have the .bashrc file in your home, create one using the touch command:

You must be in $HOME .
$ touch .bashrc

We need to refresh the environment by sourcing the .bashrc file so that the command proxystat is known to your environment. This can be done using the source command.

$ source .bashrc

Now, run your own command proxystat .

$ proxystat
Redirecting to /bin/systemctl status squid.service
● squid.service - Squid caching proxy
   Loaded: loaded (/usr/lib/systemd/system/squid.service; disabled; vendor preset: disabled)
   Active: active (running) since Mon 2021-11-15 14:00:37 IST; 20h ago
  Process: 9959 ExecStart=/usr/sbin/squid $SQUID_OPTS -f $SQUID_CONF (code=exited, status=0/SUCCESS)
  Process: 9954 ExecStartPre=/usr/libexec/squid/cache_swap.sh (code=exited, status=0/SUCCESS)
 Main PID: 9962 (squid)
   CGroup: /system.slice/squid.service
           ├─9962 /usr/sbin/squid -f /etc/squid/squid.conf
           ├─9964 (squid-1) -f /etc/squid/squid.conf
           └─9965 (logfile-daemon) /var/log/squid/access.log

  How to create a simple function on the Linux Bash shell environment?

To create a simple function that tells you much space a directory has occupied, we would employ $1 which is a positional parameters and is the first placeholder after the command name and the command du -h which gives us the space details.

The following lines have to be added to your .bashrc file

function spaceinfo()
{
        du -h /home/$1;
}

Now, you need source the .bashrc file. The name of the function is spaceinfo.

$ source .bashrc

$ spaceinfo liza
4.0K    /home/liza/.ssh
8.0K    /home/liza/interns
0       /home/liza/p3
2.2M    /home/liza

# How I do collect the IP address, gateway, subnet mask and DNS servers from a system?

Step 1:

Check if Network Manager is running using the following command:

$ systemctl status NetworkManager

● NetworkManager.service - Network Manager

   Loaded: loaded (/usr/lib/systemd/system/NetworkManager.service; enabled; vendor preset: enabled)

   Active: active (running) since Thu 2021-11-11 11:18:01 IST; 5 days ago

     Docs: man:NetworkManager(8)

Main PID: 647 (NetworkManager)

   CGroup: /system.slice/NetworkManager.service

           ├─647 /usr/sbin/NetworkManager --no-daemon

           └─743 /sbin/dhclient -d -q -sf /usr/libexec/nm-dhcp-helper -pf /var/run/dhclient-enp0s3.pid -lf...

Step 2:

Look for the active network interface using the command:

$ nmcli c show

NAME     UUID                                  TYPE            DEVICE

enp0s3   ac113210-a008-43fa-b398-1fd052d81165  802-3-ethernet  enp0s3

The active device is enp0s3.

Step 3:

For the information you want, the output of the following command provides detailed data.

$ nmcli d show enp0s3

GENERAL.DEVICE:                         enp0s3

GENERAL.TYPE:                           ethernet

GENERAL.HWADDR:                         08:00:27:                                                            4C:46:F9

GENERAL.MTU:                            1500

GENERAL.STATE:                          100 (connected)

GENERAL.CONNECTION:                     enp0s3

GENERAL.CON-PATH:                       /org/free                                                            desktop/NetworkManager/ActiveConnection/1

WIRED-PROPERTIES.CARRIER:               on

IP4.ADDRESS[1]:                         192.168.29.182/24

IP4.GATEWAY:                            192.168.29.1

IP4.DNS[1]:                             192.168.29.1

IP6.ADDRESS[1]:                         2405:201:                                                            4003:80cc:984a:902d:2637:d53d/64

IP6.ADDRESS[2]:                         fe80::e19                                                            d:c87:e029:81cc/64

IP6.GATEWAY:                            fe80::e62                                                            6:86ff:fe1e:c77c

IP6.ROUTE[1]:                           dst = 240                                                            5:201:4003:80cc::/64, nh = ::, mt = 100

IP6.DNS[1]:                             2405:201:                                                            4003:80cc::c0a8:1d01

[liza@lx-centos ~]$ nmcli d show enp0s3

GENERAL.DEVICE:                         enp0s3

GENERAL.TYPE:                           ethernet

GENERAL.HWADDR:                         08:00:27:4C:46:F9

GENERAL.MTU:                            1500

GENERAL.STATE:                          100 (connected)

GENERAL.CONNECTION:                     enp0s3

GENERAL.CON-PATH:                       /org/freedesktop/NetworkManager/ActiveConnection/1

WIRED-PROPERTIES.CARRIER:               on

IP4.ADDRESS[1]:                         192.168.29.182/24

IP4.GATEWAY:                            192.168.29.1

IP4.DNS[1]:                             192.168.29.1

IP6.ADDRESS[1]:                         2405:201:4003:80cc:984a:902d:2637:d53d/64

IP6.ADDRESS[2]:                         fe80::e19d:c87:e029:81cc/64

IP6.GATEWAY:                            fe80::e626:86ff:fe1e:c77c

IP6.ROUTE[1]:                           dst = 2405:201:4003:80cc::/64, nh = ::, mt = 100

IP6.DNS[1]:                             2405:201:4003:80cc::c0a8:1d01

What do I do with DNS on Linux?

If you are a system administartor or anyone who is in-charge of your Linux systems for your home office or small business. You have to know about the DNS settings on the Linux systems ( for that matter even on your Windows Systems).

It is the translating protocol that translates your domainname such  [www.foo.com](http://www.foo.com/)  to an IP address.

To check if your system is configured correctly, here are some of the DNS troubleshooting commands that would be handy to you.

The host command translates the  [www.yahoo.com](http://www.yahoo.com/)  to its corresponding IP address, specific to my region.

$host  [www.yahoo.com](http://www.yahoo.com/)

The expected result is

$ host  [www.yahoo.com](http://www.yahoo.com/)
[www.yahoo.com](http://www.yahoo.com/)  is an alias for  [new-fp-shed.wg1.b.yahoo.com](http://new-fp-shed.wg1.b.yahoo.com/) .
[new-fp-shed.wg1.b.yahoo.com](http://new-fp-shed.wg1.b.yahoo.com/)  has address 202.165.107.50
[new-fp-shed.wg1.b.yahoo.com](http://new-fp-shed.wg1.b.yahoo.com/)  has address 202.165.107.49
[new-fp-shed.wg1.b.yahoo.com](http://new-fp-shed.wg1.b.yahoo.com/)  has IPv6 address 2406:2000:e4:1605::9001
[new-fp-shed.wg1.b.yahoo.com](http://new-fp-shed.wg1.b.yahoo.com/)  has IPv6 address 2406:2000:e4:1605::9000

If there is a DNS issue, the expected result is
;; connection timed out; no servers could be reached.

To check which DNS servers you have on your LINUX system, you need to see what your resolv.conf says:

In my case it is 192.168.29.1 - which is the IP address of the Broadband DSL modem which provides me DNS services.

$ cat /etc/resolv.conf
# Generated by NetworkManager
nameserver 192.168.29.1
nameserver 2405:201:4003:80cc::c0a8:1d01

To check the interfaces you have, you need to use the Network Manager:

$ nmcli con show
NAME    UUID                                  TYPE      DEVICE
enp0s3  7b1642d8-222e-46f9-8f9d-c1b6d3c5bd42  ethernet  enp0s3
virbr0  c9e04188-1c13-402e-9d0b-e05751725264  bridge    virbr0

We have the ethernet interface and another bridge interface created by the Virtual Machine software.

To see the DNS settings of each interface, use the commands:

$ nmcli -f ipv4.dns con show enp0s3
ipv4.dns:                               --

$ nmcli -f ipv4.dns con show  virbr0
ipv4.dns:                              --

We can see that none of the interfaces have any DNS settings, to rectify to use the DSL server's DNS service, follow the steps:

1) Login as root.
2) But please use SUDO.

# nmcli con mod "enp0s3" ipv4.dns "192.168.29.1"

Check the DNS setting for the interface enp0s3.

# nmcli -f ipv4.dns con show enp0s3
ipv4.dns:              192.168.29.1

To restart the service use the command

#nmcli con up "enp0s3"

How do I monitor network access on my environment?

You would need to monitor network traffic between two nodes. It is more common that you think that too during the COVID era when everyone is using VPN. So if you are working from home and suffering from slow application response (particularly the applications that rely on TCP/IP's client/server methodology).

Consider system A which Centos 7 and system B which is Centos 8\. We would send traffic using Linux NETCAT command over a TCP port 5000 (you can use other free TCP ports on your systems as well). And the free monitoring tool iptraf would capture the traffic for you to analyze.

Install iptraf-ng and nc on both the servers:

# yum install iptraf-ng nc

Configure the IPTRAF utility:
Start iptraf using the command

#iptraf-ng

![Graphical user interface Description automatically generated](Image00000.jpg)

Selecting the interface:
  ![Treemap chart Description automatically generated](Image00001.gif)

NOTE:
I have selected the interface enp0s3. Please note that logging is off by default, and you need to make it on. Go to configure and toggle L to enable logging to ON.
Now, go select the interface and put the logs in a directory of your choice.

![Graphical user interface, text, application Description automatically generated](Image00002.jpg)

To generate useful traffic, start netcat on server A on port 5000:

# nc -l 5000

And go over to server B and start talking to this system via netcat.

nc 192.168.29.182 5000
The IP address is of the Server A. Generate some traffic by saying "hello" etc.
Now if you grep the log for 5000, you would see something like:

$ grep 5000 network.log
Tue Nov 16 12:07:02 2021; TCP; enp0s3; 70 bytes; from  [192.168.29.182:5000](http://192.168.29.182:5000/)  to  [192.168.29.32:51294](http://192.168.29.32:51294/) ; first packet
Tue Nov 16 12:07:02 2021; TCP; enp0s3; 52 bytes; from  [192.168.29.32:51294](http://192.168.29.32:51294/)  to  [192.168.29.182:5000](http://192.168.29.182:5000/) ; first packet
Tue Nov 16 12:07:40 2021; TCP; enp0s3; 52 bytes; from  [192.168.29.32:51294](http://192.168.29.32:51294/)  to  [192.168.29.182:5000](http://192.168.29.182:5000/) ; FIN sent; 5 packets, 295 bytes, avg flow rate      0.06 kbps
Tue Nov 16 12:07:40 2021; TCP; enp0s3; 52 bytes; from  [192.168.29.182:5000](http://192.168.29.182:5000/)  to  [192.168.29.32:51294](http://192.168.29.32:51294/) ; FIN acknowleged
Tue Nov 16 12:07:40 2021; TCP; enp0s3; 52 bytes; from  [192.168.29.182:5000](http://192.168.29.182:5000/)  to  [192.168.29.32:51294](http://192.168.29.32:51294/) ; FIN sent; 5 packets, 278 bytes, avg flow rate      0.06 kbps
Tue Nov 16 12:07:40 2021; TCP; enp0s3; 52 bytes; from  [192.168.29.32:51294](http://192.168.29.32:51294/)  to  [192.168.29.182:5000](http://192.168.29.182:5000/) ; FIN acknowleged

# How to work with text files on Linux?

A text file is an ASCII file, to identify a text file, you need to use the file command.

For example:

# file hosts

hosts: ASCII text

Now, consider the file fox.txt which has the following content:

$ cat fox.txt

The quick brown fox jumps over the lazy dog

The quick brown fox jumps over the lazy dog

The quick brown fox jumps over the lazy dog

The quick brown fox jumps over the lazy dog

The quick brown fox jumps over the lazy dog

If you want to replace the word lazy with clever you can do it using the sed command.

$ sed -i 's/lazy/clever/g' fox.txt

$ cat fox.txt

The quick brown fox jumps over the clever dog

The quick brown fox jumps over the clever dog

The quick brown fox jumps over the clever dog

The quick brown fox jumps over the clever dog

The quick brown fox jumps over the clever dog

Where -i stands for in-place replacement, s for substitution and g for global existence of lazy.

# Can you provide an example of regular expressions?

Regular expressions are used in the shell and programmatic level to match yet unknown characters/strings. It is a complicated subject, and you must study more books to understand it.

The ^ indicates a pattern at the beginning of a line, for example it can used in the following manner:

# grep ^refresh_pattern squid.conf

refresh_pattern ^ftp:           1440    20%     10080

refresh_pattern ^gopher:        1440    0%      1440

refresh_pattern -i (/cgi-bin/|\?) 0     0%      0

refresh_pattern .                0       20%     4320

The $ indicates pattern at the end, the grep command finds all the instances of http at the end of the line.

# grep http$ squid.conf

acl Safe_ports port 80          # http

acl Safe_ports port 488         # gss-http

acl Safe_ports port 777         # multiling http

How to set a Static IP address on Linux?

The first step that you need to do is identify the interface that you have using the following command:

$ nmcli c
NAME    UUID                                  TYPE      DEVICE
enp0s3  7b1642d8-222e-46f9-8f9d-c1b6d3c5bd42  ethernet  enp0s3
virbr0  c9e04188-1c13-402e-9d0b-e05751725264  bridge    virbr0

The interface name is  enp0s3.

Let us again more info about enp0s3 by using the command:

$ nmcli d show enp0s3
GENERAL.DEVICE:                         enp0s3
GENERAL.TYPE:                           ethernet
GENERAL.HWADDR:                         08:00:27:92:4E:8C
GENERAL.MTU:                            1500
GENERAL.STATE:                          100 (connected)
GENERAL.CONNECTION:                     enp0s3
GENERAL.CON-PATH:                       /org/freedesktop/NetworkManager/ActiveC>
WIRED-PROPERTIES.CARRIER:               on
IP4.ADDRESS[1]:                          [192.168.29.32/24](http://192.168.29.32/24)
IP4.GATEWAY:                            192.168.29.1
IP4.ROUTE[1]:                           dst =  [0.0.0.0/0](http://0.0.0.0/0) , nh = 192.168.29.1, mt >
IP4.ROUTE[2]:                           dst =  [192.168.29.0/24](http://192.168.29.0/24) , nh = 0.0.0.0, mt>
IP4.DNS[1]:                             192.168.29.1
IP6.ADDRESS[1]:                         2405:201:4003:80cc:9c47:139c:3724:4bf/64
IP6.ADDRESS[2]:                         fe80::fd7c:3d3f:2a54:d54f/64
IP6.GATEWAY:                            fe80::e626:86ff:fe1e:c77c
IP6.ROUTE[1]:                           dst = 2405:201:4003:80cc::/64, nh = ::,>
IP6.ROUTE[2]:                           dst = ::/0, nh = fe80::e626:86ff:fe1e:c>
IP6.ROUTE[3]:                           dst = fe80::/64, nh = ::, mt = 100
IP6.ROUTE[4]:                           dst = ff00::/8, nh = ::, mt = 256, tabl>
IP6.DNS[1]:                             2405:201:4003:80cc::c0a8:1d01

Instead of the card getting the IP v4 from my DSL modem, it would be set manually, we have all the information we need to set the static IP
address from the above command:

IP4.ADDRESS[1]:                          [192.168.29.32/24](http://192.168.29.32/24)
IP4.GATEWAY:                            192.168.29.1
IP4.DNS[1]:                             192.168.29.1

Login as root or use SUDO and enter the following command:

# nmcli c mod enp0s3 ipv4.method manual ipv4.addresses  [192.168.29.32/24](http://192.168.29.32/24)  ipv4.gateway 192.168.29.1 ipv4.dns 192.168.29.1

Now, we can confirm that the setting is done manually by using the following command.

# nmcli c show enp0s3 | grep ipv4

ipv4.method:                            manual
ipv4.dns:                               192.168.29.1
ipv4.dns-search:                        --
ipv4.dns-options:                       --
ipv4.dns-priority:                      0
ipv4.addresses:                          [192.168.29.32/24](http://192.168.29.32/24)
ipv4.gateway:                           192.168.29.1
ipv4.routes:                            --
ipv4.route-metric:                      -1
ipv4.route-table:                       0 (unspec)
ipv4.routing-rules:                     --
ipv4.ignore-auto-routes:                no
ipv4.ignore-auto-dns:                   no
ipv4.dhcp-client-id:                    --
ipv4.dhcp-iaid:                         --
ipv4.dhcp-timeout:                      0 (default)
ipv4.dhcp-send-hostname:                yes
ipv4.dhcp-hostname:                     --
ipv4.dhcp-fqdn:                         --
ipv4.dhcp-hostname-flags:               0x0 (none)
ipv4.never-default:                     no
ipv4.may-fail:                          yes
ipv4.dad-timeout:                       -1 (default)
ipv4.dhcp-vendor-class-identifier:      --

To confirm start the network service

# systemctl restart NetworkManager.service

Note: NetworkManager.service was restarted on RHEL 8.

How do I see the status of the TCP port?

The daemons are listener services that employ TCP ports to listen for client requests. A daemon is a background process.

For example, Apache runs on port 80 and squid proxy server runs on 3128, if you need to verify if the TCP ports are active and in listening mode, you should use the following command:

$ ss -lntp | grep :3128
LISTEN     0      128         :::3128                    :::*
This command means that squid is listening at port 3128.

$ ss -lntp | grep :80

This returns back to the prompt indicating that the Apache is not running on the system.

How to see the firewall status on Linux?

To check the status of the firewall, use the command with root access:

Start or restart:
# systemctl start firewalld

Check the status:
# systemctl status firewalld
● firewalld.service - firewalld - dynamic firewall daemon
   Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; vendor p>
   Active: active (running) (thawing) since Fri 2021-11-19 19:46:30 IST; 2s ago
     Docs: man:firewalld(1)
 Main PID: 162379 (firewalld)
    Tasks: 2 (limit: 4795)
   Memory: 31.4M
   CGroup: /system.slice/firewalld.service
           └─162379 /usr/libexec/platform-python -s /usr/sbin/firewalld --nofor>

Nov 19 19:46:29 lx-centos8 systemd[1]: Starting firewalld - dynamic firewall da>
Nov 19 19:46:30 lx-centos8 systemd[1]: Started firewalld - dynamic firewall dae>
Nov 19 19:46:31 lx-centos8 firewalld[162379]: WARNING: AllowZoneDrifting is ena>

The command to check firewall settings, enter the command:

#  firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3
  sources:
  services: cockpit dhcpv6-client ssh
  ports:
  protocols:
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:

The firewalld has multiple ZONES and this information pertains to the PUBLIC zone. We see that the DHCP client and ssh are among the services allowed.

# How do I check local resolution on my Linux machine?

Local resolution is the enabling of translation of a hostname/domainname to an IP address. For this we need to check the /etc/nssswitch.conf file and make sure that you have the entry:

hosts:      files dns myhostname

Which means that resolution would take place via your /etc/hosts . Let us open the /etc/hosts file add the entry

192.168.29.32 www.lx-centos8.com

Conduct the ping test if the resolution is complete:

# ping www.lx-centos8.com

PING www.lx-centos8.com (192.168.29.32) 56(84) bytes of data.

64 bytes from www.lx-centos8.com (192.168.29.32): icmp_seq=1 ttl=64 time=0.036 ms

64 bytes from www.lx-centos8.com (192.168.29.32): icmp_seq=2 ttl=64 time=0.052 ms

64 bytes from www.lx-centos8.com (192.168.29.32): icmp_seq=3 ttl=64 time=0.039 ms
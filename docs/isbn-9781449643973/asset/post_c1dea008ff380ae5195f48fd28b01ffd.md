
- What is the purpose of enabling syncookies in the Linux Kernel?
- When you want to enable a Linux Kernel command and enable it immediately without a physical reboot of the system, what command must you enable in front of the command parameter? Explain what the following command will do: echo "1" > /proc/sys/net/ipv4/ip_forward
- If you wanted to limit the number of files that a user can open simultaneously on the Fedora Linux Server to a maximum of 1, what is the command syntax you need to enable in the Linux Kernel?
- What is the best way to make a system-wide permanent change to the kernel to enable syncookies?
- Given a system that has been freshly installed your boss wants you to make sure it is up to date and locked down at the Kernel level. What steps would you take to verify what modules are loaded into the Kernel and how would you go about locking them down?
- What would you enable to set the Kernel to debug mode? Why would someone choose to enable this?
- What is the relation between sysctl.conf and the sysctl command?
- If you wanted to modify a kernel parameter without editing the sysctl.conf file would it be possible? If yes, please give the example.

## Laboratory #8

## Lab #8: Implement Best Practices for Secure Software Management

### Learning Objectives and Outcomes

Upon completing this lab, students will be able to complete the following tasks:

- Recommend security settings after discovering all installed packages in the kernel to help evaluate the security measures that are necessary
- Configure the RPM database to add repositories securely for the distribution of software to persons that do not need access to the system directly, only to download any updates or RPMs
- Verify a source tar ball to determine whether the integrity and contents of the package are what you expect before executing or installing it
- Use and leverage MD5Sum to verify the integrity of a downloaded software tar ball
- Use wget to acquire and install third party software onto the Linux system from the Internet

### Required Setup and Tools

This lab does not require the use of the Mock IT Infrastructure - Cisco core backbone network. In addition, the Instructor VM workstation and Student VM workstations should be physically disconnected from the internal network and be isolated on the classroom dedicated layer 2 switch. This will allow for a shared DHCP server to be used to allocate the IP addresses for the instructor and student workstations.

The following is required for this equipment-based lab:

- A) A classroom workstation (with at least 2 Gig RAM) capable of supporting the removable hard drive with the VM server farm connected to the classroom layer 2 switch.
- B) An instructor workstation (with at least 4 Gig RAM recommended) that shall act as the Instructor’s demo lab workstation. The instructor will display the Instructor workstation on the LCD projector to demo the loading and configuring of the Instructor VM workstation using VMware Player.
- C) Students Lab workstations will use their own VM server farm and VM student workstation. VMware Player will be used to run the Student VM and the Target VM.

The following summarizes the setup, configuration, and equipment needed to perform Lab #8:

1. A **Virtualized Server Farm** with the following components:
   - a. Microsoft DHCP server for allocating student IP host addresses
   - b. A Student and/or Instructor VM workstation
   - c. Fedora Linux Target VM
2. Standard onsite student workstation must have the following software applications loaded to perform this lab:
   - a. VMware Player 3.x
   - b. Microsoft Office 2007 or higher for Lab Assessment Questions & Answers

### Recommended Procedures

**Equipment-Based Lab #8 – Student Steps:**

Students should perform the following steps:

1. Connect the student-removable hard drive to your workstation
2. Boot up the Student VM and Microsoft DHCP VM server to allocate an IP host address
3. Enable your DOS command prompt and type “ipconfig” and “ping” your allocated IP host address 172.30.0.___ , the DHCP server 172.30.0.10, and the IP default gateway router 172.30.0.1
4. Login to the Student VM using the following credentials:
   - Login ID: “student” (case sensitive)
   - Password: “ISS316Security” (case sensitive)
5. From the GNOME Desktop, at the top left side, click on “Applications” -> Systems Tools -> Terminal

> **NOTE:** For proper completion of this lab your Fedora 14 VM will require a **LIVE** Internet connection. Do **NOT** disconnect the student workstations from the classroom network and Internet connection.

> **NOTE:** Before the sudo & su commands can execute as expected, the user account **MUST** be a member of the wheel group with the wheel group granted limited sudo access as directed in Lab 3.

### Using RPM to Perform Software Management Tasks

6. View all files associated with the sendmail package. Type the command: `rpm -ql sendmail | less` and press <enter>. Use the up & down arrow keys to scroll.

```
[student@TargetFedora01 ~]$ rpm -ql sendmail | less
```

![](img/73be0eef2ceb12f43f3eb92c420134f5_87_0.png)

7. Press the "q" key to exit and return to the command prompt.

8. Discover which package the `/bin/ls` executable belongs to. Type the command: `rpm -qf /bin/ls` and press <enter>

```
[student@TargetFedora01 ~]$ rpm -qf /bin/ls
```

![](img/73be0eef2ceb12f43f3eb92c420134f5_87_1.png)

9. Verify the integrity of files in the httpd package. Type the command: `sudo rpm -V httpd` and press <enter>.

> **Note:** If no changes have been made to any file belonging to the software package, no output will return. However, if a file has changed, output will be displayed. If the `/etc/httpd/conf/httpd.conf` has been altered as directed in Lab 7, output similar to the following should display:

```
[student@TargetFedora01 ~]$ sudo rpm -V httpd
S.5....T.   c /etc/httpd/conf/httpd.conf
```

![](img/73be0eef2ceb12f43f3eb92c420134f5_87_2.png)

Use the table below to determine what type of change has been made to a particular file.

| Flag | Description |
|---|---|
| S | Size change |
| M | Permissions changed |
| 5 | MD5 Changed |
| L | Symlink Changed |
| D | Device changed |
| U | User change |
| G | Group change |
| Missing | File has been deleted or moved |

**Table 1 - Symbol lookup when verifying integrity of packages**

10. Search for all installed packages currently installed on the computer. Type the command: `rpm -qa | less` and press <enter>. Use the arrow keys on the keyboard to scroll up or down.
11. Press the “ q ” key to exit and return to the command prompt.

### Download a Software Application via the Internet & Verify Integrity Using MD5Sum Hashing

12. Install wget software. Type the command: `sudo yum install wget -y` and press <enter>. If prompted for a password, enter the password for the student user (ISS316Security).
13. Download Python source code. Type the command: `wget http://www.python.org/ftp/python/2.6.5/Python-2.6.5.tgz` and press <enter>

```
[student@TargetFedora01 ~]$ wget http://www.python.org/ftp/python/2.6.5/Python-2.6.5.tgz
```

**Figure 44 – Downloading source code files from the Internet**

14. Open Web Browser. From the GNOME Desktop menu, *click on* “Applications” on the top left menu, then Internet->Firefox to open the Firefox web browser.

![](img/73be0eef2ceb12f43f3eb92c420134f5_89_0.png)

15. Enter the URL. Type in address bar: `http://www.python.org/download/releases/2.6.5/`

16. Locate and read a checksum. Scroll until the following syntax is located. The particular checksum on the web site for `Python-2.6.5.tgz` should match the downloaded `Python-2.6.5.tgz`.

MD5 checksums and sizes of the released files:

```text
cd04b5b9383c6c1fccdaa991af762cf4   13209175   Python-2.6.5.tgz
6bef0417e71a1a137ccc5750420fdb3    11095581   Python-2.6.5.tar.bz2
9cd2c4d23dea7dfcd964449c3008f042   15430656   python-2.6.5.amd64.msi
0b6bc43c45fb2e3195ec2daf3fad59fc2   15103488   python-2.6.5.msi
84489bba813fd36b6041b69d4310a86da   20348693   python-2.6.5-macosx10.3-2010-03-24.dmg
```

Figure 46 – List of MD5 checksums located on python.org

17. Verify downloaded checksum. Type the command: `md5sum Python-2.6.5.tgz` and press <enter> and verify the checksum matches that from the Step 15.

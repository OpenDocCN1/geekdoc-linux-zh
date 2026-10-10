
```bash
[student@TargetFedora01 ~]$ su -c 'setfacl -m g:wheel:r /var/log/messages:'
Password:
[student@TargetFedora01 ~]$ getfacl /var/log/messages
getfacl: Removing leading '/' from absolute path names
# file: var/log/messages
# owner: root
# group: root
user::rw-
group::r--
group:wheel::r--
mask::r--
other::r--
```

![](img/73be0eef2ceb12f43f3eb92c420134f5_25_0.png)

Congratulations, you have just implemented basic security hardening in your Fedora Linux Server.

## Deliverables

Upon completion of Lab #2: Configure Basic Security Controls for a Linux Server, students are required to provide the following deliverables:

- 1. Lab #2 – Screen captures of your Fedora Linux Server system hardening configuration:
    - a. boot/grub/grub.conf file
    - b. /etc/selinux/config file
    - c. “chkconfig --list | grep iptables” command
    - d. getfacl /var/log/messages command
    - e. lsattr /etc/services command
    - f. getfacl /var/log/messages command
- 2. Lab #2 – Lab Assessment Questions & Answers

## Evaluation Criteria and Rubrics

The following are the evaluation criteria and rubrics for Lab #2 that the students must perform:

- 1. Was the student able to configure the bootloader with timeout set to 0 and password credential to mitigate tampering with the GRUB loader and the boot sequence of the server? – [10%]
- 2. Was the student able to enable SELinux on a Fedora Linux Server and set it to “permissive” mode? – [10%]
- 3. Was the student able to create a student user account and to add it to a user group for managing permissions and applying access controls across the system? – [20%]
- 4. Was the student able to configure user groups with limited sudo access (with password credentials) to log and properly monitor access across the system? – [20%]
- 5. Was the student able to create iptables set to "on" for runlevels 3 & 5 to enable an internal, host-based IP stateful firewall? – [20%]
- 6. Was the student able to set restrictions and permissions for user access to files and system log files? – [20%]

## Lab #2 – Assessment Worksheet

### Configure Basic Security Controls on a Fedora Linux Server

Course Name & Number: ____________________

Student Name: ____________________

Instructor Name: ____________________

Lab Due Date: ____________________

## Overview

The students are required to submit their lab assessment answers using this Microsoft Word document template. All lab assessment questions listed are for each course’s weekly lab activity. This may be a paper-based activity or an equipment-based lab activity. Lab assessment results and answers are due at the beginning of class the following week. Students are encouraged to perform and submit their lab assessment results immediately upon completion of the lab activity or prior to the due date. During this lab they will properly secure a Linux server system. They will perform steps to secure the bootloader, enable iptables and run SELinux to help lock down the Linux OS. The students will also apply ACLs to directories and files and then check those ACLs and permissions on the system.

## Lab Assessment Questions & Answers

- 1. What is GRUB and why is it important to lock it down?
- 2. Discuss the purpose of granting “sudo” access. Why is it a good idea not to login as root user?
- 3. If a file is set with the immutable flag, what security controls does this provide for the file?
- 4. Why do you get blank window when trying to edit grub with “vi”?
- 5. How do you know when you login as root?
- 6. What command do you need to use to install vim?
- 7. What is iptables and how does this help harden the Fedora Linux Server?
- 8. Why is it important to configure and enable iptables on your Fedora Linux Server?
- 9. What is the difference between the commands `cat` and `less`?
- 10. What is the difference between `setfacl` and `getfacl`? How can "setfacl" help achieve security hardening?

## Laboratory #3

Lab #3: Apply Hardened User Account Management & Security Controls

## Learning Objectives and Outcomes

Upon completing this lab, students will be able to complete the following tasks:

- Configure a password policy by editing the /etc/login.defs file and implementing stringent password security measures on a Fedora Linux Server
- Enforce a password change every 60 days showing a warning 14 days prior to the password’s expiration across the system for all users
- Configure a minimum password length of 8 characters with stringent complexity requirements
- Create users and groups with the proper permissions and restrictions to enforce role-based access controls
- Create a temporary user account that expires in 90 days to enforce the proper principle of least privilege with contractors and temporary workers/consultants

## Required Setup and Tools

This lab does not require the use of the Mock IT Infrastructure - Cisco core backbone network. In addition, the Instructor VM workstation and Student VM workstations should be physically disconnected from the internal network and be isolated on the classroom dedicated layer 2 switch. This will allow for a shared DHCP server to be used to allocate the IP addresses for the instructor and student workstations. The following is required for this equipment-based lab:

- A) A classroom workstation (with at least 2 Gig RAM) capable of supporting the removable hard drive with the VM server farm connected to the classroom layer 2 switch.
- B) An instructor workstation (with at least 4 Gig RAM recommended) that shall act as the Instructor’s demo lab workstation. The instructor will display the Instructor workstation on the LCD projector to demo the loading and configuring of the Instructor VM workstation using VMware Player.
- C) Students Lab workstations will use their own VM server farm and VM student workstation. VMware Player will be used to run the Student VM and the Target VM.

The following summarizes the setup, configuration, and equipment needed to perform Lab #3:

- 1. A Virtualized Server Farm with the following components:
    - a. Microsoft DHCP server for allocating student IP host addresses
    - b. A Student and/or Instructor VM workstation
    - c. Fedora Linux Target VM
- 2. Standard onsite student workstation must have the following software applications loaded to perform this lab:
    - a. VMware Player 3.x
    - b. Microsoft Office 2007 or higher for Lab Assessment Questions & Answers

## Recommended Procedures

### **Equipment-Based Lab #3 – Student Steps:**

Students should perform the following steps:

- 1. Connect the student-removable hard drive to your workstation
- 2. Boot up the Student VM and Microsoft DHCP VM server to allocate an IP host address
- 3. Enable your DOS command prompt and type “ipconfig” and “ping” your allocated IP host address 172.30.0.____ , the DHCP server 172.30.0.10, and the IP default gateway router 172.30.0.1
- 4. Login to the Student VM using the following credentials:
    - Login ID: “student” (case sensitive)
    - Password: “ISS316Security” (case sensitive)
- 5. From the GNOME Desktop, at the top left side, click on “Applications” -> Systems Tools -> Terminal

![](img/73be0eef2ceb12f43f3eb92c420134f5_32_0.png)

## Configure Stringent Passwords as Per Policy Requirements

- 6. Open and edit the `/etc/login.defs` file to enforce:
    - a. a password change every 60 days
    - b. show a warning 14 days prior to the password expiring
    - c. Require a minimum password length of 8 characters
    - Type the command: `su -c 'vi /etc/login.defs'` and press <enter>.
- 7. Password: ISS316Security

```bash
[student@TargetFedora01 ~]$ su -c 'vi /etc/login.defs'
Password: 
```

**Figure 13 – Opening a file in vi as root user**

- 8. Press the “ i “ to enter **INSERT** mode in the vi editor.
- 9. Change Password aging controls as shown in figure below:

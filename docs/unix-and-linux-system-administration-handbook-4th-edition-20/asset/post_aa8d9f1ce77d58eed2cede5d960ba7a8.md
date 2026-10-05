
## 7.12 RECOMMENDED READING

- A secure web interface for management that’s accessible both inside and outside the enterprise
- The ability to easily display all users who have a certain set of privileges
- An easy way to see all the privileges granted to a particular user
- The ability to let users change (and reset) their own passwords, with enforcement of rules for picking strong passwords
- The ability for users to change their passwords globally in one operation
- A workflow engine; for example, tiered approvals before a user is given certain privileges
- The ability to coordinate with a personnel database to automatically delete access for employees who are terminated or laid off
- Configurable logging of all changes and administrative actions
- Configurable reports based on logging data (by user, by day, etc.)
- Role-based access control, including user account provisioning by role
- An interface through which hiring managers can request that accounts be provisioned according to role
- Exceptions to role-based provisioning, including a workflow for the approval of exceptions

Consider also how the system is implemented at the point at which authorizations and authentications actually take place. Does the system require a custom agent to be installed everywhere, or does it conform itself to the underlying systems?

“The Complete Buyer’s Guide for Identity Management.” Sun Microsystems white paper. 2008. sun.system-news.com/articles/129/4/sec/20930.

## 7.13 EXERCISES

- E7.1 How is a user's default group determined? How would you change it?
- E7.2 Explain the differences among the following umask values: 077, 027, 022, and 755. How would you set one of these values as a site-wide default for new users? Can you impose a umask standard on your users?
- E7.3 What is the purpose of the shadow password file?
- E7.4 Determine what authentication system the login program on your system uses. If you use PAM, determine what other programs on the system use PAM.
- E7.5 List the steps needed to add a user to a system without using useradd. What extra steps are needed for your local environment?
- E7.6 Determine the naming convention for new users at your site. What are the rules? How is uniqueness preserved? Can you think of any draw-backs? How are users removed?
- E7.7 Find a list of names (from an on-line telephone directory, perhaps) and use it as the input to a script that forms login names according to the naming convention at your site. How many users can you accommodate before you have a collision? How many collisions are there overall? Use the data to evaluate your site's naming convention, and suggest improvements.
- E7.8 Write a script to monitor the health of your /etc/passwd file. (Parts b and require root access unless you're clever.)
  a) Find any entries that have UID 0.
  b) Find any entries that have no password (/etc/shadow).
  c) Find any entries that have duplicate UIDs.
  d) Find any entries that have duplicate login names.
  e) Find any entries that have no expiration date (/etc/shadow).
- E7.9 Write a PAM module to perform authentication by randomly generating a PIN code, sending it to the user's cell phone as an SMS message, and prompting the user to enter the PIN code for verification. Install your module and configure it into the PAM login stack to achieve two-factor authentication.

## 8 Storage

UNIX storage is looking more and more like a giant set of Lego blocks that you can put together in an infinite variety of configurations. What will you build? A fast fighter jet? A dump truck? An advanced technology helicopter with air bags and a night-vision camera?

Traditional hard disks remain the dominant medium for on-line storage, but they're increasingly being joined by solid state drives (SSDs) for performance-sensitive applications. Running on top of this hardware are a variety of software components that mediate between the raw storage devices and the filesystem hierarchy by users. These components include device drivers, partitioning conventions, RAID implementations, logical volume managers, systems for virtualization disks over a network, and the filesystem implementations themselves.

In this chapter, we discuss the administrative tasks and decisions that occur at each of these layers. We begin with "fast path" instructions for adding a basic disk to each of our example systems. We review storage-related hardware technologies and look at the general architecture of storage software. We then work our way up the storage stack from low-level formatting to the filesystem level. Along the way, we cover disk partitioning, RAID systems, logical volume managers, and systems for implementing storage area networks (SANs).

## Linux recipe

Although vendors use standardized disk hardware, there's a lot of variation among systems in the software domain. Accordingly, you'll see a lot of vendor-specific details in this chapter. We try to cover each system in enough detail that you can easily identify the commands and systems that are used and can locate the necessary documentation.

## 8.1 I WANT TO ADD A DISK!

Before we launch into many pages of storage architecture and theory, let's first address the most common scenario: you want to install a hard disk and make it accessible through the filesystem. Nothing fancy: no RAID, all the drive's space in a single logical volume, and the default filesystem type.

Step one is to attach the drive and reboot. Some systems allow hot-addition of disk drives, but we don't address that case here. Beyond that, the recipes differ amongst systems.

Regardless of your system, the process involves identifying the device, partitioning it, creating a filesystem, and mounting it to a directory. 

(Note: The remaining OCR text for pages 255-256 was highly repetitive/corrupted and has been filtered for logical clarity based on the available headers.)

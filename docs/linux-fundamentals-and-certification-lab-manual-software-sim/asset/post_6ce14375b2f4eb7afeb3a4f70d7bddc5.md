
5. A digital signature is obtained through the use of \_.\_.\_.\_.\_.\_.
- a. DES encryption
- b. a digital certificate
- c. graphic tools
- d. scanning a written signature

6. Digital signatures are \_.\_.\_.\_.\_.\_.
- a. an implementation of public-key encryption
- b. provided using digital certificates
- c. implemented through gpg-pubkey on many Linux distributions
- d. All of the above

7. One form of security that is available when the computer system powers up is provided through \_.\_.\_.\_.\_.\_.\_.\_ passwords.
- a. BIOS
- b. boot loader
- c. GRUB
- d. user

8. Boot loader security \_.\_.\_.\_.\_.\_.
- a. prevents users from changing Linux operating system startup configuration
- b. prevents access to single-user mode
- c. can use MD5 passwords
- d. All of the above

9. An MD5 password \_.\_.\_.\_.\_.\_.
- a. uses plain text
- b. is an implementation of symmetric encryption
- c. is a one-way hash function
- d. is available only as a BIOS password

10. A password protection method that provides a password file that is read-only to the root user is \_.\_.\_.\_.\_.\_.
- a. MD5
- b. shadow passwords
- c. strong passwords
- d. SSH

11. Linux operating system passwords are \_.\_.\_.\_.\_.\_.\_.
- a. case sensitive
- b. not available to use MD5 hashing
- c. required to be 8 characters long
- d. changed by the root user only

12. The \_.\_.\_.\_.\_ command allows a user to log in as another user.
- a. setuid
- b. su
- c. sudo
- d. root

13. In order to access the sudo command the user must \_.\_.\_.\_.\_.\_.
- a. be able to su to the root account
- b. be a member of the admin group
- c. be listed in the /etc/sudoers file
- d. All of the above

14. A personal firewall can be a program running on a workstation computer that \_.\_.\_.\_.\_.\_.
- a. examines network packets as they arrive
- b. allows or denies packets based on a set of rules
- c. can be customized to allow network traffic from specific networks or hosts
- d. All of the above

15. The most secure services on a server are \_\_\_.
- a. those services that are not running
- b. SSH
- c. Telnet
- d. FTP

16. To stop the cups service from the command line, which of the following commands are used?
- a. cups stop
- b. service cups stop
- c. stop cups
- d. stop service cups

17. TCP wrappers provide which of the following actions?
- a. They log access attempts.
- b. They determine if the IP address is allowed or denied.
- c. They display a password prompt.
- d. All of the above

18. Which of the following commands can be used to list open or listening ports on a Linux system?
- a. netstat
- b. nmap
- c. lsof
- d. All of the above

19. CIPE is a package used to implement \_\_\_.
- a. a VPN
- b. a firewall
- c. a public key infrastructure
- d. a personal firewall

20. A method of hiding internal IP addresses behind a firewall is called \_\_\_.
- a. VPN
- b. IPSEC
- c. PPTP
- d. NAT

21. The tool to insert and delete rules from the kernel’s packet filtering table is \_\_\_.
- a. NMAP
- b. NAT
- c. IPTABLES
- d. VPN

22. The command `chmod 755 myfile` provides which of the following results?
- a. It gives the owner read, write, and execute access to the file myfile.
- b. It gives the group read and write access to the file myfile.
- c. It gives other users read and write access to the file myfile.
- d. All of the above

23. The default value of a file’s permissions can be set using the \_\_\_ command.
- a. chmod
- b. chown
- c. umask
- d. mkfile

24. An example of physical access security is \_\_\_.
- a. a firewall
- b. a VPN
- c. locking the door
- d. passwords

25. True or False: The default value of umask is 002, which provides the owner and group full access to the file.

## CHAPTER 13: TROUBLESHOOTING

### CHAPTER OBJECTIVES

- Identify and locate hardware, operating system, application software, configuration, or user problems
- Describe troubleshooting best practices
- Examine and edit configuration files based on symptoms of a problem
- Examine, start, and stop processes based on the signs and symptoms of a problem
- Use system boot disk to diagnose and rescue file system
- Inspect and determine causes of errors from system log files
- Use disk utilities to solve file system problems
- Resolve problems based on user feedback
- Recognize common errors
- Take appropriate action on boot errors
- Identify backup and restore errors
- Identify an application failure on a server
- Identify and use troubleshooting commands
- Locate troubleshooting resources and update as allowable
- Use network utilities to identify network and connectivity problems
- Remove and replace hardware and accessories based on symptoms of a problem by identifying basic procedures for adding and removing field-replaceable components
- Remove and replace hardware and accessories based on symptoms of a problem by identifying common symptoms and problems associated with each component and know how to troubleshoot and isolate the problems
- Identify proper procedures for diagnosing and troubleshooting ATA devices
- Identify proper procedures for diagnosing and troubleshooting SCSI devices
- Identify proper procedures for diagnosing and troubleshooting peripheral devices
- Identify proper procedures for diagnosing and troubleshooting core system hardware
- Identify and maintain mobile system hardware

### TROUBLESHOOTING METHODOLOGY

A methodology is a set of working methods or techniques. Troubleshooting methodologies are the techniques you use to troubleshoot a problem. Troubleshooting is a skill that can be learned and, as with any skill, it takes practice.

One of the first techniques a good troubleshooter uses is to collect all available information about the problem. There is no better information than firsthand information. For example, a user calls you and says that their Linux system won't start. After asking the obvious questions, such as “Is the computer plugged in?”, you go to look at the system yourself. After initially checking the computer, you find that it does start but the user's login fails. You have found that the problem is something other than “The computer won't start.”

At times you will have to rely on the testimony of others as to what is happening, so develop your interview techniques. Be precise in your questions. Keep in mind that the person you are talking to probably has no experience with troubleshooting a computer problem—or worse, they are a self-proclaimed expert.

After collecting as much information as possible, analyze the symptoms. You already have a lot of information about the “won’t start” problem. For instance, you know that the machine is getting power and starts up to the login screen. If you think about how a computer starts—power-on self-test (POST), loading the basic input/output system (BIOS), loading the boot loader, loading the operating system kernel, and the many processes that run to present a login prompt—you can already analyze much of the information to determine the area of the problem.

The second technique used by a good troubleshooter is to localize the problem. In the “won’t start” problem, this would consist in asking what would prevent someone from logging in to the system after the login prompt is displayed. A problem similar to this occurred recently, and it was found that an ID could not be typed in. However, the GUI screen login prompt displayed the mouse pointer and showed the mouse movement. So the problem was localized to a keyboard error, hardware or software. The keyboard hardware may have failed or the software controlling it may have failed.

The third technique used by a good troubleshooter is to isolate the trouble to specific hardware or software. In the case of the “won’t start” problem, you may restart the machine and check that the keyboard works with the BIOS. If it does, you eliminate a keyboard hardware failure as the cause. If the keyboard does not work with the BIOS, a hardware failure is probably the culprit.

After the problem is isolated, the fourth technique is to attempt to correct the specific problem. In this case, the first and most obvious solution is to replace the keyboard.

The fifth technique is to verify that the problem has been solved. Restart the computer system and check that the ID can be entered from the keyboard. If it works, great! You have solved your first computer problem and are on your way to being a good administrator.

Not all problems are this simple. Operating system problems can be very complex. A lot of software is interacting with the hardware of a Linux system, and the more components to a system, the more difficult it is to track down a problem. The following are a few general tips to troubleshooting.

- Be mentally prepared. Troubleshooting requires concentration and perseverance. If you are having a rare off day, a 15-minute troubleshooting problem can turn into a marathon event.
- Slow down. There may be an urgent need to solve the problem, but hurrying to a solution may introduce another problem instead of solving the initial one. As a Linux administrator it is your job to be confident and in control. Don’t panic. Deal with the problem calmly and methodically.
- Be patient. Impatience is usually solved by following the previous tip; slow down. Being impatient can lead to jumping to conclusions before they are thought out sufficiently. A patient individual will take time to make sure the problem is understood before making any decisions. By the way, yelling at a computer system doesn’t accomplish much; but if it makes you feel better, go ahead and yell.
- Take a break. If you have a very trying problem, take a break. You already know that sometimes if you leave a problem alone the solution will suddenly become obvious. Even if you aren’t actively working on a problem, your subconscious mind will continue to work on it in your behalf. The key is to rest so you can recognize the solution when it is presented.
- Ask for help. Even someone with less experience than you can offer a good idea. Sometimes a fresh perspective may be all you need to solve a problem.

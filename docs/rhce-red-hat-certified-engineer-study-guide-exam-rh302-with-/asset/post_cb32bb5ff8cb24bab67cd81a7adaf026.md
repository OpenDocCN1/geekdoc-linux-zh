
# Appendix A

Appendix A is a practice exam for you to take as you prepare for the RHCE exam.

Merely reading—or worse yet, skimming—this book won't suffice to prepare you for the RHCE exam. Instead, you should follow a methodical, organized process such as the following:

- 1. Take the assessment test to determine the areas in which you should spend more time studying. Strive to learn from your mistakes as well as your successes.
- 2. Study a chapter. Studying, by the way, involves more than mere reading; it involves interacting with the text, asking questions, and probing to discover the consequences of what you read.
- 3. Complete the exercises in the chapter. Bear in mind that the RHCE exam will require you to demonstrate skills, which are acquired by practice, not by precept. The exercises are the closest experience to a real RHCE exam you'll find anywhere. They're worth doing, if you plan to pass the exam.
- 4. Answer the review questions at the end of the chapter. These questions closely resemble the experience of the written portion of the RHCE exam.
- 5. Review chapter topics related to any questions you missed. Be sure you know the right answer and why the other responses are wrong.
- 6. Work your way through the entire book in this fashion, one chapter at a time.
- 7. When you believe you're ready, take the practice exam in Appendix A, then assess your performance.
- 8. Take the bonus exam included on the CD to test your readiness for the real thing. If you do well, sign up for the RHCE exam or the RHCE preparation course, according to your preference. If you don't do well, repeat steps 1–8 until you're able to pass the practice exam with confidence.
- 9. Use the Flashcard questions on the CD that accompanies this book to stay sharp while awaiting the RHCE exam.

# Assessment Test

- 1. Which /etc/conf.modules line specifies that default module path information is to be retained?
- A. default-path
- B. hold
- C. keep
- D. retain

- 2. Which of the following are components of the Linux operating system?
- A. The kernel originally created by Linus Torvalds
- B. The GNU utilities and programs
- C. The MINIX utilities and programs
- D. The Unix utilities and programs

- 3. Which of the following protocols is a popular exterior protocol?
- A. BGP-4
- B. EGP
- C. OSPF-2
- D. RIP-2

- 4. To check permission of the local host to access the X server running on server, which of the following commands should be issued?
- A. export DISPLAY=server:0.0
```
xhost
```
- B. export DISPLAY=server:0.0
```
xhost +
```
- C. export DISPLAY=server:0.0
```
xhosts
```
- D. export DISPLAY=server:0.0
```
xhosts +
```

- 5. Which of the following programs is used to configure the system time zone?
- A. timeconfig
- B. timezone
- C. timezoneconfig
- D. zoneconfig

- 6. Which of the following runlevels corresponds to multiuser operation without networking?
- A. 1
- B. 2
- C. 3
- D. 4

- 7. Which of the following programs is used to convert to MD5 password encryption?
- A. md5conv
- B. md5unconv
- C. pwconv
- D. None of the above

- 8. Which of the following commands correctly creates an initial ramdisk for use during system boot?
- A. mkinitrd /boot/inititrd-version
- B. mkinitrd /boot/inititrd-version version
- C. mkinitrd /boot/inititrd-version.img
- D. mkinitrd /boot/inititrd-version.img version

- 9. Quotas are supported on which of the following file system types?
- A. dos
- B. ext2
- C. iso9660
- D. vfat

- 10. Which of the following files specifies a user's window manager?
- A. ~/.wm_style
- B. ~/.wmanager
- C. ~/.Xclients
- D. ~/.Xsession

- 11. Which of the following are Red Hat Linux installation types?
- A. Expert
- B. Graphical
- C. Text
- D. Upgrade

- 12. Which of the following commands activates user quotas?
- A. quotaon -a
- B. quotaon -ag
- C. quotaon -au
- D. quotaon -aug

- 13. Which of the following operations should be performed?
- A. Create the quota files.
- B. Set default quotas.
- C. Set individual quotas.
- D. Turn on quotas.

- 14. What is the port number associated with the SMTP protocol?
- **A.** 22
- **B.** 25
- **C.** 50
- **D.** 110

- 15. To determine whether a Linux kernel supports firewall, you should check for the existence of which of the following files?
- **A.** /proc/net/ip_always_defrag
- **B.** /proc/net/fwchains
- **C.** /proc/net/ipv4_always_defrag
- **D.** /proc/net/ipv4_fwchains

- 16. To masquerade packets originating from a local network, which of the following commands should be specified?
- **A.** iptchains -A forward -i eth0 -s 192.168.1.0/24 -j
- **B.** iptchains -A input -i eth0 -s 192.168.1.0/24 -j
- **C.** iptchains -A local -i eth0 -s 192.168.1.0/24 -j
- **D.** iptchains -A output -i eth0 -s 1.0/24 -j

- 17. Which of the following is associated with a network address of 24 bits?
- **A.** The network address 192.168.1.0/8
- **B.** The network address 192.168.1.0/24
- **C.** An IP address with netmask of 255.0.0
- **D.** An IP address with netmask of 255.255.255

- 18. Which of the following directories contains ping command?
- A. /bin
- B. /sbin
- C. /usr/bin
- D. /sbin

- 19. Where might modules with Linux version 2.2.15 reside?
- A. /lib/2.2.15
- B. /lib/modules/2.2-2
- C. /modules/2.2.15
- D. /modules/2.2-2

- 20. Which of the following is the final operation performed by rc.sysinit?
- A. Activate swap partitions.
- B. Load the keymap.
- C. Set the logging level.
- D. Store the boot messages.

- 21. Which of the following logging configuration entries will log messages pertaining to FTP that have a critical priority?
- A. auth.alert: /var/log/messages
- B. auth.err: /var/log/messages
- C. auth.info: /var/log/messages
- D. auth.*: /var/log/messages

- 22. Which of the following key sequences switches the keyboard and video system from a virtual console to X?
- A. Ctrl+Alt+F1
- B. Ctrl+Alt+F3
- C. Ctrl+Alt+F7
- D. Ctrl+Alt+F8

- 23. To specify that the gpm service should be executed at runlevel 3, which command should be issued?
- A. hkconfig --level 3 gpm
- B. hkconfig --level 3 gpm on
- C. hkconfig --levels 3 gpm
- D. hkconfig --levels 3 gpm on

- 24. To remount the root file system in read-write mode, which of the following commands should be issued?
- A. mount -t ext2 /dev/hda1 -o defaults,ro
- B. mount -t ext2 /dev/hda1 -o defaults,rw
- C. mount -t ext2 /dev/hda1 -o defaults,remount,ro
- D. mount -t ext2 /dev/hda1 -o defaults,remount,rw

- 25. Which of the following commands will halt the system?
- A. init 0
- B. halt
- C. shutdown -h 3
- D. telinit 0

- 26. Which of the following allow you to run Windows 9x under Linux?
- A. You can configure the system for multi-boot operation.
- B. You can install LILO.
- C. You can install VMware.
- D. You can install WINE.

- 27. Which of the following time specifications defines a cron job that executes at 8:00 P.M. on the first day of odd-numbered months?
- A. 00 20 1 1-9/2,11 *
- B. 00 20 1 1-11/2 *
- C. 00 20 1 1,3,5,7,9,11 *
- D. 00 20 1 jan,mar,may,jul,sep,nov *

- 28. When you modify the file /etc/crontab, which of the following occurs?
- A. cron immediately recognizes the change
- B. You must reboot the system
- C. You must issue the touch command to update the modification time of the /var/spool/cron directory
- D. You must restart the cron system

- 29. Which of the following kinds of users log in and receive a shell prompt?
- A. Ordinary users
- B. POP users
- C. PPP users
- D. SLIP users

- 30. Which of the following files establishes the user's path?
- A. /etc/bashrc
- B. /etc/profile
- C. ~/.bashrc
- D. ~/.bash_profile


## 9. You need to take your Linux system offline for maintenance and want to check to see who else may be using it, so you can be courteous and let your users know about it. What command, or commands, will show who else is logged into your system?

- A. w
- B. finger
- C. who
- D. Isof

## 10. Your network seems to be running slower than normal, and many users are complaining of odd things happening on their computers. You suspect your company may be the victim of the latest computer virus. What tool could you use to check?

- A. ssh
- B. Nessus
- C. Snort
- D. Tripwire

## 11. You need to create a new group to support a new product roll-out. What command, or commands, will let you make a new account?

- A. addgroup project_x
- B. groupadd -g project_x
- C. newgroup project_x
- D. groupadd project_x

## 12. You want to tighten security on a particular Linux computer by limiting which users have access to the sudo command. Which file should you edit to lock down this feature?

- A. /etc/users
- B. /etc/shadow
- C. /etc/sudoers
- D. /etc/passwd

## 13. You need to set a shared file for read and write access for the file owner and members of the files group and no access for anyone else. Which command(s) will give the desired result?

- A. chmod 440 shared_file
- B. chmod 660 shared_file
- C. chmod ug=rw,o=
- D. chmod og=r,o=

## 14. You are testing out SELinux to enhance security on your Linux computer. What mode would you use to let all programs run, but log anything that would fail if you were to lock it down?

- A. enabled
- B. allowed
- C. permissive
- D. test

## 15. You are running out of room on your backup system and want to flag a large temporary file so the tape backup system skips it. What is a way you could do that?

- A. chmod -s temp_file
- B. setattr -d temp_file
- C. chattr -d temp_file
- D. attr -d temp_file

# SELF TEST QUICK ANSWER KEY

- 1. B
- 2. B
- 3. D
- 4. B
- 5. C
- 6. D
- 7. B and D
- 8. D
- 9. A, B, and C
- 10. C
- 11. A and D
- 12. C
- 13. B and C
- 14. C
- 15. C

# ENDNOTES

1. Schneider B. Secrets and lies. New York: Wiley and Sons; 2000. p. 84.
2. Northcutt S, Zeltser L, Winters S, Kent K, Ritchie RW. Inside network perimeter security. 2nd ed. Indianapolis, IN: Sams; 2005. p. 11.
3. Nemeth E, Snyder G, Hein T. The Linux administration handbook. 2nd ed. Upper Saddle River, NJ: Pearson; 2007. p. 85.
4. McCarty B. SELinux NSA’s open source security enhanced Linux. Sebastopol, CA: O’Reilly Media; 2005. p. 20.
5. Rogers R. Nessus network auditing. 2nd ed. Boston: Syngress; 2008.
6. Sotirov A, Stevens M, Appelbaum J, Lenstra A, Molnar D, et al. MD5 considered harmful today. <http://www.win.tue.nl/hashclash/rogue-ca/>; 2008 [accessed 06.25.09].
7. Burr W. NIST comments on cryptanalysis attacks on SHA-1. <http://www.csrc.nist.gov/groups/ST/hash/statement.html>; 2009 [accessed 06.25.09].
8. Liu D. Next generation SSH2 implementation: Securing data in motion. Boston: Syngress; 2009.
9. Morgan A, Kukuk T. Linux-PAM system administrators’ guide. <http://www.kernel.org/pub/linux/libs/pam/Linux-PAM-html/Linux-PAM_SAG.html>; 2009 [accessed 06.27.09].
10. OpenLDAP foundation. OpenLDAP administrators guide. <http://www.openldap.org/doc/admin24>; 2008 [accessed 06.28.09].
11. OpenLDAP foundation. OpenLDAP administrators guide. <http://www.openldap.org/doc/admin24>; 2008 [accessed 06.28.09].
12. Kukuk T. The Linux NIS/[Y]/[P]/[N]/[S]/[N]IS + howto. <http://www.linux-nis.org/nis-howto/HOWTO/index.html>; 2003 [accessed 06.24.09].
13. Rigney C, Willens S, Livingston, Rubens A, Merit, et al. RFC2865. <http://tools.ietf.org/html/rfc2865>; 2000 [accessed 06.28.09].

# Troubleshooting and Maintaining Linux

Exam objectives in this chapter:

- Monitoring Tools
- Analyzing Logs
- Backing Up and Restoring

## UNIQUE TERMS AND DEFINITIONS

- **Compact Disc (CD)** – A 4.72-in. disc developed by Sony and Philips that can store, on the same disc, still and/or moving images in monochrome and/or color; stereo; or two separate sound tracks integrated with and/or separate from the images; and digital program and information files.¹
- **Digital Versatile Disc**, formerly Digital Video Disc (DVD) – An optical storage medium with improved capacity and bandwidth compared with a CD. DVD, like CD, was initially marketed for entertainment and later for computer users. A DVD can store 4.7 GB (the equivalent of a full-length film with up to 133 min of high quality video) in MPEG-2 format and audio. Additionally, the DVD-ROM drive can read DVD movies, and modern computers with the appropriate hardware or software can decode them in real-time.²
- **File Transfer Protocol (FTP)** – A client-server protocol, which allows a user on one computer to transfer files to and from another computer over a Transmission Control Protocol/Internet Protocol (TCP/IP) network. Also, it is the client program used by the user to execute the transfer of files. It is defined in STD 9, RFC 959.³ There are two modes for FTP: active and passive.

# INTRODUCTION

Ongoing system maintenance is an important part of a system administrator’s job. Unfortunately, compared with the fire drills of critical outages or the interesting new challenges of configuring the latest tools, regular maintenance is pretty dull, and is often the first thing that gets skipped when things start to get busy. Stephen Covey would categorize it as “important, but not urgent.” It is the sort of thing that, if done well, makes the fire drills much less dramatic, and frees up time that can be spent on other fun projects.⁴

In this chapter, we’ll cover common Linux tools for managing a running system, including monitoring performance and logs, and backing up data.

Keep in mind that a little preparation goes a long way. If your system seems to be running slowly or having some other issues, it’s very helpful to have some historical data to compare with – so it is advisable to run a few of them now and then under normal load, and maybe save some screenshots so you have a good idea what “normal” looks like. Then you can look for something different if a problem comes up.

# MONITORING TOOLS

Linux provides a number of handy tools for reviewing system status and other statistics. Not all of them may be included in a default installation, or be configured to collect data, but they are all supported and can be made to work with a little effort.

## Commands

It does not take a fancy, expensive system-monitoring package to pull and compile statistics on how your system is performing. Just about everything you need to measure CPU, memory and disk utilization, I/O performance, and network and disk throughput, among others, are at your fingertips in utilities that, for the most part, are installed in almost every base Linux system. The usage of the most popular utilities is described in the paragraphs that follow.

### sar

The `sar` command (think "system activity report") is a part of the `sysstat` package, if it isn't already on your system. It can be used to gather both current and historic system statistics for the system processor. By default, with no options `sar` displays information collected by a `cron` job that is periodically gathered and stored in files at `/var/log/sysstat/sa*`, with the last two numbers of the `sa*` files corresponding to the calendar day the information was collected. Some other useful options include `sar -A` to show *all* statistics, and `sar -n DEV` to show network statistics. You can control the collection of current information by appending two numbers at the end of the command; the first will set the collection interval in seconds, the second tells how many times it should gather the information. For example, `sar -n DEV 5 4` will show network statistics for 5-s time periods a total of four times, then provide a nice average for each interface, as shown in Figure 11.1.

The `sar` command has a very thorough `man` page for further information.

![](img/95b3ebd6248b36778ccf73988aaab2f2_351_0.png)

# FIGURE 11.1

An example of using `sar` to view network statistics.

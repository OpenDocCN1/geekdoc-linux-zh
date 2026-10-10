Although monitoring will help you check up on how things are going with your system, you will need to know where to go to find information when the inevitable happens and things go badly. Just as there are numerous monitoring programs, there are even more logs. It seems that just about anything that happens in Linux is logged, and these logs, many of which reside under the /var/log directory structure, should be the first things you turn to when starting to troubleshoot. Knowing the various logs under /var/log is important for both the exam and back at your job, especially .messages, /syslog, /maillog, .secure, and /lastlog. With the amount of data that is captured in each log, you definitely do not want to have to go line-by-line through a log file to find the information you need. For this, you need good searching and sifting tools; grep, sed, awk, and tail are your closest allies.

Mechanical things break and people make mistakes. Restoring data that has been lost due to a hard disk crash or user error is inevitable. In my view, there are two types of network administrator: (1) those who have had to restore lost data from a backup and (2) those who are looking for work because their backups failed and were never tested. The good thing is that Linux offers the network administrator a myriad of methods and tools for backing up and restoring files to a variety of media. This chapter covers the basics for protecting files by ensuring that duplicate copies exist through FTP and rsync, and for creating backup sets with tar and dump. For restoring files, there is tar and restore. The dd command gives you the ability to create disk images and apply them to other media.

# SELF TEST

+   1.  Which of the following commands does not display load average?
+       A.  top
+       B.  w
+       C.  who
+       D.  uptime

+   2.  What command would you use to generate a static report of CPU utilization?
+       A.  uptime
+       B.  vmstat
+       C.  top
+       D.  iostat
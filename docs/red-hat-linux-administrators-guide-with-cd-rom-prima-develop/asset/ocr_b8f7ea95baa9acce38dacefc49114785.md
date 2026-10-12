One of the most essential aspects to correct system administration is properly diagnosing any ills or problems with the system. Linux provides logging of most all system processes for later evaluation. These log files are kept in several reserved locations to separate them from other system and user files. During the initial partitioning of the drive or drives, it is customary to set aside a /var partition to store all log files. Because they have a shorter life span than most other partitions, this partition sees more activity than other files. Learning to interpret these files will assist in fixing errors and problems under Linux.

This chapter will examine the following subjects:

+   - Tracking normal system logging procedures
+   - Understanding the different levels of logging
+   - Discarding and rotating log files
+   - Saving log files for later examination
+   - Using syslog to improve logging capabilities

# ## Monitoring System Use

When you are managing a larger Linux system, or even a relatively small one, there are times when certain processes require monitoring. This monitoring is needed for fixing errors, tracking user needs, managing security settings, determining system use, or simply finding out how the system is processing certain programs. All of these processes can be monitored or logged or configured in such a way that the system can save all messages to the hard drive.

Nearly all daemons generate some sort of message for the administrator to examine later. These daemons can include anything from the Web daemon or http (which in the case of Red Hat is by default the Apache Web server) to the sendmail daemon, which tracks every e-mail either received or sent through the machine to even the named daemon which provides dynamic name service and translates IP addresses to human-readable domains. Each of these daemons and
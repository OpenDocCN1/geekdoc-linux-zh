# Appendix B • ANSWERS TO QUESTIONS

2. Port monitoring verifies only that a service's port is accepting connections; it doesn't actually test the functionality of the service.

3. To send syslogs with a level of kern and a level of info, you would add the following to syslog.conf and restart syslog:

kern.info /var/log/kern

4. Sending both a page and an email to a system administrator ensures that he or she will receive the message even if one of those lines of communication is unavailable (such as if the pager is out of range). Redundancy in emergency reporting techniques is essential for the reason that it is necessary in system components and functions.

5. External monitoring traverses the Internet to access your services, which may be representative of how your users connect to your services. External monitoring also prevents internal network outages between your monitor and your network services from causing false outage reports. For example, external monitoring would view your service as unavailable if your connectivity to the Internet were down; internal monitoring would still view your services as available, since it uses internal networks to access your services.

6. Log rotation prevents log files from consuming all available disk space over time, and it allows for smaller, easier-to-analyze log files.

# Chapter 7

+   1. A sandbox would mimic your production environment so that any tests you run in the sandbox will produce results comparable to those you should achieve on your production platforms.

+   2. You should patch in single-user mode because there are fewer processes running that may interfere with or be affected by the patching process. If you are unable to bring the system down into single-user mode, you should choose a nonpeak time to apply the patches and kill all nonessential processes before you start.

+   3. A shared library is a file containing code that is shared among different programs and. You must pay particular attention to shared libraries when upgrading an operating system, even a small change or incompatibility in an upgraded shared library can affect many programs that are critical to your system's functionality.

+   4. To replace a disk on a server that does not support hot-swappable disks, you would have to shut down the server, remove the old disk, insert the new disk, power on the server, and (if the new disk is a different model than the old one) reconfigure your system to recognize the new disk. On a system that supports hot-swappable disks, you would simply remove the old disk and insert the new disk, letting the hardware and the operating system worry about the details of the disk-swapping process. (These are just generic procedures, however—always read your vendor's documentation before swapping.)
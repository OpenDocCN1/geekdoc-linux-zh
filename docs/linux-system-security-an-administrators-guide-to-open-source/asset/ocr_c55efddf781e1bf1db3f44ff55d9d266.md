# CHAPTER 7

# Bean Counting

# System Accounting

Although originally not designed for security purposes, Linux system accounting can provide valuable information about various activities taking place on your system. After a brief overview, this chapter discusses the appropriate security elements of system accounting and some situations for using it.

# GENERAL SYSTEM ACCOUNTING

Originally system accounting was developed for the purpose of keeping track of user resource consumption so that charges could be made against that user's account. In the days of mainframes and minicomputers, this was, in part, the way that Management Information Systems (MIS) departments got their funding. With the advent of personal workstations, the use of system accounting for that purpose has declined.

The Linux implementation of system accounting does not include many of the postprocessing scripts and configuration files (such as chargefee and the /var/adm/fee found on Solaris, IRIX, and other commercial UNIX systems) for fiscal accounting purposes, but it does include much (if not all) of the data required for such computations. Instead, Linux focuses on providing connection and process accounting information, each of which is described in detail in this chapter.
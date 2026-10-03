# CHAPTER SUMMARY

# KEY TERMS

+   - process
- ps command
- pgrep command
- Syslog
- crontab file
- priocntl command
- nice command
- prstat command
- ps command
- CDE Process Manager

This chapter described Solaris processes and the various Solaris utilities available to monitor them. Using commands such as ps, prstat, and sdtprocess, you can view all the attributes associated with a process.

The concept of sending signals to a process was described. A signal is a message sent to a process to interrupt it and cause a response. You also learned how to send signals to processes to cause a response such as terminating a process.

Setting process priorities was described. The various commands, such as nice and priocntl, which are used to set and change process priorities, were described. In addition, I described how to use the crontab and at facilities. Use these facilities to submit batch jobs and schedule processes to run when the system is less busy to reduce the demand on resources such as the CPU and disks.

Finally, I described the syslog messaging facility. syslogd is the daemon responsible for capturing system messages such as warnings, alerts, or informational messages. You’ll monitor these messages proactively to resolve problems that may be occurring on your system.

The system administrator needs to be aware of the processes that belong to each application. As users report problems, the system administrator can quickly locate the processes being used, and look for irregularities. By keeping a close watch on system messages and processes, you’ll become familiar with what is normal and what is abnormal. Don’t wait for problems to happen—watch system messages and processes daily. Create shell scripts to watch processes for you and to look for irregularities in the system log files. By taking a proactive approach to system administration, you’ll find problems before they affect the users.

In Chapter 10, “The LP Print Service,” we’ll explore another topic that you’ll need to become very acquainted with—the LP Print Service, the facility responsible for all printing within the Solaris environment.
Hardware failure indications should report specific information about the failed component, such as the serial number or hardware path. This can help network support personnel locate the failed component in the server. A lower severity may be used when redundant components fail, to indicate that the problem is important but not necessarily urgent to fix. Hardware monitoring is discussed in Chapters 4 and 5.

Hardware failures used to cause the system to fail, but servers are more resilient today. Servers can now continue to run, often in a crippled state, after a hardware failure. For example, a server can detect bad memory pages and deallocate them, but this leaves less memory available for the applications. The fact that a component failure may not be obvious again points out the importance of continual monitoring of the system. Repairs can then be made during a planned downtime period.

You also need to monitor the status of the server software. The software can be divided into the following categories:

+   - Operating system or firmware
- System vendor applications or middleware
- Database and enterprise resource planning applications
- User applications

If the operating system fails, you will see a failure (panic) message on the server console. The server status will be shown as “DOWN” to an enterprise management product, such as HP OpenView. You need to reboot the system and look at system log files or core files to diagnose the problem.

The failure of a key software application may also be a critical event to a system operator. Typically, only one key application is configured per UNIX server, so the failure of the application is essentially equivalent to a failure of the server. If you know the processes making up the application, you can periodically check the status of the processes by using UNIX commands. Some monitoring tools can automatically notify you of the failure of an important process.

Some vendors provide high availability software to help protect your server. This software also needs to be monitored to ensure that it is working properly. Other important applications include database applications and enterprise resource planning applications. Later chapters describe some of the sophisticated monitoring products that are available for these applications. Management applications, such as a backup software application, also need to be monitored. Errors encountered during a backup should be reported, because such errors indicate that critical data is not being adequately protected.

The easiest application failure to detect is the failure of an application process. An application can also get into a process loop or deadlock situation. Although the effect is the same to the end-user, the application is unusable; this is a much more difficult situation to detect. You are unlikely to see these situations reported as external events, although you may receive some external indications, such as timeout errors, when trying to use a service. In general, to detect these types of problems, you need to measure the performance and resource usage, and compare it to baselines.
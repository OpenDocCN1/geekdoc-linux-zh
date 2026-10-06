# Chapter 7 ♦ Logging 177

syslog-ng, you could specify if that the message was intercepted by syslog-ng contained your logging prefix, you could write that message to a specific file.

Another really useful feature of syslog-ng, especially if you are setting up a central-logging host, that you can save the messages to a specific file in a specific directory where the messages originated. All of these adds up to a more granular experience for organizing your log files with syslog-ng.

To configure syslog-ng, we will take a slight deviation because the /etc/syslog-ng.conf file that is read by syslog-ng on startup is, in fact, maintained by UseConfig by default. To edit it but also maintain control of the syslog-ng file by UseConfig. You need to edit the template for syslog-ng, which is because only a few macros are used by UseConfig to control the workings of syslog-ng (relating to the source of the messages controlled by syslog-ng).

To edit the configuration of syslog-ng, you need to edit the /etc/syslog-ng/syslog-ng.conf.

YaST is a very capable manager when it comes to services; it is alive to control them in a user-friendly fashion. If you feel uncomfortable YaST automatically starts using UseConfig to dynamically update your system based on the contents of the files in /etc/sysconfig to ensure that the system can maintain your configuration changes. If you do not want YaST to maintain a particular service, find the file that controls the general use of the service you are interested in, for example, syslog-ng, open the file /etc/sysconfig and find the line SYSLOG_CREATE_CONFIG="yes", and change it to "no". This ensures that YaST will not change your configuration files.

The syslog-ng file contains three important definitions that make up a log profile:

+   **The log source** — The program or system capability that generates the log data

+   **The filter** — Any filters that should be applied to the messages that are being logged

+   **The log destination** — The local file or network destination to which logs should be sent

In the default syslog-ng configuration that is installed, all of the default log profiles used are in the syslog-ng configuration. As example, we will examine the components that make up the iptables logging rules — the log source, the filter, and the log destination —as they describe the three main components of syslog-ng and also show the regular expression features of syslog-ng.
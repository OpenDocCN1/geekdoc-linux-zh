be helpful to know how to create your own RPM. The following RHCE objective is step one in that process, to

- Build a simple rpm that packages a single file

This chapter also addresses several network tasks from the RHCE objectives. The configuration of an iSCSI initiator, as described in the following objective, is the configuration of a client:

+   - Configure system as an iSCSI Initiator persistently mounting existing Target

The following objective relates to the configuration of a system as a Kerberos client:

+   - Configure system to authenticate using Kerberos

Finally, the following objective is related to the nitty-gritty of enterprise networking;

+   - Route IP traffic and create static routes

# CERTIFICATION OBJECTIVE 12.01

# Automate System Maintenance

As discussed in Chapter 9, RHEL 6 includes a number of standard scripts for system maintenance, driven by the /etc/crontab and the /etc/anacrontab configuration files. In that chapter, you can review basic information on when scripts in various /etc/cron.* directories are run. In this chapter, you'll get into the details of some of the standard scripts in the /etc/cron.* directories and then analyze various script commands in detail. With that information in hand, you'll be able to create administrative scripts too.

# Standard Administrative Scripts

Start with the scripts in the /etc/cron.hourly directory. While the intent of the 0anacron script was summarized in Chapter 9, you'll analyze it in detail here. But first, start with a simpler script, mcelog.cron, which logs machine check exception data on an hourly basis. That script has two lines. The first line is standard on most scripts, as it specifies that the commands that follow are governed by the syntax of the bash shell:

```
#!/bin/bash
```
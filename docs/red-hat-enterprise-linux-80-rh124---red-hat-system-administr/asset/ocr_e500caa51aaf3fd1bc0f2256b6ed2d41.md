# CHAPTER 1 | Managing Services and Support

If a current SoS report does not exist, an administrator can generate and attach one later. Use the **redhat-support-tool addattachment** command to attach the report.

Support cases can be viewed, modified, and closed by the subscriber:

+   Command (? for help): **listcases**

Type the number of the case to view or 'e' to return to the previous menu.
1 [Waiting on Red Hat] System fails to run without power
No more cases to display
Select a Case: **1**

+   Type the number of the section to view or 'e' to return to the previous menu.
1 Case Details
2 Modify Case
3 Description
4 Recommendations
5 Get Attachment
6 Add Attachment
7 Add Comment
End of options.
Option: q

Select Case: **q**

```
[user@~]$ redhat-support-tool modifycase --status=Closed 01034421
Successfully updated case 01034421
[user@~]$
```

The Red Hat Support Tool has advanced application diagnostic and analytic capabilities. Using kernel crash dump file **redhat-support-tool** can create and extract a **backtrace**. The kernel crash dump file is created using the **kdump** command. A backtrace is a report of the active stack frames at the point of a crash dump and provides os diagnostics. One of the options of **redhat-support-tool** is to open a support case.

The tool also provides log file analysis. Using the tool's **analyze** command, log files of many types, including operating system, JBoss, Python, Tomcat, and ovirt, are parsed to recognize problem symptoms. The logs can be viewed and diagnosed individually. Preprocessed analysis, as to raw data such as crash dump or log files, allows support cases to be opened and made available to engineers more quickly.

# JOINING RED DEVELOPER

One other useful resource from Red Hat is Red Hat Developer. Available at https://developer.redhat.com, this program provides subscription entitlements to Red Hat software for development purposes, documentation, and premium books from experts on microservices, serverless computing, Kubernetes, and Linux. A blog, and other resources are also available, as well as links to Red Hat Customer Portal.

Registration is free, and can be completed at https://developer.redhat.com/register.
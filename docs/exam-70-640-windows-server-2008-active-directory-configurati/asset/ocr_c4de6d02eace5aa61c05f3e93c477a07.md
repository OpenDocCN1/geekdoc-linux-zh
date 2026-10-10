After Windows Server 2008 is installed, the edition cannot be changed without reinstalling it.

# How To Install Windows Server 2008 Without Activating It

+   1. Run the Windows Server 2008 Setup program.
+   2. When you are prompted to enter a product key for activation, do not enter a key. Click No when Setup asks you to confirm your selection.
+   3. You may be prompted to select the edition of Windows Server 2008 that you want to evaluate. Select the edition that you want to install.
+   4. When you are prompted, read the evaluation terms in the Microsoft Software License Terms, and then accept the terms.
+   5. When the Windows Server 2008 Setup program is finished, your initial 60-day evaluation period starts. To check the time that is left on your current evaluation period, run the Slmgr.vbs script that is in the System32 folder. Use the -dll switch to run this script. The slmgr.vbs -dll command displays the number of days that are left in the current 60-day evaluation period.

# How To Re-Arm the Evaluation Period

This section describes how to extend, or re-arm, the Windows Server 2008 evaluation period. The evaluation period is also known as the "activation grace" period.

When the initial 60-day evaluation period nears its end, you can run the Slmgr.vbs script to reset the evaluation period. To do this, follow these steps:

1. Click **Start**, and then click **Command Prompt**.
2. Type `slmgr.vbs -dll`, and then press **ENTER** to check the current status of your evaluation period.
3. To reset the evaluation period, type `slmgr.vbs -rearm`, and then press **ENTER**.
4. Restart the computer.

This resets the evaluation period to 60 days.

# How To Automate the Extension of the Evaluation Period

You may want to set up a process that automatically resets the evaluation period every 60 days. One way to automate this process is by using the Task Scheduler. You can configure the Task Scheduler to run the Slmgr.vbs script and to restart the server at a particular time. To do this, follow these steps:

1. Click **Start**, point to **Administrative Tools**, and then click **Task Scheduler**.
2. Copy the following sample task to the server, and then save it as an .xml file. For example, you can save the file as `Extend.xml`.

```
<xml version="1.0" encoding="UTF-16"?><Task version="1.2" xmlns="http://schemas.microsoft.com/windows/2004/02/mit/task"><RegistrationInfo><Date>2007-09-17T14:26:04.433</Date><Author>Microsoft Corporation</Author></RegistrationInfo><Triggers><TimeTrigger id="18c4a453-d7aa-4647-916b-af0c3eal6a6b"><Repetition><Interval>PT90d</Interval><StopAtDurationEnd>false</StopAtDurationEnd></Repetition><StartBoundary>2007-10-05T02:23:24</StartBoundary><EndBoundary>2008-09-17T14:23:24.777</EndBoundary></TimeTrigger></Triggers><Principals><Principal id="Author"><UserId>domain\alias</UserId>
```
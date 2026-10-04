# Chapter 10 > Securing IIS

# Figure 10.21 Directory Security

![](bbox=[0.308, 0.095, 0.631, 0.335])

# Figure 10.22 Authentication Methods

![](bbox=[0.308, 0.394, 0.631, 0.584])

At this point you can click OK and close the Master WWW properties screen. However, not all Web properties have been set. Some properties are not available in the Internet Services Manager, so you must set them directly using the adisil.vbs script located in the AdminScripts directory of your IIS installation. Open a command prompt, change to the AdminScripts directory on your system, and enter the commands shown here:

+   - adisil.vbs SET W3SVC/AspAllowOutOfProcComponents 0 (To prevent out-of-process components from running under the SYSTEM process)
- adisil.vbs SET W3SVC/AspErrorsToNTLLog 1
adisil.vbs SET W3SVC/AspLogErrorRequests 1 (To record ASP errors to the Windows EventLog)
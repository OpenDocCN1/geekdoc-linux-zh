your key logger to the session that you want to monitor. So, in this case, simply migrating our Meterpreter shell to the winlogon process puts us in the correct mode to look for passwords. We then need to start keyscan again.

Let's step through this process:

+   6. Type “ps” in Meterpreter to get a process list. Look for the PID of the process “winlogon”.

![](bbox=[0.188, 0.277, 0.452, 0.458])

As you can see in the image above winlogon.exe has the Process ID number 472 (yours will be different). We simply need to migrate our Meterpreter session to that ID.

+   7. Type “migrate <winlogin PID#>” or in my case here “migrate 472”.

![](bbox=[0.188, 0.61, 0.535, 0.668])

+   8. Now go ahead and start keyscan again, “keyscan_start”.

+   9. Then Lock the Windows 11 workstation and log back in.

+   10. And finally, dump the keylog to view the user password using, “keyscan_dump”:

![](bbox=[0.188, 0.79, 0.495, 0.872])
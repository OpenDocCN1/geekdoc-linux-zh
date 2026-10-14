
| Option | Function |
|---|---|
| `-y` | Performs uninstall (only with `-m` or `-q`). |
| `-f` | Forces applications to close at shutdown. |
| `-n` | Does not create uninstall directory. |
| `-z` | Does not reboot when update completes. |
| `-q` | Initiates Quiet mode – no user interface. |
| `-m` | Initiates Unattended mode. |
| `-l` | Lists installed Hot Fixes. |

Be careful when modifying the default functionality of `hotfix.exe` to avoid putting your system in an unstable state.

## Summary

This chapter has attempted to give you a framework for managing patches and upgrades. While upgrading and reinstalling systems can be a tedious and time-consuming process, it is important to understand the motivations behind these tasks, as well as create a solid process to perform them. Each operating system has its own set of tools and commands to install patches, and the information presented here should provide value to experienced as well as inexperienced administrators on a given platform.

## UPGRADING VS. RE-INSTALLING

Upgrading and re-installation are the two methods you can use to move your systems from one operating system version to another. Over the course of one to two years, you should expect to upgrade or re-install each server in your environment. If you have only a few servers, or if a given server has a very complex set of software and configurations, you may opt for upgrading over reinstalling. Upgrades generally retain system information and allow you to back out of the upgrade if problems arise. However, upgrades can require more resources, and may require longer periods of time to complete.

If you have a large number of servers that are similarly configured, or if you are concerned about the amount of time an upgrade may take, then re-installation may be the best option for you. Re-installations are generally faster and cleaner than upgrades. Re-installations also give you the opportunity to reconfigure the hardware, such as disk layouts, whereas upgrades must rely on the current configuration of the system. Use the information in Tables 5.1 and 5.2 to help you determine which course of action is right for you.

## PATCH, HOT FIX, AND SERVICE PACK MANAGEMENT

Over time, users, administrators, and developers discover performance, stability, and security problems with their operating systems. Patches, Hot Fixes and Service Packs are the vehicles that vendors use to relay operating system fixes to users. Literally hundreds of different patches can be made available for any one version of an operating system, so it is important to understand how to choose and manage those patches that you plan to introduce into your environment.

Patches can quickly get out of hand if you have a large installation or a mix of different operating systems. Developing a strategy and schedule for testing and deploying patches is crucial to your overall patch management scheme. Poor patch management not only leads to poor systems performance, but may lead to patch apathy, where the administrator is so frustrated with patches that they are not even deployed. Don't let this happen to you.

Develop a schedule and a procedure, and stick with them. Only deploy those patches that are absolutely necessary to avoid bloating your servers, as well as to avoid possibly introducing more problems than you can solve. Use the GUI and command-line tools available to properly install patches, and whenever possible, have software contracts with your vendors so that you are assured to always have access to the latest available patches.

## NAME RESOLUTION AND REGISTRATION

### UNIX
- The UNIX HOSTS File
- DNS Setup
- BIND 4 DNS Server Configuration
- BIND 8 DNS Server Configuration
- `nslookup`

### WINDOWS
- The Windows HOSTS File
- DNS Setup
- `LMHOSTS`
- WINS
- DHCP

![](img/415c89a1ede71e11e5040a0038b6916c_205_0.png)

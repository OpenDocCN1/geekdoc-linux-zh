selected regular users to the inner sanctums of the root administrative account. Because of the risks, just be sure to disable the ACLs when the lab is complete. If the selected user is michael, one method is with the following command:

```
# setfacl -b u:michael /root
```

If you've configured ACLs on files within the /root directory, be sure to disable those as well. Of course, in standard Linux configurations, the /root directory is mounted on the same volume as the top-level root directory (/). During the lab, you should have mounted that top-level root directory with the acl option. That should be confirmed in the output to the mount command. Given the risks, you should restore the original configuration with the following command:

```
# mount -o remount /
```

# Lab 4

This lab is designed to raise awareness of the time and effort required to disable and re-enable SELinux in enforcing mode. If you switch between disabled and permissive mode, the time and effort required should be about the same. While it may not seem to take that much time, if you have to reconfigure SELinux in enforcing mode, it might seem to take “forever” as nothing else can be done while the system is being rebooted and relabeled.

# Lab 5

Standard users in RHEL 6 run as unconfined_u SELinux user types. As such, there are few limits on their user accounts. If instructions on an exam or from a corporate policy require certain limits on regular users, you may want to set up the ___default___ user with the SELinux user_u user type. Alternatively, if you're told to set up specific users to a limited type, such as xguest_u or staff_u, multiple semanage login commands may be appropriate.

# Lab 6

After testing a user as a guest_u user, most administrators will want regular users to have more privileges.

# Lab 7

Users configured with the guest_u SELinux user type are not normally allowed to execute scripts even in their own home directories. That can change with the allow_guest_exec_content boolean described in the lab. Success in this lab is based on a simple comparison; whether a script can be executed with and without the active boolean.
To put SELinux in enforcing mode, change the line containing the SELINUX assignment to SELINUX=enforcing. Similarly, you can change the policy by setting SELINUXTYPE.

# If you will use SELinux in the future

If you will use SELinux in the future but not now, turn it on when you install Linux, and run it in permissive state with the policy set to the policy you will eventually use. Permissive state writes the required extended information to inodes, but it does not stop you from doing anything on the system.

If you turn on SELinux after it has been disabled, when you reboot the system SELinux has to add extended attributes to the files in the filesystem. This process can take a long time on a large file-system. If you are never going to use SELinux, disable it.

# getenforce, setenforce, AND sesstatus: WORK WITH SELINUX

The `getenforce` and `setenforce` utilities report on and temporarily set the SELinux mode. The `sestatus` utility displays a summary of the state of SELinux:

```
```
# getenforce
Enforcing
# setenforce permissive
# sestatus
SELinux status:              enabled
SELinuxfs mount:            /selinux
Current mode:               permissive
Mode from config file:      enforcing
Policy version:             24
Policy from config file:    targeted
```
```

# SETTING THE TARGETED POLICY WITH system-config-selinux

The `system-config-selinux` utility displays the SELinux Administration window (Figure 11-1), which controls SELinux. To run this utility, enter `system-config-selinux` from a command line in a graphical environment or select Main menu: System→Administration→SELinux Management.

With Status highlighted on the left side of the SELinux Administration window, choose Enforcing (default), Permissive, or Disabled from the drop-down list labeled System Default Enforcing Mode. The mode you choose becomes effective next time you reboot the system. You can use the drop-down list labeled Current Enforcing Mode to change between Enforcing and Permissive modes immediately. When you change the mode using this list, the system resumes the default mode when you reboot it.

To modify the SELinux policy, highlight Boolean on the left side of the SELinux Administration window and scroll through the list of modules. For example, the SpamAssassin (page 682) module has two policies. The first, Allow user spamassassin
groups=0(root),1(bin),2(daem),3(sys),4(adm),6(disk),10(wheel)
[root@server1 root]# touch samplefile2
[root@server1 root]$ ls -1 samplefile2
-rw-r-r- 1 root sys 0 Jul 17 19:28 samplefile2 [root@server1 root]#

# **NOTE**

> If you use group passwords as described earlier in this section, you can use the new-grp command to change your primary group to a group of which you are not a member, provided you supply the appropriate password when prompted.

Although command-line utilities are commonly used to administer users and groups, you can instead use a graphical utility to create, modify, and delete user and group accounts on the system. These utilities run the appropriate command-line utility in the background. To create and manage users and groups in Red Hat Fedora Core 2 from within a desktop environment, you navigate to the Red Hat button, System Settings, Users and Groups, as shown in Figure 11-11. Alternatively, you can use the `system-config-users` command at a terminal within a desktop environment to obtain the screen in Figure 11-11.

![](bbox=[0.17, 0.56, 0.77, 0.87])

**FIGURE 11-11** *Configuring users and groups within a desktop environment*
# Updates and Security Fixes

Red Hat maintains a public list of errata at http://rhn.redhat.com/errata/. Such errata are classified by RHEL releases. If you have an RHEL subscription, affected packages normally made available through the RHN. All you need to do is run the yum update command periodically. This list is useful for those third parties who use RHEL source code, such as CentOS, Scientific Linux, or even Oracle Linux.

# Package Groups and yum

The yum command can do more. It can install and remove packages in groups. These are the groups defined in the xml files described in Chapter 2. One location for that file is on the RHEL 6 DVD, in the /repodata subdirectory. At the start of most of those stanzas, you'll see the <id> and <name> XML directives, which list two identifiers for each of those groups.

But that's a lot of work to find a package group. The yum command makes it simpler. With the following command, you can identify available package groups from configured repositories:

```
# yum grouplist
```

Note how the groups are divided into installed and available groups. Some of the groups listed may be of particular interest, such as "Remote Desktop Clients", some of which you'll use in Chapter 9. To find out more about this group, run the following command, with output shown in Figure 7-10.

```
# yum groupinfo "Remote Desktop Clients"
```

![](bbox=[0.07, 0.88, 0.92, 0.98])
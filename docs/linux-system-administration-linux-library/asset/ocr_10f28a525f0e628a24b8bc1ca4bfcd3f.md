# Deleting a Group with Linuxconf

The Linuxconf utility can also be used to delete a group. Simply select the Group Definitions option as before. When presented with the group list, highlight the one you wish to delete. You will then be presented with the same Group Specification screen as shown in Figure 6.4, with the existing values filled in. Click the Del button, and activate the changes as before.

# Manually Removing a Group

Although you can remove a group simply by editing the /etc/group file to delete the line that corresponds to the group you wish to remove, that's not as efficient as the other methods. If you remove the group's entry in /etc/group, you should probably remove the corresponding entry in the /etc/shadow file (if shadowed group passwords are stored, if you have elected to use group passwords). If you do not use passwords for your groups, this file will not be automatically updated.

# In Sum

As a multiuser OS, Linux relies upon user accounts and groups to maintain security and keep the system usable to all users. Over the years, manual methods, text-based tools, and GUI tools have been developed to manage these accounts and groups. However you do it, though, it's important that you understand how Linux handles its accounts and groups—the relationship between usernames and UIDs or group names and GIDs; where passwords are stored; and how users are assigned to groups. Understanding these topics will allow you to effectively manage your user base, whether it's just one or two people or thousands. These subjects are also critically important for understanding Linux system security, which is the topic of the next chapter.
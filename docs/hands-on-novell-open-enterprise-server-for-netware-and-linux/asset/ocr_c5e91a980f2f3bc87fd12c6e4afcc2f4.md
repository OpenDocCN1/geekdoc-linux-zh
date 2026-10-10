d. Click **LmCMann**, and then click **OK** to display effective rights for Luke. Record the effective rights here:

e. Click **Close** to close the Effective Rights dialog box.

5. Click **Cancel** to close the Properties of KThiele dialog box. Exit ConsoleOne, and log out.

# Group Trustee Assignments

As described in Chapter 5, groups are network objects that help organize users with common network requirements and are useful in simplifying trustee assignments. When a group is made a trustee of a directory or file, all members of that group are also considered trustees of the directory or file, with the same rights assigned to the group. When users are members of a group, their effective rights in a directory are a combination of any personal trustee assignments plus any rights they have from being group members. For example, all IT Department users need to have Read and File Scan rights to the Apps\Utility directory to run certain software. To do this, you can make the ITMgrs group created in Chapter 5 a trustee of the Apps\Utility directory with Read and File Scan rights. Because Eric, Kellie, and Luke are members of the ITMgrs group, they have Read and File Scan rights to the Apps\Utility directory. If you want Kellie's user account to be responsible for changing data, you could also make her a trustee of the Utility directory with Create, Write, Erase, and Modify rights, as shown in Figure 6-3.

![](bbox=[0.13, 0.39, 0.65, 0.58])

Figure 6-3 A sample group trustee assignment

Kellie's effective rights would then be [R W C E M F]; the [R F] rights come from her membership in the ITMgrs group, and the [W C E M] rights come from the trustee assignment made to the KThiele user account. Luke's effective rights would be [R F] from being a member of the ITMgrs group.

You can use **Remote Manager** to make trustee assignments. The advantages of this utility include being able to use the Internet to work from any location and to manage the server from other desktop environments, such as Linux or Macintosh. The main disadvantage is that you can't check effective rights for other users in **Remote Manager**. Checking a user's effective rights in a directory requires logging in to **Remote Manager** as that user. In addition to being slower, this method can be difficult if you don't know the user's password. In Activity 6-4, you learn how to use **Remote Manager** to make the trustee assignments shown previously in Figure 6-3. In Activity 6-5, you use **Remote Manager** to check effective rights for other users.

# Activity 6-4: Making Group Trustee Assignments in Remote Manager

**Time Required:** 5 minutes

**Objective:** Use **Remote Manager** to assign rights to groups.

**Requirements:** Internet Explorer from a Windows XP computer or Java-enabled Firefox from a SUSE Linux 10 computer

**Description:** In this activity, you use **Remote Manager** to make the ITMgrs group a trustee of the Utility directory with Read and File Scan rights. In addition, you give the KThiele user account [W C E M] rights.
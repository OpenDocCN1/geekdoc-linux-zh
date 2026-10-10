![](bbox=[0.11, 0.06, 0.15, 0.1])

Because you have to log in as different users to check their effective rights in Remote Manager, the remaining activities focus on using ConsoleOne, Windows, and NetWare Administrator to make it easier to set up trustee assignments and check effective rights. If you prefer to use Remote Manager from a Linux desktop and are using a dedicated server, you might want to run Remote Manager on your desktop and use ConsoleOne from your NetWare 6.5 server console, as described in Chapter 5, to check effective rights.

# Inherited Rights

Inherited rights are the NetWare feature that allows a user, group, or container's effective rights to a directory to “flow down” into files and other subdirectories. Inheritance is an essential concept in making file system security efficient by eliminating an excessive number of trustee assignments. For example, Eric wanted all users to have Read and File Scan rights in the Office, Desktop, and Utility subdirectories of Apps to install and run the software stored in these directories. Eric could have assigned rights to all users by making the UAS container a trustee of each subdirectory with Read and File Scan rights. However, by using inherited rights, he was able to simply assign the UAS container Read and File Scan rights to the CORP:Apps directory and then let the effective rights flow down to subdirectories, as shown in Figure 6-7. In Activity 6-7, you use Eric's method to give all your users rights to the software directories in the Apps directory structure.

![](bbox=[0.14, 0.37, 0.64, 0.58])

+   → Indicates trustee assignment

+   ↓ Indicates inherited rights

Figure 6-7 Using inherited rights

In Figure 6-7, a box for each user and group is included under each directory to indicate the user or group's trustee assignment and effective rights. A vertical arrow above a trustee assignment indicates that the rights are inherited from a higher directory. When calculating inherited rights for a specific object, be sure to remove any rights that will be blocked by an Inherited Rights Filter on that subdirectory or file. A horizontal arrow indicates that a direct trustee assignment has been made to that directory. A user's effective rights consist of the sum of the rights in the user's box combined with the rights in any group or container box to which he or she belongs.

![](bbox=[0.04, 0.8, 0.08, 0.86])

# Activity 6-7: Applying Inherited Rights

**Time Required:** 10 minutes

**Objective:** Use ConsoleOne to assign rights to containers and check effective rights.

**Requirements:** A completion of Activities 6-1 through 6-6 and an Apps directory structure containing a Utility subdirectory with at least one user in the Engineering OU created in Chapter 4
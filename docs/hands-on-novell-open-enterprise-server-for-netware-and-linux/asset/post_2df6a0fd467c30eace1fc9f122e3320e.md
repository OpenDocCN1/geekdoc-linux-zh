
## Activity 6-2: Making User Trustee Assignments in Windows

**Time Required**: 10 minutes

**Objective**: Use Windows to assign rights to users, groups, and containers.

**Requirements**: Same as Activity 6-1

**Description**: Kellie is taking a vacation, and before leaving, she wants to grant Luke the rights to manage files in her home directory. In this activity, you log in with the account you created for Kellie in Chapter 5, and then use Windows Explorer to add Luke as a trustee of Kellie’s home directory with Read and File Scan rights.

1. Log in with the user name you created for Kellie in Chapter 5:
   - a. Enter **KThiele** in the User name text box and the password you set for Kellie in the Password text box.
   - b. Click the **Advanced** button, click the **Context** browse button, navigate to your UAS container, click the IT OU, and then click **OK** to place ITUAS in the Context text box.
   - c. Click **OK** to log in.
2. If necessary, log on to your Windows computer with your local user name and password.
3. Follow these steps to map drive letter L: to the IT directory:
   - a. Right-click **My Network Places**, and then click **Novell Map Network Drive** to open the Map Drive dialog box.
   - b. Click the **Choose the drive letter to map** list arrow, and then click L: in the list of options.
   - c. Enter \\IPAddress\volumepath\IT (with IPAddress representing your server’s IP address and volumepath representing the path to your CORP volume data) in the Enter the network path to the resource text box, and then click the **Map** button to open a window for the IT directory.
4. Follow these steps to add Luke as a trustee of Kellie’s home directory:
   - a. Right-click Kellie’s home directory, and click **Properties** to open the KThiele Properties dialog box.
   - b. Click the **NetWare Rights** tab to display the Trustees list box shown in Figure 6-1.

![](img/840007e8f98ea6653e5877e945c27dc6_233_0.png)

Figure 6-1 Viewing current trustees in the KThiele Properties dialog box

   - c. If necessary, expand the IT OU in the lower pane.
   - d. Click **L**McMann, and then click the **Add** button to add Luke to the Trustees list box. Record Luke’s default rights here: ____________
   - e. If necessary, change LMcMann's rights to only Read and File Scan access rights.
   - f. Click **OK** to save the assignment.
5. Close the IT directory window, and stay logged in for the next activity.

## Viewing Effective Rights

When working with file system security, often you need to verify a user's effective rights to a directory. Although you can use Windows Explorer or Remote Manager to view your effective rights in any directory or file, you can't view another user's effective rights. To verify effective rights in the file system, you should use ConsoleOne or NetWare Administrator. In Activity 6-3, you learn how to use ConsoleOne to check a user's effective rights in a directory.

![](img/840007e8f98ea6653e5877e945c27dc6_234_0.png)

## Activity 6-3: Viewing Effective Rights with ConsoleOne

**Time Required**: 5 minutes

**Objective**: Use ConsoleOne to list rights for users.

**Requirements**: Same as Activity 6-1

**Description**: In this activity, you use ConsoleOne to view Luke's effective rights to Kellie's home directory.

1. If necessary, log in to eDirectory with your administrative user name and password, start ConsoleOne, and then click to expand your eDirectory tree and UAS container.
2. If necessary, click to expand the **IT OU**.
3. Follow these steps to view the trustees of Kellie's home directory:
   - a. Right-click the **KThiele** directory, and then click **Properties** to open the Properties of KThiele dialog box.
   - b. Click the **Trustees** tab to display all trustees of Kellie's home directory. Record the trustees here:
4. Follow these steps to check Luke's effective rights to Kellie's home directory:
   - a. Click the **Effective Rights** button to open the Effective Rights dialog box, shown in Figure 6-2.

![](img/840007e8f98ea6653e5877e945c27dc6_234_1.png)

Figure 6-2 The Effective Rights dialog box

   - b. Click the **browse** button next to the Trustee text box to open the Select Object dialog box.
   - c. Click the **up arrow** to display all users in the IT OU.
   - d. Click **L**McMann, and then click **OK** to display effective rights for Luke. Record the effective rights here:
   - e. Click **Close** to close the Effective Rights dialog box.
5. Click **Cancel** to close the Properties of KThiele dialog box. Exit ConsoleOne, and log out.

## Group Trustee Assignments

As described in Chapter 5, groups are network objects that help organize users with common network requirements and are useful in simplifying trustee assignments. When a group is made a trustee of a directory or file, all members of that group are also considered trustees of the directory or file, with the same rights assigned to the group. When users are members of a group, their effective rights in a directory are a combination of any personal trustee assignments plus any rights they have from being group members. For example, all IT Department users need to have Read and File Scan rights to the Apps\Utility directory to run certain software. To do this, you can make the ITMgrs group created in Chapter 5 a trustee of the Apps\Utility directory with Read and File Scan rights. Because Eric, Kellie, and Luke are members of the ITMgrs group, they have Read and File Scan rights to the Apps\Utility directory. If you want Kellie's user account to be responsible for changing data, you could also make her a trustee of the Utility directory with Create, Write, Erase, and Modify rights, as shown in Figure 6-3.

![](img/840007e8f98ea6653e5877e945c27dc6_235_0.png)

Figure 6-3 A sample group trustee assignment

Kellie's effective rights would then be [R W C E M F]; the [R F] rights come from her membership in the ITMgrs group, and the [W C E M] rights come from the trustee assignment made to the KThiele user account. Luke's effective rights would be [R F] from being a member of the ITMgrs group.

You can use **Remote Manager** to make trustee assignments. The advantages of this utility include being able to use the Internet to work from any location and to manage the server from other desktop environments, such as Linux or Macintosh. The main disadvantage is that you can't check effective rights for other users in **Remote Manager**. Checking a user's effective rights in a directory requires logging in to **Remote Manager** as that user. In addition to being slower, this method can be difficult if you don't know the user's password. In Activity 6-4, you learn how to use **Remote Manager** to make the trustee assignments shown previously in Figure 6-3. In Activity 6-5, you use **Remote Manager** to check effective rights for other users.

## Activity 6-4: Making Group Trustee Assignments in Remote Manager

**Time Required:** 5 minutes

**Objective:** Use **Remote Manager** to assign rights to groups.

**Requirements:** Internet Explorer from a Windows XP computer or Java-enabled Firefox from a SUSE Linux 10 computer

**Description:** In this activity, you use **Remote Manager** to make the ITMgrs group a trustee of the Utility directory with Read and File Scan rights. In addition, you give the KThiele user account [W C E M] rights.

1. If necessary, start your computer, and log on to your local system. If you're using Windows with Novell Client, you can log in to eDirectory with your administrative user name and password.
2. Start your Web browser and enter `https://IPAddress:8009` (replacing `IPAddress` with the IP address of your NetWare 6.5 server) to display the Remote Manager Login window.
3. Log in to Remote Manager with your administrative user name and password.
4. Under the Manage Server heading, click the **Volumes** link to display the Volume Management window.
5. Click the **CORP** volume to open it. (If you're working on a shared classroom server, click your **STUDENTS** volume first and then click your `##Corp` directory).
6. Click your **Apps** directory to display all its subdirectories (see Figure 6-4).

![](img/840007e8f98ea6653e5877e945c27dc6_236_0.png)

7. Click the **Info** icon next to the Utility directory to display the Directory entry information window shown in Figure 6-5.

![](img/840007e8f98ea6653e5877e945c27dc6_236_1.png)

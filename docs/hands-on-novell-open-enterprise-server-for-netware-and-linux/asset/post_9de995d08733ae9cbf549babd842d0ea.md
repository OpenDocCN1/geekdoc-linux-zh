
![](img/840007e8f98ea6653e5877e945c27dc6_246_0.png)

The Inherited Rights and Filters dialog box

-   f. Click **Cancel** to close the Inherited Rights and Filters dialog box.
-   g. Click **OK** to close the 2006 Properties dialog box.

-   7. Close the window for the USAGE subdirectory.
-   8. Close any open windows, and leave ConsoleOne open for the next activity.

## Working with Supervisor Rights

When combining inherited rights and trustee assignments, you must remember that a new trustee assignment for a user, group, or container object overrides the object’s inherited rights and becomes the object’s effective rights with one exception: When a user, group, or container has been granted the Supervisor right to a directory, new trustee assignments made to subdirectories or files don’t override the inherited Supervisor right. For example, to help limit use of the Admin account, an administrator might want to give a special user account rights to manage certain directory structures. You can do this in one of two ways: Grant a user name or Organizational Role object all rights [R W C E M F A] to the directory structures, or grant the Supervisor right to the directory structures. If you grant all rights, the rights can be redefined in a subdirectory. However, if you grant the Supervisor right to a directory structure, the rights can’t be reduced by another trustee assignment or IRF, as shown in Figure 6-11.

![](img/84007e8f98ea6653e5877e945c27dc6_246_1.png)

Granting the Supervisor right

When the Supervisor right is assigned to a directory, it can't be changed or blocked in one of the subdirectories; it can be changed only at the point of origin. Therefore, the user with the Supervisor right can manage an entire directory structure without being blocked by another user or an incorrect trustee assignment. In the following activities, you practice assigning the Supervisor right to the EKenton user account and then attempt to change your effective rights in the directory structure.

## Activity 6-11: Granting Supervisor Rights

Time Required: 10 minutes

Objective: Use ConsoleOne to assign rights to users.

Requirements: Same as Activity 6-1

Description: To manage information in the IT and Apps directory structures without having to log in as the Admin user, Eric made his user account a trustee of the IT directory with the Supervisor right. In this activity, you use ConsoleOne to grant the EKenton user account Supervisor rights to the Apps and IT directories, and then verify effective rights in each location.

-   1. If necessary, start your Windows computer, log in to eDirectory with your administrative user name and password, and start ConsoleOne.
-   2. If necessary, click to expand your eDirectory tree and UAS container.
-   3. If necessary, click to expand your CORP volume. (If you're using a classroom server, expand your Corp directory)
-   4. Follow these steps to add the EKenton user as a trustee of the IT directory with Supervisor rights:
    -   a. Right-click the IT directory, and then click Properties to open the Properties of IT dialog box.
    -   b. Click the Trustees tab to display the existing trustees of the IT directory.
    -   c. Click the Add Trustee button to open the Select Object dialog box.
    -   d. If necessary, click the up arrow to navigate to your IT OU.
    -   e. Click the EKenton user name and then click OK to add it to the Trustees list box.
    -   f. Click the Supervisor right, and then click OK to save the assignment.
-   5. Follow these steps to check Eric's effective rights in the KThiele subdirectory:
    -   a. If necessary, expand the IT directory.
    -   b. Right-click the KThiele subdirectory, and then click Properties to open the Properties of KThiele dialog box.
    -   c. Click the Trustees tab, and then click the Effective Rights button to open the Effective Rights dialog box.
    -   d. Click the browse button to open the Select Object dialog box.
    -   e. Click the up arrow to navigate to the IT OU, click the EKenton user name, and then click OK to display his effective rights in Kellee's subdirectory. Record the effective rights here:
-   6. Close the dialog box, and then click Cancel to return to the ConsoleOne window. Leave ConsoleOne open and stay logged in for the next activity.

## Activity 6-12: Changing Supervisor Rights

Time Required: 10 minutes

Objective: Use ConsoleOne to assign rights to users.

Requirements: Completion of Activity 6-11

**Description:** Kellie was not happy about Eric having Supervisor rights to her home directory. She would prefer he had only Read and File Scan rights. In this activity, you learn how Eric used ConsoleOne to reduce his Supervisor right in Kellie’s home directory by experimenting with different trustee assignments and checking his effective rights.

-   1. If necessary, start your Windows computer, log in to eDirectory with your administrative user name and password, and start ConsoleOne.
-   2. If necessary, click to expand your eDirectory tree and **UAS** container.
-   3. If necessary, click to expand your **CORP** volume (or **Corp** directory, if you're using a shared classroom server) and the **IT** directory.
-   4. Follow these steps to add the **Ekenton** user name as a trustee of Kellie’s home directory with only Read and File Scan rights:
    -   a. Right-click the **KThiele** subdirectory, and then click **Properties** to open the Properties of KThiele dialog box.
    -   b. Click the **Trustees** tab, and then click the **Add Trustee** button to open the Select Objects dialog box.
    -   c. If necessary, click the **up arrow** to navigate to the **IT OU**.
    -   d. Double-click the **IT OU**, click the **Ekenton** user name, and then click **OK** to add it to the Trustees list box with the default Read and File Scan rights.
    -   e. Click the **Apply** button to save the assignment.
-   5. Follow these steps to check Eric’s effective rights in Kellie’s home directory:
    -   a. Click the **Effective Rights** button to open the Effective Rights dialog box.
    -   b. Click the **browse** button to open the Select Object dialog box.
    -   c. Click the **up arrow** to navigate to the **IT OU**.
    -   d. Double-click the **IT OU**, click the **Ekenton** user name, and then click **OK** to display his effective rights. Record Eric’s effective rights and explain how he obtained them: ____________________________
-   6. Click **Close** twice to return to the ConsoleOne window.
-   7. For Eric’s trustee assignment to work in Kellie’s directory, you need to remove the Supervisor right from his trustee assignment in the IT directory at the point of origin and replace it with all rights by following these steps:
    -   a. Right-click the **IT** directory, and then click **Properties** to open the Properties of IT dialog box.
    -   b. Click the **Trustees** tab to display the trustee assignments.
    -   c. Click the **Ekenton** user name’s trustee assignment, change the access rights to remove the Supervisor right, and then select all other rights.
    -   d. Click the **Apply** button to save the trustee assignment changes, and then close the dialog box.
-   8. Right-click the **KThiele** subdirectory, and then click **Properties**. Click the **Trustees** tab, repeat Step 5, and record Eric’s effective rights in Kellie’s home directory: ____________________________
-   9. Click **Close** and then click **Cancel** to return to the ConsoleOne window.
-   10. Exit ConsoleOne, and log out.

## Using the RIGHTS Command

Documenting user trustee assignments is an important task in managing a network file system. Using ConsoleOne or Remote Manager to view trustee assignments and determine user effective rights in each directory and subdirectory of a large file system can be time consuming. The **RIGHTS** command is another method of displaying and printing trustee assignments in a directory structure. In addition, the **RIGHTS** command is convenient for making trustee assignments from the command prompt or creating a batch file or

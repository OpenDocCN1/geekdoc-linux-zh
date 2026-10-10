
![](img/840007e8f98ea6653e5877e945c27dc6_221_0.png)

Figure 5-30 The Move Object window

8. Click the **Exit** button to end your iManager session and return to the iManager Login window.
9. Close your Web browser and log off the local computer.

# Moving a Container Object

When managing the structure of the eDirectory database, sometimes you need to move a container object from one location to another within the eDirectory hierarchy to make access to resources easier, for example. As discussed in Chapter 7, when a container becomes a subcontainer of another container object, the subcontainer has access rights to objects in the parent container. For example, Mfg is currently a subcontainer of the Engineering container, but Luke McHann has suggested that Mfg be made a separate container to prevent accidental access to Engineering Department resources.

Moving a container object is more complex than moving a leaf object because it changes the hierarchy of the eDirectory tree, thereby reorganizing the eDirectory database. In Chapter 4, you learned that the eDirectory database is divided into one or more partitions, starting with the root partition. Each partition is a separate file or replica located on one or more NetWare servers. The main reason for creating additional partitions is to divide a large eDirectory database into smaller files or replicas for more efficient access. However, partitioning eDirectory also makes it easier to move containers. When a container is made a separate partition, it becomes a separate file that can be moved and synchronized to another location in the hierarchical structure of the eDirectory database. As a result, to move a container object to another location in the eDirectory tree, you need to perform these three steps:

- Create a partition that starts with the container to be moved (the Mfg OU, in this example).
- After a partition has been created for the container, use ConsoleOne or iManager 2.5 to move the container’s partition to the new location. (iManager version 2.0 does not include an option to move container objects.)
- Complete the move by merging the Mfg container’s partition back into the root partition.

Another consideration when moving container objects is that creating and merging partitions requires changes to the root partition of the eDirectory tree. As a result, to move container objects, NetWare requires that your user name have the Supervisor right to the root of the eDirectory tree, as described in Chapter 7. In Activity 5-20, you perform a three-part procedure to move one of your OUs to a new location.

# Activity 5-20: Moving an OU in ConsoleOne

**Time Required:** 10 minutes

**Objectives:** Use ConsoleOne to move a container object.

**Requirements:** A Mfg OU within the Engineering OU (created in Chapter 4)

**Description:** This activity consists of three parts. In Part I, you make a separate partition for the Mfg container. In Part II, you move the Mfg container to the UAS Organization, and in Part III, you merge the Mfg partition into the UAS root partition.

![](img/840007e8f98ea6653e5877e945c27dc6_222_0.png)

# Part I: Creating a New Partition

Before you can move a container object, you need to make the container a separate partition. Follow these steps:

1. If necessary, log in to eDirectory with your administrative user name and password.
2. Start ConsoleOne.
3. To display partition information in the ConsoleOne window, click your **UAS** Organization, and then click **View, Partition and Replica View** from the menu.
4. If necessary, expand the **Engineering OU** to display the Mfg OU, and then click the Mfg OU to select it.
5. Click **Edit, Create Partition** from the menu to open the Create Partition dialog box.
6. Click **OK** to create a new partition and return to the ConsoleOne Partition and Replica view.
   Record the change to the Mfg container icon:

# Part II: Moving the Container

After the container is a separate partition, you can use ConsoleOne to move the Mfg container beneath the UAS Organization by following these steps:

1. Right-click the Mfg partition, and then click **Move** to open the Move dialog box.
2. Click the **browse** button next to the Destination text box to open the Select Object dialog box.
3. Navigate to and click your UAS container, and then click **OK**.
4. Click **OK** to move the Mfg OU.

# Part III: Merging the Mfg Partition Back into the Root Partition

Although he could have left Mfg as a separate partition, Eric wanted to keep the number of partitions to a minimum to reduce administrative overhead. In this part of the activity, you merge the Mfg partition back into the root partition by performing these steps:

1. Click the Mfg partition to select it.
2. Click **Edit, Merge Partition** from the menu to open the Merge Partition dialog box.
3. Click **OK** and wait for the Mfg partition to be merged back into the parent UAS partition. After the merge is finished, the partition icon is removed from the Mfg OU.
4. Change the view back to the Console view by clicking **View, Console View** from the menu.
5. Click the **Mfg OU** to confirm that all objects have been moved along with the Mfg container to be placed under the UAS Organization.
6. Exit ConsoleOne, and log out.

Congratulations! You're well on your way to becoming a CNA. Now that you've established login security by creating user, group, and Organizational Role objects for the IT Department, you can apply what you've learned to set up login security for the other UAS departments by performing the end-of-chapter projects. In Chapter 6, you secure the file system by granting users the rights they need to access files and applications.

# CHAPTER SUMMARY

- Network administrators must know how to set up the eDirectory system by creating the necessary objects and establishing a login security system. Although ConsoleOne is a powerful and easy-to-use Windows-based utility that Novell CNAs use when setting up and securing the network, NetWare 6.5 relies primarily on the iManager utility to create and maintain user and group objects via a Web browser.

- Login security consists of account restrictions, intruder detection, and authentication. Account restrictions include password, time, and address restrictions and can be set for user and user template objects. Intruder detection, enabled on a container-by-container basis, helps protect against attackers guessing user passwords by locking user accounts after the specified number of incorrect login attempts have been made in a given time period.

- User templates make creating user objects more efficient. You can use them to define the path to users' home directories and set common account and password restrictions.

- LDAP provides a way to exchange directory information between systems that are X.500 compatible, such as eDirectory and Microsoft Active Directory, by using LDIF files. You can use LDIF files as a quick way to create user objects.

- Novell supplies an Organizational Role object that's useful when assigning rights to certain user accounts. Organizational Role objects are similar to groups, except that they usually represent positions in the organization. If another user is assigned the responsibilities, you simply need to change the occupant of the organizational role to give him or her the required privileges.

- When managing an eDirectory system, often you need to move objects from one container to another. Although moving leaf objects is fast and easy, moving a container from one location to another requires creating a partition starting at the container to be moved, moving the partition to the new location, and then merging the new partition with the parent partition of the container it has been moved into.

# KEY TERMS

**address restrictions** — Security restrictions that require a user to log in only from specified client IP addresses.

**authentication** — The part of NetWare security that helps protect against attackers by validating each network packet to guarantee that it was sent from an authorized user.

**authorization** — The process of verifying a user's name and password to allow him or her to access network resources.

**intruder detection** — A part of login security that works at the container level by setting a limit on the number of incorrect login attempts that can be made on a user account during a specified time period.

**Lightweight Directory Interchange Format (LDIF)** — An ASCII text file format that uses a standardized syntax to add, change, or delete objects in LDAP-compatible directory systems.

**login security** — The security system used to perform the authorization process. *See also authorization*.

**Organizational Role object** — An object type that enables you to assign rights to a job position, for example, rather than a specific user.

**password restrictions** — Security restrictions that force users to use passwords that exceed or meet a minimum length and must be changed within a specified period.

**time restrictions** — Security restrictions that allow users to log in to the network only during specified hours.

**user template** — A property that defines standard settings and configures restrictions for each user in a container.

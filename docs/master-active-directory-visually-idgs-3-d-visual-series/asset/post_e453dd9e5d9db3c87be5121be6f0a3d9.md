
# RESTORING THE ACTIVE DIRECTORY (CONTINUED)

When you use the Restore Wizard, you select what items you want to restore. This is particularly useful if a folder is lost. You can restore the folder and the files in it without having to perform a complete restore of your entire system.

To restore the Active Directory, you choose to restore System State Data.

The wizard may prompt you for the location of the backup job, and then the restore process begins. After the restoration is complete, you can reboot your computer. When the server is back online, changes are replicated from the other domain controllers so that the Active Directory database on your computer is up-to-date.

In some instances, however, you may not wish for certain data to be updated through replication. In this case, you can choose to *authoritatively* restore that data. You can learn how to use an authoritative restore in the next section.

![](img/763d5ae436311371600c0952a3da9094_513_0.png)

![](img/763d5ae436311371600c0952a3da9094_513_1.png)

3. Click Restore Wizard.
4. The Restore Wizard appears.
5. Click Next to continue.

## TIPS

**Can I restore other data when I am restoring the System State Data, or should I perform this task individually?**

You can restore any data that you want by selecting the desired data in the file list. The Restore Wizard then restores all the data that you select.

**What happens if I leave my server in safe mode?**

Safe mode is provided so that you can repair problematic parts of your system. When safe mode is in effect, a limited number of hardware drivers are running and your server services are disabled. If you leave your server in safe mode, it is not available on the network or to service clients. Also, your Active Directory data cannot be updated through replication with other domain controllers until you reboot into normal mode.

![](img/763d5ae436311371600c0952a3da9094_514_0.png)

![](img/763d5ae436311371600c0952a3da9094_514_1.png)

5. Expand the What To Restore File and select System State by clicking the check box.
6. Click Next to continue.
7. Click Finish to perform the restore.

## PERFORMING AN AUTHORITATIVE RESTORE

After performing an Active Directory restore using the Restore Wizard, you may also need to perform an authoritative restore as well before rebooting from safe mode. An authoritative restore is used to tag certain information to prevent the Active Directory replication process from updating it. For example, say you accidentally delete an OU. The deletion is then replicated to the other domain controllers. You can restore that OU from backup, but when you bring your server online, the other domain controllers delete it again because of replication. An authoritative restore prevents this from happening. When you authoritatively restore an object, OU, or domain, the restore is tagged as authoritative and replicated to the other domain controllers instead of the domain controllers replicating the error back to the server.

The authoritative restore is performed using the command line utility, Ntdsutil, which is accessible from the Run line. If you want to perform an authoritative restore, you must do so after the Backup Wizard restore has taken place and before you reboot your server out of safe mode.

![](img/763d5ae436311371600c0952a3da9094_515_0.png)

### TIPS

**What happens if I perform a restore and reboot my server before running an authoritative restore?**

If you reboot into normal mode before using authoritative restore, the server will be updated through replication. If you are trying to replace an accidentally deleted object or another operation in which replication should not overwrite the restore, then you must use the authoritative restore function. If not, the error is replicated back to your server and you have to go through the restore process again.

**Can Ntdsutil perform other tasks?**

Yes. Ntdsutil can help you with other Active Directory management tasks. To see a list, simply access Ntdsutil at the Run line and then type Help when the console opens.

![](img/763d5ae436311371600c0952a3da9094_516_0.png)

![](img/763d5ae436311371600c0952a3da9094_516_1.png)

5. Type `restore subtree` followed by the correct information for the object, OU, or domain.
6. Review the results and type `quit` to end the Ntdsutil session.

## CLEANING THE LOST AND FOUND FOLDER

For the most part, Active Directory maintains itself. It performs replication automatically, defragments the database, and takes care of database issues. The Active Directory also performs “garbage cleanup” at 12-hour intervals to remove unnecessary log files and delete old, or tombstoned, objects from the Active Directory.

One item you should occasionally check, however, is the LostAndFound folder. LostAndFound is a hidden container in Active Directory Users and Computer. From time to time, misplaced objects are put in the LostAndFound container. For example, say you create an object to be added to a container. At the same time, another administrator deletes the container. Now, the object has nowhere to go. Because the Active Directory cannot determine where to place the object, it is put in the LostAndFound container and held there.

As a part of your administrative duties, you should occasionally check the LostAndFound container to see if the objects residing there need to be deleted or moved to a valid container.

![](img/763d5ae436311371600c0952a3da9094_517_0.png)

![](img/763d5ae436311371600c0952a3da9094_517_1.png)

1. Choose **Start** > **Programs** > **Administrative Tools** > **Active Directory Users and Computers**.
2. The Console opens.

![](img/763d5ae436311371600c0952a3da9094_518_0.png)

### TIPS

**How can I move a LostAndFound object?**

If you find an object in the LostAndFound container that you want to keep, you can move it to a different location. Select the object and then choose Action > Move. In the window that appears, select a new location for the object.

**How often should I check the LostAndFound container?**

Objects end up in the LostAndFound container only in environments with multiple domain controllers and even multiple domains. In an Enterprise environment, you should check the LostAndFound container every few weeks because a greater possibility of misplaced objects exists. In medium to smaller environments, a once-a-month check is plenty.

![](img/763d5ae436311371600c0952a3da9094_518_1.png)

3. Choose View > Advanced Features.

![](img/763d5ae436311371600c0952a3da9094_518_2.png)

4. Click LostAndFound.
5. Review any files in the details pane and delete or move them as necessary.

# RESOURCE KIT TOOLS

## Installing the Resource Kit

To help you manage and maintain the Active Directory, the Windows 2000 Resource Kit contains some additional tools for Active Directory management. These tools are described in the following sections so that you can see what tools are available, what they do, and when you would want to use them.

Before you can access the tools, you must install the Resource Kit that is located on your Windows 2000 Server CD-ROM. Browse the CD, open the Support folder, and then open the Reskit folder. Double-click the Setup icon to install the Resource Kit on your server. The Resource Kit contains both tools and online documentation to assist you with a variety of Windows 2000 features and options.

You can also expect Microsoft to release updates, patches, and additional tools for the Active Directory from time to time. You can keep abreast of these updates by accessing the update Web site available at Start > Windows Update.

![](img/763d5ae436311371600c0952a3da9094_519_0.png)

![](img/763d5ae436311371600c0952a3da9094_519_1.png)

1. Open the installation CD-ROM.
2. Open Support, Reskit, and then double-click Setup.
3. Follow the on-screen instructions to complete setup.

## Accessing the Resource Kit

After you install the Resource Kit, you can access it from the Start > Programs menu. You see from this menu that you can choose to open either the online books or the Tools Console.

When the console opens, you can expand the Resource Kit, expand Windows 2000 Resource Kit, and click on Tools A to Z. A list of available tools on the Resource Kit appears in the details pane.

If you are uncertain about which tool you want to use, click the Tool Categories container in the left pane so that each tool is accompanied by a short description in the details pane.

The following sections point out the tools that are useful with Active Directory management and when you should consider using each particular tool.

![](img/763d5ae436311371600c0952a3da9094_520_0.png)

1. Choose Start > Programs > Resource Kit > Tools Management Console.

![](img/763d5ae436311371600c0952a3da9094_520_1.png)

2. Expand the Resource Kit and click Tools A to Z or Tools Categories.

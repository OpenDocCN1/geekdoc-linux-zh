
![](img/4e6a76e57a4105be55d8a1cc0750b023_34_0.png)

Figure 20. Specifying other groups for the user

When you have added all the groups you want, click **OK** to continue.

- **Login shell** - the shell that is started when the user logs in.
- **Password** - the password used to log in. To define a password, click the button labeled **<not displayed>** and you will see a window similar to Figure 21.

![](img/4e6a76e57a4105be55d8a1cc0750b023_34_1.png)

Figure 21. Specifying the password for the new user

Type in the password for the user and click **OK** to continue.

> Note
> Caldera OpenLinux uses shadow passwords by default.

- Home directory - this is the user's home directory. It is the first place a user to go when logging in. It contains files and programs that are owned and used by that user.

- Disabled/Enabled - with this you define if an account is enabled or disabled. You can toggle this by clicking the button.

- Shadow information - here you define the password properties: expiration, change timeframe, etc. If you want to change the default, click the button and you will see a window similar to Figure 22.

![](img/4e6a76e57a4105be55d8a1cc0750b023_35_0.png)

Figure 22. Password properties for the new user

When you have edited the properties, click OK to save them.

3. After you have typed in all necessary information for the new user, click OK to create the new user.

## 2.8.1.1 Deleting a user

When you want to delete a user, select the user from the list and click User > Delete User. You will see a window similar to Figure 23.

![](img/4e6a76e57a4105be55d8a1cc0750b023_36_0.png)

Figure 23. Deleting a user

Click **Yes** to delete the user.

## 2.8.1.2 Editing a user

When you want to edit a user, select the user from the list and choose **User > Edit User.** You will see a window similar to Figure 24.

![](img/4e6a76e57a4105be55d8a1cc0750b023_36_1.png)

Figure 24. Edit a user

Here you can modify the following attributes of a user:

- Other groups
- Login shell
- Password
- Home directory
- Disabled/Enabled
- Shadow information

We described these attributes in 2.8.1, "Managing accounts" on page 21.
When you are done, click OK.

## 2.8.2 Managing groups

You can access the tool for managing groups by selecting Accounts > Groups > Manage groups. You will see a window similar to Figure 25.

![](img/4e6a76e57a4105be55d8a1cc0750b023_37_0.png)

Figure 25. Group Administration

Here you can perform operations related to the groups.

### 2.8.2.1 Creating a new group

You can create a new group by selecting Groups > Create Group. You will see a window similar to Figure 26.

![](img/4e6a76e57a4105be55d8a1cc0750b023_38_0.png)

Figure 26. Creating a new group

Type in the name of the new group and click **OK** to create it.

### 2.8.2.2 Deleting a group

Select the group you want to delete from the list of all the groups and choose **Groups > Delete Group**. You will see a window similar to Figure 27.

![](img/4e6a76e57a4105be55d8a1cc0750b023_38_1.png)

Figure 27. Deleting a group

Click **Continue** to actually delete a group.

### 2.8.2.3 Rename a group

Select the group you want to rename from the list of all the groups and choose **Groups > Rename Group**. You will see a window similar to Figure 28.

![](img/4e6a76e57a4105be55d8a1cc0750b023_39_0.png)

Figure 28. Renaming a group

Type in the name for the group and click **OK** to rename.

### 2.8.2.4 Merge a group

You have the option to merge users from one group to another. Select the group to which you want to merge another and choose **Groups > Merge Group**. You will see a window similar to Figure 29.

![](img/4e6a76e57a4105be55d8a1cc0750b023_39_1.png)

Figure 29. Merge a group

Type in the name of the group you want to merge. Click **OK** to continue.

### 2.8.2.5 Group membership

You can change the members of a group. To change the members of a desired group select the group from the list of all the groups and choose **Groups > Group Membership**. You will see a window similar to Figure 30.

![](img/4e6a76e57a4105be55d8a1cc0750b023_40_0.png)

Figure 30. Group membership

You can add or remove users from a group. Click OK to save your changes.

## 2.9 Daemons (services)

This tool is used to manipulate the daemons that will start at server startup. After the tool is started, you will see a window similar to Figure 31.

![](img/4e6a76e57a4105be55d8a1cc0750b023_40_1.png)

Figure 31. System services

Here you define which services (daemons) will be started at startup. When you are finished, click OK to save your changes.

## 2.10 Filesystem

You can mount or unmount the devices. After the tool is started, you will see a window similar to Figure 32.

![](img/4e6a76e57a4105be55d8a1cc0750b023_41_0.png)

Figure 32. Filesystems

On the left side you see unmounted devices. If you want to mount the device, select it from the list and click **Mount**. On the right side you see mounted devices. If you want to unmount an already mounted device, select it from the list and click **Unmount**. By selecting the mounted or unmounted device and clicking **Info**, you will see the information about the particular device.

### 2.10.1 Mounting an NFS volume

You can mount NFS filesystem by choosing **Action > Mount**. You will see a window similar to Figure 33.

![](img/4e6a76e57a4105be55d8a1cc0750b023_42_0.png)

Figure 33. Mounting an NFS volume

Type in the required values and click OK to mount the NFS volume.

## 2.11 Hostname

Here you can change the hostname of your server. After the tool is started, you will see a window similar to Figure 34.

![](img/4e6a76e57a4105be55d8a1cc0750b023_42_1.png)

Figure 34. Changing the hostname

Type in the new hostname and click OK to save it.

## 2.12 Resources

With this tool you can examine hardware resources. After the tool is started, you will see a window similar to Figure 35.

### System Resource Information

This table shows you several information about your cpu(s). You can access more information over the info menu.

| system resource | resource value |
|---|---|
| processor | 1 |
| vendor_id | Intel |
| cpu family | 6 |
| model | 5 |
| model name | Pentium II (Desch) |
| stepping | cpu MHz | 399.09174 |
| cache size | 512 KB |
| fdiv_bug | no |
| hit_bug | no |

Figure 35. System resources

Here you can get information about the following resources:

- Block devices
- Character devices
- Interrupts
- System load average
- IOports
- DMA

To access this information, select the appropriate option from the Info menu. For example if you select Interrupts, you will see a window similar to Figure 36.

### System Interrupts

Here you can see the registered interrupt lines, the number of already processed interrupts on that line, a '*' if it is shared interrupt and the device(s) using this interrupt.

| irq | device | processed |
|---|---|---|
| 0 | timer | 23849 |
| 1 | keyboard | 6335 |
| 2 | cascade | 0 |
| 6 | floppy | 60 |
| 8 | rtc | 0 |
| 10 | ips | 112149 |
| 11 | Intel EtherExpress | 164583 |
| 12 | PS/2 Mouse | 467340 |
| 13 | fpu | 1 |
| 14 | ide0 | 1563 |
| 15 | PCnet/Fast+ 79C | 17219 |

![](img/4e6a76e57a4105be55d8a1cc0750b023_44_0.png)

## 2.13 Time

Here you can set the time and time zone. After the tool is started, you will see a window similar to Figure 37.

![](img/4e6a76e57a4105be55d8a1cc0750b023_45_0.png)

Figure 37. Setting the time

Type in the current time. If you also want to change the time zone, click the button for it. You will see a window similar to Figure 38.

![](img/4e6a76e57a4105be55d8a1cc0750b023_45_1.png)

Figure 38. Setting the time zone

Select your region and you will be presented with the time zones for that region. Select the one that matches your city. After that you will be back in the System Time panel. Click OK to save the changes.

## 2.14 Peripherals menu

In the Peripherals menu of COAS tools you can access the following tools:

- **Mouse** - for managing the mouse
- **Printers** - for managing the printers

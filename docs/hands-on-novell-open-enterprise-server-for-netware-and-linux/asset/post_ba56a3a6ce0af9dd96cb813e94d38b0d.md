
## Directory Attribute Form

| Directory | Attributes |
|---|---|
| Shared | Di, Ri |
| Inventory | Di, Ri |
| Forms | Di, Ri |
| IT\Web | Di, Ri, P |
| Engineer | Di, Ri |
| Apps | Ri, P |
| Apps\Office | Di, Ri, P, Ic, H |
| Apps\Utility | Di, Ri, H |

Created by: 
Date: 

Figure 6-16 The UAS Directory Attribute Form

## File Attribute Form

| File | Attributes |
|---|---|
| Apps\Office\*.exe | Sh |
| Engineer\CAD\*.* | Ro |
| Apps\Utility\*.exe | X |

Created by: 
Date: 

Figure 6-17 The UAS File Attribute Form

attributes, the Execute Only attribute is important when software is used in an environment where there’s a possibility of illegal copying.

## Implementing Directory and File Attributes

As a network administrator, you need to be able to use NetWare utilities and Windows to set directory and file attributes in the network file system. Knowing how to use Remote Manager is required for the CNA test, but as a network administrator, you’ll also find it convenient to know how to use Windows utilities. In the following activities, you learn how to use Remote Manager and ConsoleOne to set and view file and directory attributes.

### Activity 6-14: Setting Directory Attributes in Remote Manager

- **Time Required:** 5 minutes
- **Objective:** Use Remote Manager to assign attributes to directories.
- **Requirements:** A Windows XP or SUSE Linux 10 computer and completion of Activity 3-5
- **Description:** In this activity, you use Remote Manager to set directory attributes on the Apps directory structure. You'll set attributes for the remaining directories shown in Figure 6-16 in the end-of-chapter projects.
    1. If necessary, start your computer, and log on to your local system. If you're using Windows with Novell Client, log in to eDirectory with your administrative user name and password.
    2. Start your Web browser and enter **https://*IPaddress*:8009** (replacing *IPaddress* with the IP address of your NetWare 6.5 server) to display the Remote Manager Login window.
    3. Log in with your administrative user name and password to display the Remote Manager Volume Management window.
    4. Navigate to your **CORP** volume (or **##Corp** directory, if you're using a shared classroom server).
    5. Click on the **Attributes** column of the Apps directory to display the Folder Attributes window shown in Figure 6-18.

![](img/840007e8f98ea6653e5877e945c27dc6_261_0.png)

    6. Click to enable the **Rename Inhibit** and **Immediate Purge** check boxes.
    7. Click **OK** to save your settings and return to the NetWare File Listing window.
    8. Click the **Apps** directory to display its contents.
    9. Click on the **Attributes** column of the Office directory to display the Folder Attributes window.
    10. Click to enable the **Delete Inhibit**, **Rename Inhibit**, **Immediate Purge**, **Immediate Compress**, and **Hidden** check boxes.

Many systems and utilities display hidden files and directories. By default, however, Windows XP doesn't display hidden files or directories unless you select Tools, Folder Options from the Windows Explorer menu and click the Show hidden files and folders option button in the View tab.

    11. Click **OK** to save your attribute settings and return to the NetWare File Listing window.
    12. Click the **Exit** button to return to the Remote Manager Login window.
    13. Close your Web browser, and stay logged in for the following activity.

### Activity 6-15: Setting Attributes in ConsoleOne

- **Time Required:** 5 minutes
- **Objective:** Use ConsoleOne to set directory attributes.
- **Requirements:** Completion of Activity 6-14 and a Windows XP computer with Novell Client installed
- **Description:** In this activity, you use ConsoleOne to set the remaining attributes Eric defined in Figure 6-16 for the Apps directories.
    1. If necessary, start your computer, and log in to eDirectory with your administrative user name and password.
    2. Start ConsoleOne.
    3. Expand your UAS container and navigate to your CORP volume (or ##Corp directory, if you’re using a shared classroom server).
    4. Click to expand the Apps directory.
    5. Follow these steps to set attributes for the Utility subdirectory:
        a. Right-click the Utility directory and click Properties to open the Properties of Utility dialog box shown in Figure 6-19.

![](img/840007e8f98ea6653e5877e945c27dc6_262_0.png)

Figure 6-19 The Properties of Utility dialog box

        b. If necessary, click the Attributes tab.
        c. Click to enable the Delete Inhibit, Rename Inhibit, and Hidden check boxes.
        d. Click OK to save the attribute changes and return to the ConsoleOne window.
    6. Close ConsoleOne, and stay logged on for the next activity. You set the remaining directory attributes in the end of chapter hands-on projects.

## The FLAG Command

Just as the RIGHTS command is useful for documenting or setting access rights from the DOS prompt, the NetWare FLAG command is useful for documenting and setting directory and file attributes. As a network administrator, you should know how to use the FLAG command’s directory and file options to work with attributes.

### Setting and Documenting Directory Attributes

The FLAG command uses the /DO parameter to set and view directory attributes:

```
FLAG path [+/-] attribute_list /DO
```

You can replace attribute_list with one or more of the directory attributes shown previously in Table 6-5. Use the + operator if you want to add the attribute to the directory or the - operator to remove the attribute from the directory. The path parameter is optional, and if you enter only the FLAG /DO command, you see a list of attribute settings for all subdirectories of the current directory. In the following activity, you practice using the FLAG command to view attribute settings.

### Activity 6-16: Documenting Attribute Settings with the FLAG Command

- **Time Required:** 5 minutes
- **Objective:** Use the FLAG command to document attribute settings.
- **Requirements:** Completion of Activity 6-15
- **Description:** In this activity, you use the FLAG command to document your directory attributes and then set attributes for the Forms directory.
    1. If necessary, start your computer, and log in with your administrative user name and password.
    2. Open a command prompt window (click **Start, Run**, type **command**, and click **OK**), and change to drive **F:**.
    3. View help information on the FLAG command by entering **FLAG /?** and pressing **Enter**. If you see the “Bad command or file name” message, enter **CD SYS:\PUBLIC**, press **Enter**, and repeat the FLAG command.
    4. To view help information on setting directory attributes, enter the **FLAG /? DO** command, and then press **Enter**.
    5. To view all your directory attribute settings, enter the **FLAG volumename:*.* /DO** command (substituting the path to your **##Corp** directory for *volumename*), and then press **Enter**. (For example, if you’re using a shared classroom server, enter the command **FLAG STUDENTS:##Corp\*.* /DO**, replacing **##** with your assigned student number. If you’re using a dedicated server, enter the command **FLAG CORP:*.* /DO**.)
    6. To view attribute settings for all subdirectories, enter the **FLAG volumename:*.* /DO /S** command, and then press **Enter**.
    7. To set the Delete Inhibit and Rename Inhibit attributes on your Forms directory, enter the **FLAG volumename:Forms +Di +Ri /DO** command, and then press **Enter**.
    8. Exit the command prompt window, and log out.

In a recent department meeting with David Hesse and other department managers, Eric reported that he had planned the NetWare 6.5 file system security in the Engineering and Manufacturing departments, which will enable users to take advantage of the network’s file system. Of course, managers were anxious to know when their departments would be ready to go online with the new NetWare 6.5 server. Eric explained that he had documented their processing needs and that you would be working with him to set up their file system access rights (see the projects at the end of this chapter).

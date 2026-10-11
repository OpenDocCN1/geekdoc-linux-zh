
## GROUP POLICY COMPUTER CONFIGURATION

You have a number of possibilities when configuring client computers using Group Policy. The computer configuration portion of the Group Policy is divided into three major categories: software settings, Windows settings, and administrative templates. Each of these containers have different policy files that you can configure for your policy. (See Appendix A for more information on configuring Group Policies.)

The software settings container has an icon for software installation. You can use the Group Policy to automatically install applications onto a user's computer using the Windows installer. This feature enables you to create custom application packages that are pushed to the user's computer and automatically installed. This feature allows each user in the group to have a particular set of applications automatically installed.

Explaining how to configure custom packages for your Group Policy is beyond the scope of this book, but you can refer to the Windows Help files or the Windows 2000 Server Resource Kit to learn more about software package development.

![](img/763d5ae436311371600c0952a3da9094_457_0.png)

![](img/763d5ae436311371600c0952a3da9094_457_1.png)

## CONFIGURING GROUP POLICY PROPERTIES

1. **Expand** the policy you want to configure and click Computer Configuration.
2. **Expand** the Software Settings, Windows Settings, and Administrative Templates containers to see the contents.
3. Select Software Installation.
4. Choose Action: Properties.

![](img/763d5ae436311371600c0952a3da9094_458_0.png)

![](img/763d5ae436311371600c0952a3da9094_458_1.png)

5. Click Browse to establish a default software installation package.
6. Use these buttons to configure options for user settings when a new package is added to a client computer.
7. Use these buttons to specify a basic or minimum user interface during the installation.
8. Click to uninstall the applications.

### How does the software installer work?

Just as a policy can download system and user settings, the Group Policy can be configured to push the installer application and installation files to a user's desktop. This feature allows the user to obtain a software installation without having to perform any of the installation manually. This feature ensures that all users have the same software applications installed and configured appropriately.

### Can a user manually change the software configuration as he would do during a normal setup routine?

The installation settings are defined by the Group Policy administrator when a software package is created. The entire package is then run on the client system. Depending on configuration, the user may be able to make some configuration choices, but this depends on the configuration of the package. This feature prevents users from making configuration changes during setup that are not desirable and ensures that all users in the group have the same software setup configuration.

## GROUP POLICY COMPUTER CONFIGURATION CONTINUED

By accessing the properties sheets for the package installation object, you can configure general options for the package installer. On the General tab, you can load a default package, and you can use the radio buttons to establish the way the packages appear to users. Under the New Packages category, you can choose the options:

- **Display the Deployment Software dialog box:** This dialog box appears when you deploy a new package so that you choose whether to assign, publish, or configure the package properties.
- **Publish:** This option specifies that you want the new package to be published when it is added. Publishing occurs to users only, not computers.
- **Assign:** This option specifies that you want the new package to be assigned with the standard package properties. Assignment can occur to either users or computers.
- **Configure Package Properties:** This option specifies that the configure package properties form should appear when a new package is added. You can use this if you expect to stray from the standard package properties.

![](img/763d5ae436311371600c0952a3da9094_459_0.png)

![](img/763d5ae436311371600c0952a3da9094_459_1.png)

9. Click the File Extensions tab.
10. Click the drop-down box to select a file extension.
11. Click Up or Down to rearrange the precedence.
12. Click the Categories tab.
13. Click Add.

- Use the File Extensions tab to generate a list of file extensions that will invoke the application to open on the user’s desktop.
- Use the Categories tab to configure categories under which the applications appear in Add/Remove programs in Control Panel.

## TIPS

### Can I change the file extensions that are associated with a software package?

Yes. The File Extensions tab enables you to list the file extensions that are to be associated with the package. For example, if you installed Microsoft Office, you can specify that the application should open automatically when a user attempts to open a Word (.doc) file. This feature is useful for programs that can handle a number of different file types and ensures that users use a certain program to work on a certain kind of file.

### Can I modify the way that programs appear under Add/Remove Programs in the Control Panel?

Yes. The Categories tab enables you to add categories in Add/Remove Programs in Control Panel where the software program will exist. This feature allows you to add custom categories so that all corporate software programs appear in one place. For example, the ABC Engineering has some custom programs. You can add a category labeled ABCs that appears in Add/Remove Programs in Control Panel so that the custom programs are stored in one location.

![](img/763d5ae436311371600c0952a3da9094_460_0.png)

![](img/763d5ae436311371600c0952a3da9094_460_1.png)

1. The Enter New Category dialog box appears.
2. Type the name of the category where the program will appear.
3. Click OK.
4. Click OK to close the properties sheet.

## ADDING A NEW PACKAGE TO THE CONSOLE

Choose Action->New->Package.

## GROUP POLICY COMPUTER CONFIGURATION CONTINUED

You can easily add different installer packages to the console by using the Action menu. You may have existing installer packages (.msi files) that have been previously created, and this option allows you to use those packages.

Next, you can configure the Windows settings so that they apply to the members of the Group Policy. You can expand the Windows Settings container, which enables you to configure both script and security settings. The Script icon in the console tree allows you to add startup and shutdown scripts that run automatically when a Group Policy member starts up and shuts down his or her computer. Scripts can be written and customized to meet the needs of your environment; then you can add them to the Group Policy from this location.

![](img/763d5ae436311371600c0952a3da9094_461_0.png)

1. Browse and select the Windows Installer package that you want to load.
2. Click Open.

![](img/763d5ae436311371600c0952a3da9094_461_1.png)

### WINDOWS SETTINGS

1. Expand the Windows Settings container and click the Scripts icon to configure the Startup and Shutdown scripts.

![](img/763d5ae436311371600c0952a3da9094_462_0.png)

## TIPS

### How many software packages can I add to the Group Policy?

You can add as many software packages to the Group Policy as needed for your organization. This is an issue that you should plan carefully so that the software installation feature of the Group Policy is used in an effective manner. Too many software packages can create management and traffic problems. The key rule is to use them as they are needed and to avoid unnecessary or trivial packages.

### What are startup and shutdown scripts?

Startup or shutdown scripts are custom scripts that run on the client computer when the computer is either started or shutdown. The script may perform system checks or file checks—basically anything that you want to run at either startup or shutdown. Scripts are often created for specific network or company needs.

![](img/763d5ae436311371600c0952a3da9094_462_1.png)

![](img/763d5ae436311371600c0952a3da9094_462_2.png)

1. Use this interface to add, edit, or remove startup scripts that you want applied to this Group Policy.
2. To view the current script files stored in the GPO, click Show Files.
3. Click Add.
4. Type the name of the script you want to load. You can also click Browse to locate the script you want to load.
5. Click OK.

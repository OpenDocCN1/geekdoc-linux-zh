
## Assigning an Application to a User or Computer

When an application is assigned to a user, the application is advertised on the Start menu of the user’s workstation. The actual installation of the application is triggered when the user attempts to access it through the Start menu. This allows the software to be installed on demand.

To understand the process of assigning an application to a user, consider this example: Suppose the Sales department needs to have all users running Microsoft Excel to complete their daily sales reports. Using a Group Policy linked to the Sales OU, you can modify the settings to include the assignment of the Excel package file. When a member of the Sales OU logs on, Windows Installer adds Excel as a selection on the Start menu and changes the registry to associate .xls files with Excel. When a user attempts to access the program for the first time using the Start menu selection, the installation process begins. Additionally, if the user attempts to open a file named with an .xls extension and Excel is not already installed, Windows Installer automatically begins the installation, and the file that was originally accessed will be opened upon completion. As we will discuss later in this lesson, installations can be configured to be totally automated or can require some user input.

The behavior of assigning an application using the Computer Configuration\Policies\Software Settings\Software Installation node of Group Policy is somewhat different than assigning it within the User Configuration node. When you use the Computer Configuration node, the application is installed during startup. This is a safe method, because a minimum number of processes compete for utilization and few, if any, other applications are running that could cause conflicts.

## Publishing an Application

Publishing an application is only available under the User Configuration\Policies\Software Settings\Software Installation extension. When an application is published, it is advertised in Add Or Remove Programs in the Control Panel. A published application is not listed as an option on the Start Menu or on the desktop as it is when an application is assigned. Using the Publish option instead of Assign might be preferred when users are allowed to choose their applications, rather than forcing them to use a specific application.

To understand the Publish option in Group Policy, consider the example of a company that has many graphic artists. Because the graphic artists have different software preferences, it has been determined that three applications will be available and users can install the application they prefer to use. Publishing a list of available applications allows users to install their preferred application or they can install all of them, if desired.

Using the Publish method of distributing applications also allows a file-activated installation to take place. This functionality is identical to the assigned application functionality discussed earlier. When a user opens a file associated with an application that does not currently exist on the user’s workstation, the application is installed.

> **WARNING**
>
> If you have blocked the availability of the Add Or Remove Programs application in Control Panel through Group Policy, users cannot access published applications. Prior to publishing applications, be sure to check that access to Control Panel or Add Or Remove Programs has not been blocked.
>
> As a precautionary step, you should test the available applications to ensure that they can function together if the user opts to install them all. With certain application types, such as multimedia applications, conflicts in the required versions of supporting files may cause a malfunction. It is always prudent to test each application and its compatibility before it is distributed to the users. In addition, testing the deployment to be sure that applications are distributed only to the intended recipients is equally important.

## CONFIGURE SOFTWARE INSTALLATION DEFAULTS

**GET READY.** To configure a GPO to assign or publish an application, complete the following steps:

1. **OPEN** the Group Policy Management Editor window for an existing GPO, and expand the User Configuration or the Computer Configuration node, followed by Policies, followed by Software Settings.
2. As shown in Figure 9-1, right-click the appropriate Software Installation node and then click **Properties**.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_227_0.png)

3. In the **General** tab of the Software Installation Properties dialog box, key the Uniform Naming Convention (UNC) path (`\\servername\sharename`) to the software distribution point for the Windows Installer packages (.msi files) in the GPO in the **Default Package Location** box.
4. In the **New Packages** section on the General tab, select one of the following:
    - **Display The Deploy Software Dialog Box**. Use this option to specify that the Deploy Software dialog box displays when you add new packages to the GPO, allowing you to choose whether to assign, publish, or configure package properties. This is the default setting.
    - **Publish**. Use this option to specify that the applications will be published by default with standard package properties when you add new packages to the GPO. Packages can be published only to users, not computers. If this is an installation under the Computer Configuration node of the Group Policy Object Editor console, the Publish choice is unavailable.
    - **Assign**. Use this option to specify that the applications will be assigned by default with standard package properties when you add new packages to the GPO. Packages can be assigned to users and computers.
    - **Advanced**. Use this option to specify that the Properties dialog box for the package will display when you add new packages to the GPO, allowing you to configure all properties for the package.
5. In the **Installation User Interface Options** section, select one of the following:
    - **Basic**. Use this option to provide only a basic display for users during all package installation in the GPO.
    - **Maximum**. Use this option to provide all installation messages and screens for users during the installation of all packages in the GPO.
6. Click the **Advanced** tab, as shown in Figure 9-2, and select any of the following options to apply the options to all packages in the GPO:

![](img/a8ee53dbf1310726255b6fbb9f296fb2_228_0.png)

    - **Uninstall The Applications When They Fall Out Of The Scope Of Management.** Use this option to remove the application when it no longer applies to users or computers.
    - **Include OLE Information When Deploying Applications.** Use this option to specify whether to deploy information about Component Object Model (COM) components with the package.
    - **Make 32-Bit X86 Windows Installer Applications Available To Win64 Machines.** Use this option to specify whether 32-bit Windows Installer Applications (.msi files) can be assigned or published to 64-bit computers.
    - **Make 32-Bit X86 Down-Level (ZAP) Applications Available To Win64 Machines.** Use this option to specify whether 32-bit application files (.zap files) can be assigned or published to 64-bit computers.
7. In the **Application Precedence** list box, move the application with the highest precedence to the top of the list using the Up or Down buttons. The application at the top of the list is automatically installed if the user invokes a document with the related filename extension and the application has not yet been installed.
8. Click the **Categories** tab, and then click **Add**. The Enter new category dialog box is displayed, as shown in Figure 9-3.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_228_1.png)

9. Key the name of the application category to be used for the domain in the Category box, and click **OK**.
10. Click **OK** to save your changes.

**PAUSE. LEAVE** the Group Policy Management Editor open for the next exercise.

You have now configured default Software Installation settings for GPOs in Windows Server 2008 Active Directory.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_229_0.png)

![](img/a8ee53dbf1310726255b6fbb9f296fb2_229_1.png)

> **TAKE NOTE**
>
> The application categories that you establish are per domain, not per GPO. You need to define them only once for the whole domain, not once for each GPO.

## CREATE A NEW SOFTWARE INSTALLATION PACKAGE

**GET READY.** To create a new Windows Installer package within a GPO, complete the following steps:

1. **OPEN** the Group Policy Management Editor for the GPO you wish to configure. In the Computer Configuration or User Configuration node, drill down to Policies and then Software Settings.
2. Right-click the **Software Installation** node, select **New**, and then click **Package**. The Open dialog box is displayed.
3. In the File Name list, key the UNC path to the software distribution point for the Windows Installer packages (`.msi` files), and then click **Open**. The UNC path is very important. If you do not use a UNC path to the software distribution point, clients will not be able to find the package files.
4. As shown in the Deploy Software dialog box in Figure 9-4, select one of the following:
    - **Published**. Use this option to publish the Windows Installer package to users, without applying modifications to the package. It is only available if the policy was configured under the User Configuration node of Group Policy. Publishing cannot occur in a computer-based policy.
    - **Assigned**. Use this option to assign the Windows Installer package to users or computers, without applying modifications to the package.
    - **Advanced**. Use this option to set properties for the Windows Installer package, including published or assigned options and modifications.
5. Click **OK** and then choose from the following options:
    - If you selected Published or Assigned, the Windows Installer package has been successfully added to the GPO and appears in the Details pane.
    - If you selected Advanced, the Properties dialog box for the Windows Installer package opens to permit you to set properties for the Windows Installer package, including deployment options and modifications. Make the necessary modification and click **OK**.

**PAUSE. LEAVE** the Group Policy Management Editor open for later exercises.

You have now created a Software Installation package within Active Directory Group Policy.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_229_2.png)

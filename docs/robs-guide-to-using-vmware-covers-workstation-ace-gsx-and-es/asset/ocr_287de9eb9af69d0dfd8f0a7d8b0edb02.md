# Table 5.3: Overview of files inside a VMware ACE Package.

| File or Path | Description |
|---|---|
| autorun.inf | When a user inserts a removable medium into a device such as a CD-ROM player, the installation defined in this file will start. |
| app.vmpl, config.ini and preferences.ini | These files contain information needed for encrypting the virtual machine at deployment time. |
| instmsiw.exe | This is the installation package for the Microsoft Windows Installer. If it is not already there, it can be installed to perform the installation with the .msi file. |
| package.msi | This is the Microsoft Windows Installer package to install the VMware ACE package. |
| setup.exe | This file can be used to start the installation of the package manually. |
| VMware ACE.msi | This is the Microsoft Windows Installer package for the VMware ACE runtime environment. |
| Project (directory) | Contains any custom scripts needed for the virtual machine. |
| Virtual machine directory | A directory with all the virtual machine's files. |

The New Package Wizard will guide you through the process of creating the deployment package. Start the wizard from the Project menu, or click the link Create package for distribution to end users in the project's main window. Perform the following steps to create the package:

+   1. Provide a name for the package and enter the location for the new package. You can also provide some descriptive text for the end user to see when he or she executes the package.
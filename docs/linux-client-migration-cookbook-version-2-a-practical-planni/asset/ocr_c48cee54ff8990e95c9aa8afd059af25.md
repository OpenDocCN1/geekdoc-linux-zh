# Progression Desktop

Application Settings Destinations

Please select the applications whose settings you wish to apply. You can use the drop down menu to select an appropriate destination for applications that can be applied to multiple destinations.

If you do not wish to migrate an application, you may select the "Do Not Migrate" option for that application.

AOL

AOL Instant Messenger

GAIM

Microsoft

MSN Messenger

Kopete

Microsoft Excel

OpenOffice.org Calc

Microsoft Outlook

Evolution

Microsoft PowerPoint

OpenOffice.org Imp

Go Back

Continue

![](bbox=[0.273, 0.083, 0.833, 0.493])

C-33 Progression Desktop applying settings to Linux

Performing a migration using the GUI is the simplest approach. However, because this approach requires installing Progression Desktop on each machine (either off of the CD or a network share), this option does not scale well to large environments. This approach is probably best suited for migrations of smaller groups of systems (ten to twenty). For larger groups, you should consider the other approaches.

# Command line (with templates)

Templates are defined policies, which tell the Progression Desktop engine what items are are to be saved from the Windows machine and what items are to be applied to the new Linux machine. Templates are used as part of an automated migration processes without having to step through the Progression user interface each time you want to perform a migration on a specific machine. Templates are simple XML files, which can be created by editing the default templates provided, or by capturing a temporary template that is created during a migration with the GUI.

Once the template has been created, a simple batch file or shell script can create, which installs Progression Desktop automatically and then runs it
# Extra

To provide the compatibility functions, the .NET Framework includes the Microsoft.VisualBasic.Compatibility namespace when using the Upgrade Wizard. This namespace includes functions that exist in the Visual Basic 6 language. The .NET Framework duplicates much of the functions built into Visual Basic 6, making many functions in the language unnecessary. To make the upgrade process as simple as possible, these functions provide the same interfaces as VB 6 functions while remaining compliant with .NET managed code. For example, VB .NET does not include the ability to create control arrays. So for VB 6 projects to upgrade successfully, the compatibility library includes control arrays for each of the basic controls in the language. VB .NET also removes controls like the FileListBox and DriveListBox completely. The compatibility library provides these controls for use with upgraded projects. A number of removed functions like SendKeys also exist within this namespace.

You can use Visual Basic 6 to continue maintaining existing applications instead of upgrading. Both Visual Basic 6 and Visual Basic .NET can coexist on a single system. If you maintain a very large product that functions well in VB 6, you may want to leave your application in VB 6. You may find the upgrade process difficult due to the number of fundamental changes in the language.

![](bbox=[0.07, 0.52, 0.42, 0.82])

![](bbox=[0.52, 0.52, 0.95, 0.82])

You can click Browse to change the directory for the upgraded project.

5 Click Next.

Step 4 appears and notifies you that the wizard finished gathering all necessary information.

6 Click Next on step 4 of the wizard.

The wizard processes the project.

The wizard opens the new project.

Double-click the UpgradeReport.htm file in the Solution Explorer to see errors.
addition, Microsoft recommends adding administrators to the Schema Admins group only for the duration of the task. Also, be sure to test any modifications in an isolated environment that closely matches your actual production environment before releasing the changes to the production network. Planning modifications can sometimes delay the deployment of a desired application or feature, but it is well worth the effort if something does not function as designed in the test environment. You may want to institute a change management process (CMP) infrastructure prior to beginning modifications. The CMP will permit you to track exactly which changes were made to the schema and who made those changes.

# INSTALLING THE SCHEMA MANAGEMENT SNAP-IN

As discussed, some commercial applications such as Microsoft Exchange will modify the schema as a part of their installation process. You can also extend the schema manually using the Active Directory Schema snap-in. To modify the schema manually, you must meet the following requirements:

+   • You must be a member of the Schema Admins group.
+   
+   • The Active Directory Schema snap-in should be installed on the domain controller holding the Schema Master Operations role.

# INSTALL THE SCHEMA MANAGEMENT SNAP-IN

**GET READY.** Before you begin these steps, you must be logged on as a member of the Schema Admins group.

> The Schema Management snap-in is not installed by default in Windows Server 2008. To enable any edits of the Active Directory schema, it is necessary to have the snap-in available. Adding the Active Directory Schema snap-in to a Microsoft Management Console (MMC) window is the simplest way to modify the schema. The MMC is a graphic tool similar to other tools included with Windows Server 2008. It allows you to customize a set of tools you wish to have available for easy management.

+   1. From a command prompt, key `regsrv32 schmmgmt.dll` to register the necessary DLL file needed to run the Active Directory Schema MMC snap-in.
+   
+   2. Close the Command Prompt window, click **Start**, and then select **Run**.
+   
+   3. Key `mmc/a` in the dialog box and click **OK**.
+   
+   4. Click the **File** menu and select **Add/Remove Snap-in**.
+   
+   5. Click **Add** to see the list of available snap-ins.
+   
+   6. Double-click **Active Directory Schema** in the list.
+   
+   7. Click **OK**.
+   
+   8. If you want to save this console for future use, click **File** and then click **Save**. By adding this step, you can simply open the console or create a shortcut on your desktop for easy accessibility.

**PAUSE.** The Schema Management snap-in has been installed.

In the previous exercise, you added the Schema Management snap-in by registering the associated DLL file. This DLL is not registered by default in Windows Server 2008 and needs to be added manually to run the Schema Management MMC snap-in.

> When performing administrative tasks, you should not log on to the console of a domain controller. Instead, it is recommended that administrative tasks be performed from an administrative workstation running Windows XP or Windows Vista, using a normal user account and the **Run As** program. Details on the Run As program and the security issues surrounding this warning are explained further in Lesson 6.
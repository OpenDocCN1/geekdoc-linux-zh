In addition, the Trusted Publisher Properties dialog box lets you decide if you wish to verify that a certificate has not been revoked. If a certificate has been revoked, the user should not be allowed to gain access to network resources. You have the option of checking either the Publisher or the Timestamp of the certificate to determine if it has been revoked.

Software restriction policies can be an asset to your organization’s security strategy when they are understood and implemented properly. Planning how you want to use software restriction policies is your best defense in preventing problems. Microsoft has several recommendations that can help you to plan and implement software restriction policies, including the following:

+   Combining these two security features allows you to have tighter control over program usage.
+   
+   - Software restriction policies should be used with standard access control permissions.
+   
+   - The Disallowed Default Security Level should be used cautiously, because all applications will be restricted unless explicitly allowed.
+   
+   - If policies that cause undesirable restrictions on a workstation are applied, reboot the computer in Safe mode to troubleshoot and make changes, because software restriction policies cannot be applied in Safe mode. Rebooting in Safe mode is a temporary solution, because the policies remain in effect until they are modified or removed.
+   
+   - When editing software restriction policies, you should disable the policy so that a partially complete policy does not cause undesirable results on a computer. After the policy modifications have been made, the policy can be enabled and refreshed.
+   
+   - Creating a separate GPO for software restriction policies allows you to disable or remove them without affecting other policy settings.
+   
+   - Test all policies before deploying them to the users. Very restrictive policies can cause problems with files that are required for the operating system to function properly.

# SUMMARY SKILL MATRIX

> **IN THIS LESSON YOU LEARNED:**
> 
> - Group Policy can be used to deploy new software on your network and remove or repair software originally deployed by a GPO from your network. This functionality is provided by the Windows Installer service within the Software Installation extension of either the User Configuration\Policies\Software Settings or Computer Configuration\Policies\Software Settings node.
> 
> - Three types of package files are used with the Windows Installer service: .msi files for standard software installation, .mst files for customized software installation, and .msp files for patching .msi files at the time of deployment. All pertinent files must reside in the same file system directory.
> 
> - A .zap file can be written to allow non-Windows Installer-compliant applications to be deployed. A .zap file does not support automatic repair, customized installations, or automatic software removal. In addition, these files must be published.
> 
> - A shared folder named a software distribution point must be created to store application installation and package files that are to be deployed using Group Policy. Users must have the NTFS Read permission to this folder for software installation policies to function.
> 
> - Software to be deployed using Group Policy can either be Assigned or Published. Assigning software using the User Configuration node of a Group Policy allows the application to be installed when the user accesses the program using the Start menu or an associated file. Assigning software can also be performed using the Computer Configuration node of a Group Policy, which forces the application to be installed during computer startup. Publishing an application allows the application to be available through Add Or Remove Programs in Control Panel. In addition, published applications can be divided into domain-wide software categories for ease of use.
# What is the difference between the passwords?

Your current administrator account and password is for the Enterprise administrator group. You use this account on domain controllers. Because you are uninstalling the Active Directory, the administrator account is returned to a local standalone server account. The first password you are prompted for checks your account and permission to perform the uninstall. The second password box in the wizard asks you to assign a new password to the local standalone server administrator account.

# If I reinstall the Active Directory after an initial uninstall, is the Active Directory data still current?

When you reinstall the Active Directory, or even install the Active Directory for the first time, the data, such as objects, are replicated from other domain controllers (assuming they exist). For example, all user accounts and other objects are replicated to the new domain controller automatically. You are not required to configure the data of each domain controller individually.

![](bbox=[0.01, 0.51, 0.48, 0.81])

+   8. Type an account username and password with Enterprise Administrator privileges.
+   9. Click Next to continue.

![](bbox=[0.5, 0.51, 0.96, 0.81])

+   10. Type the administrator password for the standalone server's administrator account.
+   11. Retype the password for confirmation.
+   12. Click Next to continue.
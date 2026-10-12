The **Yum package manager** allows for an automatic verification of all packages it installs or upgrades. This feature is enabled by default. To configure this option on your system, make sure the `gpgcheck` configuration directive is set to **1** in the `/etc/yum.conf` configuration file.

Use the following command to manually verify package files on your filesystem:

```
rpmkeys --checksig package_file.rpm
```

See the Product Signing (GPG Keys) article on the Red Hat Customer Portal for additional information about Red Hat package-signing practices.

# 3.1.2.2. Installing Signed Packages

To install verified packages (see Section 3.1.2.1, “Verifying Signed Packages” for information on how to verify packages) from your filesystem, use the `yum install` command as the **root** user as follows:

```
yum install package_file.rpm
```

Use a shell glob to install several packages at once. For example, the following commands installs all `.rpm` packages in the current directory:

```
yum install *.rpm
```

> **IMPORTANT**
> 
> Before installing any security errata, be sure to read any special instructions contained in the erratum report and execute them accordingly. See Section 3.1.3, “Applying Changes Introduced by Installed Updates” for general instructions about applying changes made by errata updates.

# 3.1.3. Applying Changes Introduced by Installed Updates

After downloading and installing security errata and updates, it is important to halt the usage of the old software and begin using the new software. How this is done depends on the type of software that has been updated. The following list itemizes the general categories of software and provides instructions for using updated versions after a package upgrade.

> **NOTE**
> 
> In general, rebooting the system is the surest way to ensure that the latest version of a software package is used; however, this option is not always required, nor is it always available to the system administrator.

# Applications

User-space applications are any programs that can be initiated by the user. Typically, such applications are used only when the user, a script, or an automated task utility launch them.

Once such a user-space application is updated, halt any instances of the application on the system, and launch the program again to use the updated version.

# Kernel
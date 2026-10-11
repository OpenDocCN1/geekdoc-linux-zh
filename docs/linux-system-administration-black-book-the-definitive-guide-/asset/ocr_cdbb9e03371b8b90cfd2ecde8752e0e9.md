# # Immediate Solutions

# ## Installing The First Machine

To install the initial machine in a way that makes your KickStart build process easiest, do the following:

+   - If at all possible, do a network installation using NFS as the file server. Those who are not using NFS may want to have multiple copies of the Red Hat installation CD-ROM available, because otherwise you'll be able to do only one install at a time.
+   - Choose a Custom-class installation, which ensures that you will have the least amount of tweaking to do later.
+   - If you intend to use DHCP to provide network information to these machines, set up the DHCP server before you install the prototype.
+   - Go through the trouble of choosing Select Individual Packages when it is time to choose package groups. Doing this allows you to micromanage exactly what programs are placed on the machine. You will not have to go back afterward and remove the items that will not be used during a security sweep later.

**TIP:** Don't worry about accidentally deleting packages that are necessary to satisfy installation dependencies. The installer double-checks this before proceeding and allows you to turn on the option to install the missing dependencies.

+   - If you want to offer multiple video modes to your users, customize the X configuration during the install.

Now, continue to the section "Cloning Machine Configurations."

**NOTE:** If you intend to use the %post section to add configuration items to the KickStart file, you should still follow this procedure.

| Related solutions: | Found on page: |
| :--- | :--- |
| Setting Up A DHCP Server | 213 |
| Setting Up NFS Exports | 505 |
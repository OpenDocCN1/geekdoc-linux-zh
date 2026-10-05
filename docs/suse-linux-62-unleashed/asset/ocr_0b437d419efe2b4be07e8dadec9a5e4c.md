# Starting and Configuring VMware

After you choose your configuration, the script installs the VMware software under /usr/local/bin directory, and exits. In order to run VMware, you must have a license file from VMware, Inc. This license may be obtained by registering at the VMware home page, and will be emailed to you. When you receive the license, save the email message as a text file license.

Next, use the mkdir command to create a directory in your home directory named .vmware, then copy the license into the .vmware directory like this:

```
# mkdir .vmware ; cp license .vmware
```

To first start VMware, type vmware at the command line of your terminal window. (You do not need to be logged in as the root operator, but you will need read and write permission for the device /dev/zero). The VMware configuration window and configuration dialog box appears, as shown in Figure 29.3.

![](bbox=[0.205, 0.373, 0.795, 0.608])

The OK button to continue. You'll then see the Configuration Wizard screen, as shown in Figure 29.4.

To start your configuration, click the Next button. Throughout the configuration process, you can step forward or backward to change settings. The next screen, shown in Figure 29.5, asks you to select the Guest Operating System. Note that you can even install another Linux distribution, or if you click Other, another UNIX variant, such as FreeBSD.

VMware can be used to install and run other operating systems on your computer. It is possible to install and run multiple operating systems at the same time on a single computer, and to network the different operating systems. I guess this would be called a "LAN-in-a-box?
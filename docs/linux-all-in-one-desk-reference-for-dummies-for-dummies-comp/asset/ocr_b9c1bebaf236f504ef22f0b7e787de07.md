![](bbox=[0.13, 0.13, 0.2, 0.24])

For Fedora Core, you have to download Nessus from www.nessus.org/download/ and install it. Before you try to install Nessus, you must install the sharutils RPM. That package includes the uudecode utility that the Nessus installation script needs. The sharutils package isn't installed with any of the standard package groups in Fedora Core, so you have to install it yourself. To install sharutils, mount the companion DVD and install it with the following commands:

```
cd /media/cdrom/Fedora/RPMS
rpm -ivh sharutils*.rpm
```

To download and install Nessus, follow these steps. (These instructions work on all Linux distributions.)

+   1. At www.nessus.org/download, select the version of Nessus you want to download. For Linux systems, download the Nessus 2.2.5 installer.
+   2. Type the following command to install Nessus. (You must have the development tools, including The GIMP Toolkit, installed.)
+   sh nessus-installer-2.2.5.sh
+   
+   Respond to the prompts from the installer script to finish the installation. You can usually press Enter to accept the default choices.

After the installation completes, follow these steps to use Nessus. (In Knoppix, choose Main Menu→System→Security→NESSUS Security Tool, and then go to Step 8.)

+   1. Log in as root and type the following command to create the Nessus SSL certificate used for secure communication between the Nessus client and the Nessus server:
+   essus-mkcert
+   2. Provide the requested information to complete the certificate generation process.
+   3. Create a nessusd account with the following command:
+   essusd-adduser
+   4. When prompted, enter your username, password, and any rules. (Press Ctrl+D if you don't know what rules to enter.) Then press the Y key.
+   5. If you want to, you can configure nessusd by editing the configuration file /usr/local/etc/nessus/nessusd.conf.
+   
+   If you want to try out Nessus, you can proceed with the default configuration file.
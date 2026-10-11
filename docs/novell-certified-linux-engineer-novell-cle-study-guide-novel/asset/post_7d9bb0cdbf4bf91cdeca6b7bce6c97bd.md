
With that, your system is now ready for an NNLS installation. Let's do that in Lab Exercise 5.3.

## Lab Exercise 5.3: Installing NNLS

In this exercise, you will install NNLS. If you haven't completed Exercises 5.1 and 5.2, complete those before attempting this exercise.

To install NNLS, complete the following:

1. Install NNLS using a custom install by completing the following steps:
   - a. Verify that the current directory is /media/iso.
   - b. At the shell prompt, enter . /install.sh.
   - c. When prompted, enter i to install.
   - d. When prompted to use an Express install, type no.
   - e. You are now prompted to select the NNLS components you want to install. In this book, we're going to install everything up front. Then, as you progress through the remaining chapters, you will configure each product. Enter a to select all products.
   - f. Enter f to finish making selections.
   - g. In the License Agreement screen, press the spacebar until you are prompted to agree to the license agreement.
   - h. When prompted to agree to the license, enter y.

2. Provide eDirectory NNLS installation parameters by completing the following:
   - a. When prompted for the location of the NICI file, enter /media/floppy/file_name.nfk.
   - b. When prompted, enter 1 to create a new eDirectory tree.
   - c. When prompted for the tree name, enter CLE-TREE.
   - d. When prompted for the eDirectory port, press Enter.
   - e. When prompted for the admin name and context, enter cn=admin.ou=1f.o=CLE.
   - f. When prompted to enter the admin user's password, enter novell.
   - g. When prompted for a server context, press **Enter**.
   - h. When prompted for the LDAP port number, press **Enter**.
   - i. When prompted for the secure LDAP port number, press **Enter**.
   - j. When prompted for the iMonitor HTTP port, press **Enter**.
   - k. When prompted for the iMonitor secure HTTP port, press **Enter**.

**WARNING** Be sure to use a different password for your admin user when you deploy NNLS in a production environment. You would be surprised how many eDirectory admin user objects are out there in corporate environments that have a password of *novell*.

3. Configure the LUM component of NNLS by completing the following:
   - a. When prompted for the LDAP server IP address, enter your server's IP address.
   - b. When prompted for the admin name and context, press **Enter**.
   - c. When prompted for the admin user's password, press **Enter**.
   - d. When prompted for the LDAP port, press **Enter**.
   - e. When prompted for the secure LDAP port, press **Enter**.
   - f. When prompted for the partition root, press **Enter**.
   - g. When prompted for the workstation context, press **Enter**.
   - h. When prompted to select services that will use eDirectory for authentication, enter **a** to select all of them; then enter **f**.

**TIP** Notice that the NNLS installation script remembers previously entered values for other components and automatically uses them for the default values for other NNLS components. You can use these defaults by simply pressing **Enter**.

4. Configure DirXML parameters by completing the following:
   - a. When prompted to supply the eDirectory server's IP address, press **Enter**.
   - b. When prompted for the admin user's name and context, press **Enter**.
   - c. When prompted for the admin user's password, enter **novell**.
   - d. When prompted for the secure LDAP port, press **Enter**.

5. Configure eGuide by completing the following:
   - a. When prompted for the LDAP server's IP address, enter your server's IP address.
   - b. When prompted for the LDAP server's port, press **Enter**.
   - c. When prompted for the secure LDAP port, press **Enter**.
   - d. When prompted for the LDAP admin username and context, press **Enter**.
   - e. When prompted for the admin user's password, enter **novell**.

6. Configure Samba by completing the following:
   - a. When prompted to supply the eDirectory server's IP address, press **Enter**.
   - b. When prompted for the admin user's name and context, press **Enter**.
   - c. When prompted for the admin user's password, enter **novell**.
   - d. When prompted for the LDAP server's IP address, press **Enter**.
   - e. When prompted for the Samba Proxy username, press **Enter**.
   - f. When prompted for the Samba Proxy user's password, enter **novell**.
   - g. When prompted for the LDAP server's port, press **Enter**.
   - h. When prompted for the secure LDAP port, press **Enter**.
   - i. If prompted to remove existing Samba packages, press **Enter**.

7. Configure iFolder by completing the following:
   - a. When prompted for the LDAP server's IP address, press **Enter**.
   - b. When prompted for the LDAP server's port, press **Enter**.
   - c. When prompted for the LDAP admin username and context, press **Enter**.
   - d. When prompted for the admin user's password, enter **novell**.
   - e. When prompted for the IP address of the iFolder server, enter your server's IP address.
   - f. When prompted to enter iFolder admin usernames, press **Enter**.
   - g. When prompted to supply the iFolder user data path, press **Enter**.

8. Configure NetMail by completing the following:
   - a. When prompted to supply the admin username and context, press **Enter**.
   - b. When prompted to supply the admin user's password, enter **novell**.
   - c. When prompted to supply the NetMail DNS server address, enter your server's IP address.
   - d. When prompted to supply the NetMail secondary DNS server address, enter your organization's secondary DNS server address, if it exists. This parameter is optional.
   - e. When prompted for your NetMail domain, press **Enter**.
   - f. When prompted for your WebAccess HTTP port, press **Enter**.
   - g. When prompted for your WebAccess secure HTTP port, press **Enter**.
   - h. When prompted for your NetMail LDAP port, press **Enter**.
   - i. When prompted for the IP address of the server where iManager will be installed, enter your server's IP address.
   - j. When prompted for the admin user's name and context, press **Enter**.
   - k. When prompted for the admin user's password, enter **novell**.
   - l. When prompted to supply the eDirectory server's IP address, enter your server's IP address.
   - m. When prompted for the LDAP server's port, press **Enter**.
   - n. When prompted for the iManager WebAdmin HTTP port, press **Enter**.
   - o. When prompted for the iManager WebAdmin secure HTTP port, press **Enter**.

9. Configure iPrint by completing the following:
   - a. When prompted for your eDirectory tree name, press **Enter**.
   - b. When prompted for the admin user's name and context, press **Enter**.
   - c. When prompted for the admin user's password, enter **novell**.
   - d. When prompted to supply the eDirectory server's IP address, enter your server's IP address.

10. Configure Virtual Office by completing the following:
    - a. When prompted to supply the eDirectory server's IP address, enter your server's IP address.
    - b. When prompted for the admin user's name and context, press `Enter`.
    - c. When prompted for the admin user's password, enter `novell`.
    - d. When prompted for the NetStorage authentication domain host, press `Enter`.
    - e. When prompted for the NetStorage proxy username and context, press `Enter`.
    - f. When prompted for the NetStorage proxy user's password, enter `novell`.
    - g. When prompted for the users context, enter `o=CLE`.
    
    > Be careful on the preceding step. You've been pressing Enter for so many parameters, it's easy to accidentally press it on this step.
    
    - h. When prompted for the iFolder server's IP address, press `Enter`.

11. Configure Red Carpet by completing the following:
    - a. When prompted for the Red Carpet administrator's email address, enter your email address. If you want to use the NetMail account for your admin user object, you could enter `admin@cle.com`.
    - b. When prompted, specify whether or not your server uses a proxy server.

12. Finish the installation by completing the following:
    - a. When prompted to view the installation summary information, press `Enter`.
    - b. If you need to make any changes, enter `yes` and make the necessary changes. If you're satisfied with the current settings, enter `no`.

13. Wait while NNLS is installed. This can take up to 15 minutes.

14. When the installation is complete, you are prompted to view the readme file. Enter `y` to view it.

15. When prompted to save the installation settings to a file, enter `y`.

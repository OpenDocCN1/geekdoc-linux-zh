# # Installing CentOS

The first screen you see is the Welcome screen. Click Forward to step through each procedure as follows:

+   *   **Firewall** — Firewall settings allow or deny access to the services running on your CentOS system to other computers on your network.
+   
+   *   **SELinux** — SELinux is an additional layer of security that provides finer-grained security controls than the traditional access permission scheme. The default setting on CentOS is that SELinux security is enforced.
+   
+   *   **Date and Time** — Set the date and time, or enable the network time protocol to keep your system clock properly set. Click Forward.
+   
+   *   **Create User** — For your daily use of CentOS, you should have your own user account. You should typically log in with this username (of your choosing) and use only the *root* user to perform administrative tasks. In the first of the four textboxes on the screen, type a username (e.g., `dmiller` or `mjohnson`). Next, type your full name (e.g., `Devlin Miller` and `Mel Johnson`). Then type your password in the Password textbox and again in the “Confirm Password” textbox. Click Forward.
+   
+       If some form of network authentication is used, such as LDAP, Kerberos, or SMB authentication, you can click on the Use Network Login button. See the “Enabling Authentication” sidebar for information on choosing different authentication types.
+   
+   *   **Sound Card** — This stage lets you test your system’s sound card settings. Click Forward.
+   
+   *   **Additional CDs** — Specify any additional installation CDs or DVDs that you have to install more software.

Firstboot is complete. Click Finish to continue. You may need to reboot. See Chapter 3 for a description of how to log in to CentOS and start learning how to use Linux.

When CentOS starts up the next time, it will boot up normally to a login prompt. A graphical boot screen is displayed (instead of a scrolling list of services starting up).

# # Enabling Authentication

In most situations, you will enable shadow passwords and MD5 passwords (as selected by default) to authenticate users who log in to your computer from local password and shadow password files. To change that behavior, you can select the “Use Network Login” button during the Create User setup during Firstboot.

The shadow password file prevents access to encrypted passwords. MD5 is an algorithm used to encrypt passwords in Linux and other UNIX systems. It replaces an algorithm called *crypt*, which was used with early UNIX systems. When you enable MD5 passwords, your users can have longer passwords that are harder to break than those encrypted with *crypt*. You can also use SHA512 or SHA256 for encrypting passwords.
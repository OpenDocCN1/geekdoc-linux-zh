# Making the Switch

Postfix is easy to install and configure. The first thing to do is to make a backup of all your Sendmail information that you want to keep, just in case. After you have done this, you need to use `ym` to remove `Sendmail` and install Postfix.

After Postfix has been successfully installed, you can begin configuring it. The scripts for Postfix are all located in `/etc/postfix` and include

+   
+   1.  **install.cf**—The script generated when Postfix is installed. This file lists the locations Postfix uses and can be a big help when working with the **main.cf** file.
+   2.  **main.cf**—The principal configuration script for Postfix. Within the remarks at the start of the script, you are advised to change only a couple of options at any time. This is sage advice, given that there are more than 300 possibilities!
+   3.  **master.cf**—The throttle control for Postfix. This script enables you to change settings for Postfix that directly affect the speed at which it works. Unless you have a reason to tinker with this file, leave it alone. Trust me: You will know when you need to make changes.
+   4.  **postfix-script**—The script used by Postfix as a wrapper. You cannot execute it directly; instead it is called by Postfix itself.

You can keep your original Sendmail aliases file for use with Postfix because it will not make much difference to it.

You will also require the services of `system-switch-mail`, which can also be installed by using `yum`.

After `system-switch-mail` has been successfully installed, switch to a root terminal and type the following:

```
# system-switch-mail
```

You are then greeted with a simple text screen, asking which MTA you want to use. Select Postfix and simply press Enter. After a few seconds, a new window appears, informing you that your MTA has been successfully switched. All you then need to do is ensure that Postfix is enabled in runlevel 5 by checking the service (`system-config-services`).

Further configuration of Postfix focuses on the **main.cf** file, which is extensively documented throughout the file using comments.

The beauty of Postfix is that it can be used in any situation from a single home user to a large corporation that has thousands of clients, even up to the ISP level. It can even be linked to MySQL for authentication purposes and virtual hosting.
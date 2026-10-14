
![](img/3137cdda7122042e86dbeafe9840d4ed_314_0.png)

## Figure 13-8: The Linuxconf menu

![](img/3137cdda7122042e86dbeafe9840d4ed_314_1.png)

## Figure 13-9: Configuring name server settings

## SPECIFYING THE NAME SERVER

The illustration shown in Figure 13-9 shows the options for configuring the name server settings of your Internet (PPP) connection. Plug in the values provided by your ISP (not the sample values shown in the illustration) and choose “Accept.”

![](img/3137cdda7122042e86dbeafe9840d4ed_315_0.png)

## CONFIGURING PPP

If you need to modify your PPP setup, use the screen shown in Figure 13-10. Configuring a PPP connection is covered in more detail in Chapter 3, “Connecting to the Internet.”

### Figure 13-10: Modifying your PPP setup

![](img/3137cdda7122042e86dbeafe9840d4ed_315_1.png)

## SETTING APACHE WEB SERVER OPTIONS

The Apache Web server comes preconfigured, so your Web site can be up and running as soon as you put your HTML files in the /home/httpd/html directory. If you want to tweak any of the Apache settings, use the screen shown in Figure 13-11.

### Figure 13-11: Tweaking Apache settings

## SETTING FTP SERVER OPTIONS

If you plan to allow Internet users to access files on your machine via FTP connections, use the screen shown in Figure 13-12 to configure the FTP server options.

![](img/3137cdda7122042e86dbeafe9840d4ed_316_0.png)

### Figure 13-12: Configuring FTP

## ADDING NEW USERS

Use the screen shown in Figure 13-13 to add new users to your system. Only the "Login name" field is mandatory, but it's a good idea to fill in the "Full name" field as well, so you can remember the real names of your users. If the new users want a command shell other than Bash, select it from the "Command interpreter" list. After you press the "Accept" button, you will be prompted to enter the initial password for the new account.

![](img/3137cdda7122042e86dbeafe9840d4ed_316_1.png)

### Figure 13-13: Adding new users

![](img/3137cdda7122042e86dbeafe9840d4ed_317_0.png)

## CHANGING THE ROOT PASSWORD

If you need to change the password for the root user, use the screen shown in Figure 13-14. Enter root's old password in the input box and press “Accept,” and then you'll be prompted to enter and confirm the new password.

### Figure 13-14: Changing the password for the root user

![](img/3137cdda7122042e86dbeafe9840d4ed_317_1.png)

## EMAIL ALIASES

If you'd like to route incoming mail for a certain user to an alternative inbox, use the screen shown in Figure 13-15. In the example shown, mail addressed to postmaster will be delivered to root instead. You can enter more than one address in the lower panel if you want mail rerouted to multiple users.

### Figure 13-15: Routing incoming mail

![](img/3137cdda7122042e86dbeafe9840d4ed_318_0.png)

## SETTING UP LOCAL DRIVES

Use the screen shown in Figure 13-16 to modify, add, or delete drives or partition mounts. Double-click an item to modify the mount parameters.

### Figure 13-16: Accessing local volume and volume specification

![](img/3137cdda7122042e86dbeafe9840d4ed_318_1.png)

## SETTING THE SYSTEM RUNLEVEL

The system runlevel settings control whether your system boots up in single-user mode (level 1), text mode (level 3), or graphical mode (level 5). Single-user mode boots with a minimal set of essential drivers and is typically used only in cases of emergency, similar to the Safe Mode of Windows 95/98. (Runlevels 2 and 4 are not used.)

### Figure 13-17: Adjusting runlevel settings

![](img/3137cdda7122042e86dbeafe9840d4ed_319_0.png)

## CONFIGURING LILO

If you want to change any of the LILO settings, use the screen shown in Figure 13-18. If your computer accesses a hard drive in LBA mode, make sure the “Use linear mode” box is checked. You can change the LILO boot prompt timeout from the default of five seconds. Setting the timeout to zero tells LILO to wait indefinitely for user input, instead of booting the default system after the time delay. The dialog box shown here shows how to select the operating system LILO starts by default if you have a nonzero timeout value.

### Figure 13-18: Changing LILO settings

![](img/3137cdda7122042e86dbeafe9840d4ed_319_1.png)

## SETTING THE SYSTEM CLOCK

Use the screen shown in Figure 13-19 to modify the system date, clock, or time zone.

### Figure 13-19: Modifying date and clock settings

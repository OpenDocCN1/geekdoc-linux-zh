
command to print and the `lpc` command to see a printer queue. Both Postfix and Sendmail have a `newaliases` command and `mailq` commands for updating aliases and checking the mail queue, respectively.

So, to the user, a change in mail or printing services should (in theory) be nearly invisible. Users can print documents using the same commands they always used and the documents will be printed. Users can send mail as they always did and the fact that a different mail transport is being used should make no difference.

## Getting Linux Software "up2date"

The `up2date` facility is the preferred method from Red Hat, Inc. for updating Fedora and Red Hat Enterprise Linux software. Using `up2date`, you can determine if any software packages in your Linux distribution have updates available, and you can ask to have them downloaded and installed automatically.

Fixes and improvements continue after a distribution, such as Fedora Core or Red Hat Enterprise Linux, is released. You can incorporate those fixes and features into Red Hat Linux, using a connection to the Internet and `up2date`.

This section tells you how to determine which updates are available to your Red Hat Linux system. Then it describes how you can register to use the Red Hat Network and use the `up2date` tool to gather those updates.

> **NOTE:** The `up2date` service is used for getting fixes to your Red Hat Linux system. It is not used to pick up every change that occurs to the software packages included with Red Hat Linux.

With the transition from Red Hat Linux to Fedora and Red Hat Enterprise Linux, changes in what `up2date` supports are among the most significant changes to the latest distributions from Red Hat. In particular, `up2date` has been modified to allow you to not only download software from Red Hat FTP sites, but also from repositories of software built to work with the `apt` and `yum` facilities.

> **CROSS REFERENCE:** For detailed descriptions of `apt` and `yum`, refer to Chapter 5.

## Getting updates from the Red Hat Network

Red Hat has created a system that automatically notifies you of available updates and lets you easily download and install them on your Red Hat Linux system. The service is called Red Hat Network. Registering with the Red Hat Network allows you to run the `up2date` program from your Red Hat Linux computer whenever you are ready to do the updates.

Red Hat Network provides a mechanism that can:

- Alert you to the latest fixes and enhancements available for Red Hat Linux.
- Install the packages that include those changes to your system.

A lot of information about the Red Hat Network is available from its Web page (rhn.redhat.com). This section provides an overview of how the service works and steps you through the registration process.

> **NOTE:** If you are using an older Red Hat Linux version, you may need to get a new SSL certificate and new up2date software to get the up2date facility to work. Refer to rhn.redhat.com to get those items.

If you don't mind giving out your e-mail address, street address, and phone number, there are some pretty good reasons for creating a Red Hat Network (RHN) account for yourself. With a free RHN account you can register your Red Hat Linux system and create system profiles. Just registering your first machine also entitles you to receive all updates for that machine. To get more services (or entitle more machines), you can purchase a subscription to RHN. To keep your RHN account, Red Hat is currently asking that you occasionally fill out a survey, describing how you use Red Hat Linux.

> **NOTE:** Because Red Hat Network is fairly new and constantly evolving, it is possible that many of the features and entitlements described in this section will change. I recommend that you check the Red Hat Network site for information on new features if the procedures in this section seem outdated.

### Using the Red Hat Network alert notification tool

To register your system with Red Hat and start the process of getting notifications of updates, you don't have to go further than your desktop. A round icon with an exclamation point in the middle appears on the desktop panel, ready to help you check for critical updates to Red Hat Linux.

> **NOTE:** If the Red Hat Network Alert icon is not on your desktop, you can put it there by selecting the Red Hat menu on your desktop panel, then clicking System Tools → Red Hat Network Alert Icon.

Figure 10-8 shows you what the Red Hat Network Alert icon looks like when updates are available. (If no updates are available, a blue checkmark icon appears instead.)

![](img/27a85d56d393921ced6412ae6e8336bf_407_0.png)

**Figure 10-8:** The Red Hat Network alert notification tool appears as a round icon on your desktop panel.

Click the icon and the Red Hat Network Alert Notification Tool window appears. Follow these steps to begin the process of getting updates:

- 1. From the Red Hat Network Alert Notification Tool window, click Forward. The Terms of Service window appears.
- 2. Read the Terms of Service. Then either click Forward (to continue) or click Remove From Panel (to remove the icon and not use the service). If you continue, the Proxy Configuration window appears.
- 3. If you need to go through a proxy server to get to the Internet for HTTP (Web) service, click Enable HTTP Proxy, identify the location of the proxy server, and then add any authentication information you need to connect to that server. Click Forward to continue.
- 4. On the Configuration Complete window that appears, click Apply. At this point, the red icon turns blue and changes from an exclamation point to a check mark.
- 5. To register with Red Hat Network and check for software updates, proceed to the next section.

## Registering with Red Hat Network

To register your system with Red Hat Network, you can click the blue RHN icon, use the `rhn_register` command or simply look for the Red Hat Network Configuration window to pop up when you run `update`. Using any of these methods requires a connection to the Internet and root access to your computer — the latter because the registration process needs to access your computer’s RPM database. Though only the first computer you register can receive free automatic updates, you can register as many computers as you want with this tool. Here’s how it works:

- 1. From a Terminal window type `rhn_register`. The first time you run this, the Red Hat Network Configuration window appears.
- 2. Select each of the following tabs to fill out basic configuration information:
  - **General** — Select an RHN server to use to get your updates. One should already be entered. If you need to go through an http proxy or provide a user name and password to reach the server, enter that information on this tab as well.
  - **Retrieval / Installation** — Set preferences here related to whether or not packages are immediately installed after they are downloaded and whether or not they are kept on your hard disk or deleted after installation. By default, packages are installed after retrieval, verified using GPG, and the RPMs are removed after they are installed. Packages that have had modifications to configuration files are not upgraded.
  - **Package Exceptions** — By default, any kernel packages are not upgraded. You can add other packages, or even selected files, to skip.
- 3. If you do not have the Red Hat, Inc. public key on your keyring (and you selected to use GPG as is set by default), you are prompted to install the key. Click Yes to install the key. The Welcome to Red Hat Update Agent window appears.
- 4. Click Forward. The Review the Red Hat Privacy Statement window appears.
- 5. Read the explanation of the registration procedure and click Next. The Red Hat Privacy Statement appears. This statement tells you, among other things, how your personal information is used and how Red Hat uses cookies to track activities.
- 6. Read the privacy statement. If it is acceptable, click Forward. The Login window appears.
- 7. Add information to create a user account and click Forward. The information you provide includes:
  - **User name** — Type a name of your choosing.
  - **Password** — Type a password (then type it again in the next box to verify it).
  - **E-mail address** — Type the address at which you would like Red Hat to contact you.

The Register a User Account window appears.

Add the information and click Forward. The next screen asks for some personal information, including name, address, phone number, fax number, and how you would like to be contacted (e-mail, regular mail, phone, fax, or e-newsletter).

- 8. A Register a System Profile-Hardware window appears. This window displays information about your Red Hat Linux version, host name, IP address, CPU mode, CPU speed, and memory.
- 9. Select a profile name (the host name is used by default) or service ID number (which can be the computer's serial number) and click Forward.

The registration process begins building a list of packages installed on your computer. These are gathered so they can become part of your system profile. These packages are then displayed in the Register a System Profile-Packages window.

- 10. Check that the packages that appear in the window are all okay to include in your system profile (unselecting the ones you don't want to include) and click Next. The Send Profile Information to Red Hat Network window appears.
- 11. Click Forward to register the system-profile information with the Red Hat Network. (Or choose not to send the information by clicking Cancel.) Your information is sent and the Registration Finished window appears.
- 12. Click Forward to end the session.

After you have finished registering with Red Hat Network you can go to the RHN site and log in to use the service. You are now also ready to run the `up2date` command to update your software packages.

## Getting Updates

After you have registered your computer with Red Hat Network you can use the `up2date` command (or right-click the notification icon and click Launch up2date) to find and install

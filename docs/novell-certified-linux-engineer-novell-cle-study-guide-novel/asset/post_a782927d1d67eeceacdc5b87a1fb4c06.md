
To configure global client policies, complete the following steps:

1. Open a web browser and navigate to `https://your_server_IP_address/iFolderServer/Admin`.
2. In the iFolder **Welcome** screen, select **Global Settings**.
3. Authenticate as your admin user.
4. Select **Global Policies**.
5. On the **Client Policies** line, select **Display**.
6. Configure your policies.
7. Select **Update Client Policy**.

Global client policies are very useful for establishing a baseline system configuration. It is very likely, however, that there will be users who require a slightly different configuration.

You can accommodate them by configuring a customized set of policies for individual users. Individual user policies override global client policies. To configure an individual user's client policies, complete the following steps:

1. Open a web browser and navigate to `https://your_server_IP_address/iFolderServer/Admin`.
2. In the iFolder **Welcome** screen, select **User Management**.
3. Authenticate as your admin user.
4. In the **Enter Username** field, enter the username you wish to configure a customized policy for.
5. Click **Search**.
6. In the search results, select the user whose policies you want to edit.
7. Scroll down to the **Policy** line, then select **Edit**. The **Policies** screen appears. Notice that, although it appears identical to the **Global Client Policy** screen we worked with previously, the policies displayed only apply to the selected user.
8. Configure your policies.
9. Select **Update Client Policy**.

That's it. Your server is ready to go. Next, you need to install and configure the iFolder client on the Windows workstations in your network.

## Installing and Configuring the iFolder Client

Before we address this task, you need to understand that you don't necessarily have to use the iFolder client. As mentioned earlier, you can opt to simply use the iFolder applet from within a web browser (sorry, it only works with Internet Explorer 5 or later) to access your iFolder files.

If you choose the web browser route, however, your users won't have the benefit of automatic synchronization. They will have to manually download and upload their files. In my opinion, you should deploy the iFolder client to all your users' workstations, including their desktop PCs, their notebook PCs, and even their home computers if they do a lot of work from home.

The web page option should be reserved for emergencies when users need access to their iFolder files from a computer that doesn't have the iFolder client installed. An example of this would be a sales representative visiting a client, and the notebook computer's hard drive crashes.

In this case, the presentation files saved in the iFolder directory are no longer available. Using the web page option, the sales rep can borrow a PC and access the iFolder server over the web without having to install the iFolder client on the borrowed PC.

iFolder can also provide a huge benefit to users on the road. Users can even access their files using an airport kiosk Internet terminal.

The iFolder client can be installed on Windows 98, Windows Me, Windows 2000 Professional, and Windows XP systems. The systems you are going to deploy the iFolder client on must have Internet Explorer 5.0 or later installed.

When you think of installing the iFolder client on all the Windows workstations in your network, it sounds like a daunting task. Novell makes it relatively easy, however, by providing the client software through the iFolder website. You don't have to worry about running a CD around to all your users' workstations.

To install the iFolder client, complete the following steps:

> **NOTE**
> Depending on how you have configured your iFolder global client policies, you may not see some of the options listed in the following steps (such as the Remember Pass Phrase option). These steps are written using the default iFolder policy configuration.

1. On the user workstation, open Internet Explorer and navigate to `https://your_server_IP_address/iFolder`.
2. If prompted, select **Yes** to accept the security certificate. The screen in Figure 8.13 appears.

![](img/c7771e8540507f2b00c088c7a411b57b_362_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_362_1.png)

3. Under **iFolder Windows Client**, click **Download**.
4. In the **File Download** dialog, click **Open**.
5. Wait while the installation file is downloaded and run.
6. In the iFolder **Welcome** screen, click **Next**.
7. In the **License Agreement Language** screen, select your language and then click **Next**.
8. Read the license agreement and then close the browser window.
9. When prompted to accept the license agreement, select **Yes**. The screen in Figure 8.14 is displayed.

**FIGURE 8.14**
The iFolder Choose Destination Location screen.

![](img/c7771e8540507f2b00c088c7a411b57b_363_0.png)

**FIGURE 8.15**
The iFolder Setup Complete screen.

![](img/c7771e8540507f2b00c088c7a411b57b_363_1.png)

10. Select the destination folder for your client installation and then click **Next**.
11. When prompted that the installation is complete, click **Finish**.
12. Read the ReadMe file, then close the Notepad window.
13. When prompted, select **Yes, I Want to Restart My Computer Now**; then click **Finish**.
14. Wait while your workstation reboots. When the system has been restarted, the screen shown in Figure 8.15 is displayed.
15. Click **Continue**. The screen in Figure 8.16 is displayed.

**FIGURE 8.16**
The iFolder Login screen.

![](img/c7771e8540507f2b00c088c7a411b57b_363_2.png)

16. In the User ID field, enter the username of a user in your eDirectory tree.

> You don't need to include the user's context. The iFolder server will search for the user in the contexts you configured previously.

17. In the Password field, enter the user's password.
18. Click Login. The iFolder Location screen appears.
19. The iFolder Location field is automatically populated with the path you specified in your global client policies screen. If you want to use a different directory, enter it here; otherwise, click OK. The screen in Figure 8.17 appears.

![](img/c7771e8540507f2b00c088c7a411b57b_364_0.png)

**FIGURE 8.17**
The iFolder New Internet Folder Setup screen.

20. In the iFolder New Internet Folder Setup screen, mark the following as desired:
    - **Enable automatic login at startup**—This option will automatically authenticate the iFolder client to the iFolder server at start-up using the username and password you supplied. This option works well if the workstation only has one user. If you have multiple users using the same workstation, you may not want to use this option.
    - **Encrypt files**—Selecting this option will encrypt the files on the iFolder server. Unless you have a good reason not to, you should always select this option.
21. Click OK. The screen in Figure 8.18 is displayed.

**FIGURE 8.18**
The iFolder Get Pass Phrase screen.

![](img/c7771e8540507f2b00c088c7a411b57b_365_0.png)

**TIP** The pass phrase is used as an encryption key for encrypting files on the iFolder server.

22. In the iFolder Get Pass Phrase screen, enter a pass phrase for the user account in the Enter pass phrase and Confirm pass phrase fields.
23. In the **Hint** field, enter a pass phrase hint.
24. If you want the pass phrase to be automatically entered during login, mark **Remember pass phrase**. Otherwise, click **OK**. The screen in Figure 8.19 is displayed.

**FIGURE 8.19**
The iFolder Pass Phrase Recovery screen.

![](img/c7771e8540507f2b00c088c7a411b57b_365_1.png)

25. In the iFolder **Pass Phrase Recovery** screen, if you want the network administrator to be able to recover a lost pass phrase, mark **Enable pass phrase recovery**. Otherwise, click **OK**.

**WARNING** Be aware that if a user forgets his or her pass phrase and pass phrase recovery is disabled, the account must be deleted and re-created. Using the pass phrase recovery option is usually a good idea for this reason.

The iFolder installation is now complete. You should see the iFolder shortcut created on your Windows desktop, as shown in Figure 8.20.

You will also see an iFolder icon in your system tray, as shown in Figure 8.21.


## FIGURE 16.13

![](img/a0884097af3186d9b4f616aaa3f065b0_607_0.png)

Enter an account name for this particular dial-up account and the phone number of the ISP.

Now enter the username and password for the account using the modem. These should be the username and password you defined for yourself under the PAP Connection Settings or they can also be the username and password you would normally use to Telnet or ssh into your Linux machine. If you normally use an alias for your e-mail, determine your unique username on the Linux system and enter that instead. For example, I would use kjcox as my username rather than kerry.cox, which would be the prefix to my e-mail address and is simply an alias for kjcox.

## FIGURE 16.14

![](img/a0884097af3186d9b4f616aaa3f065b0_607_1.png)

Insert your username and password to your Linux machine in the required fields.

## INTERNET CONNECTIVITY

The rp3-config program next prompts you to choose an ISP (see Figure 16.15). Currently you can choose between a Normal ISP connection or AT&T Global Network Services. For now, you should choose the Normal ISP option.

The program prompts you to confirm your choices (see Figure 16.16). If the settings displayed match those that you have deemed correct, you may confirm your options and create the account by clicking Finish. You still have the option to return to earlier settings and modify your selections or to choose Cancel if you do not want to create the account now.

## FIGURE 16.15

![](img/a0884097af3186d9b4f616aaa3f065b0_608_0.png)

> Select the ISP of your choice. This option is still awaiting more choices and will be expanded to include other Internet Service Providers as they become available.

## FIGURE 16.16

![](img/a0884097af3186d9b4f616aaa3f065b0_608_1.png)

> Confirm your options and create the unique dial-up account.

The program now presents a window that shows your system's available modem connection (see Figure 16.17). The window shows not only your account name and the phone number of the ISP, but also the connection's current status. You may use this window to display your online status. Here, too, you may add, edit, delete, copy, or dial into any of the accounts that you created.

If you decide to change any of the accounts, highlight the particular account and click Edit. The Edit Internet Connection dialog box appears (see Figure 16.18). Here you can change the account name to something more descriptive or change the default username and password. If your ISP changes its default phone number, you may also edit that field.

## FIGURE 16.17

![](img/a0884097af3186d9b4f616aaa3f065b0_609_0.png)

*The available Internet connections on your Linux machine. In this window, you can modify each account.*

## FIGURE 16.18

![](img/a0884097af3186d9b4f616aaa3f065b0_609_1.png)

*Edit each account's default information.*

If your modem requires additional information or if you wish to help automate the PPP daemon, the Advanced tab allows you to change supplementary options (see Figure 16.19). You can also enter DNS server information in the fields provided.

For more information on the modems detected or manually set up on your system, click the Modems tab of the Internet Connections dialog box (see Figure 16.20). You may add, edit, or delete the modems listed in this tab. If you have more than one modem attached to your system, you can select one to be the default modem that you normally use to dial out.

## FIGURE 16.19

![](img/a0884097af3186d9b4f616aaa3f065b0_610_0.png)

> *Configure DNS settings and dial-up properties under the Advanced tab of the Edit Internet Connection dialog box.*

## FIGURE 16.20

![](img/a0884097af3186d9b4f616aaa3f065b0_610_1.png)

> *Edit the modem choices attached to your system.*

You can also edit any modems that you may have into which other users can dial. For example, if you have multiple phone lines, you can configure each modem attached to your system in the Modems tab.

To change any setting on your modem, click the Edit button. The Edit Modem Properties dialog box appears (see Figure 16.21). In this dialog box, you make any alterations needed. If you do not already have a volume control on your modem, this dialog box enables you to raise or lower the settings. You can also disable touch-tone dialing, which is the de facto standard for most phone lines.

Once you have customized your modem, you can start your dial-up connection. The command to execute the dial-up connection is rp3. Any user can execute the PPP daemon and create a dial-up connection. From the command line or from the RH PPP Dialer icon located under the Programs, Internet menu, you can execute the rp3 program. It will present you with a Choose dialog box that enables you to select which interface to make active (see Figure 16.22). Select your account name, which in this case would be ppp0. Again, you can call the account name whatever you wish, but for the purposes of this example we are keeping it ppp0, much as the system itself would do when creating a new PPP connection.

## FIGURE 16.21

![](img/a0884097af3186d9b4f616aaa3f065b0_611_0.png)

> *In the Edit Modem Properties dialog box, you can edit selected modem options, such as the volume, the unique device name, and the baud rate.*

## FIGURE 16.22

![](img/a0884097af3186d9b4f616aaa3f065b0_611_1.png)

> *Choose your dial-up account name and start the PPP daemon.*

After your modem has dialed and successfully established a connection, a window appears that displays a small graph of bandwidth usage. By right-clicking the graph you can also disconnect or reconnect to your host provider. You can also configure the account and modem properties from under the same window. The kppp3 program provides Linux users the same conveniences associated with the Windows operating system. Gnome continues to assist new users in converting to Linux and to make Linux into a user-friendly platform.

### Running kppp under KDE

With earlier releases of KDE running under Red Hat, you are first prompted to enter the root password in a dialog box when starting the kppp program as a normal user. This corrects the security hole under previous releases that required you to use the chmod command and change the permissions on /usr/bin/kppp to 4711 so that regular users could also use kppp. Previously there was a security issue with the /etc/kppp/options file, which contained the word `lock`. The kppp program wanted to control this file itself and place the word `lock` in the file when initiated. This problem has since been resolved, and kppp runs as root instead.

To use kppp, follow these steps:

1.  When first started, the program prompts you with the main kppp dialog box. Click the Setup button and begin entering the information regarding your ISP, as shown in Figure 16.23.

**FIGURE 16.23**

![](img/a0884097af3186d9b4f616aaa3f065b0_612_0.png)

Setting up kppp in the kppp Configuration dialog box.

Figure 16.23 shows an entry created for a connection called My ISP. The name depends entirely upon your own hosting service, but it should be something easily identifiable if you have multiple connections to different ISPs.

2.  You will want to edit this dial-up configuration and enter the appropriate DNS settings, phone numbers, passwords etc. Click on the Edit... button. This should bring up a Edit Account My ISP dialog box. Your own dialog box will be given the name you determined for your new account. Select the Dial tab under the Edit Account window. Then enter a phone number or the main access number of the ISP, as shown in Figure 16.24.

If you plan to configure the connection script yourself, be sure to choose the setting Script-based in the Authentication field of the Dial tab. You can also choose a Terminal-based setting, which allows you to type your username and password while connecting to the Internet Service Provider. Other alternatives include PAP- and CHAP-based authentication. These two alternatives query the contents of your pap-secrets and chap-secrets files located in the /etc/ppp directory. You can have pppd store your password so you do not have to input it each time that you wish to connect. However, this alternative poses a security risk if you do not want others using your connection for their own purposes.

**FIGURE 16.24**

![](img/a0884097af3186d9b4f616aaa3f065b0_613_0.png)

*Entering the unique phone number under the Dial tab in the kppp Configuration dialog box.*

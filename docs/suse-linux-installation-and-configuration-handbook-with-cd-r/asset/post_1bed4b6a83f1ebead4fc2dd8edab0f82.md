
**No-show users**—Users in this list will not be shown as icons in the KDM login manager. If you check the Show All Users But No-Show Users Box, the users in the All users list will be shown as icons. Users belonging to this list will not show up as icons in KDM.

You can uncheck the Show Users check box to hide all users and allow logins only by typing in the username and password. Also, if you check the Sort Users check box, users' icons will be sorted according to username. By selecting a user from any group and clicking the icon, you can change the icon that belongs to this user. The default KDM users icon path is `/opt/kde/share/apps/kdm/pics/users`. If you add more icons to this path, you will be able to set up an icon for each user who can access the system. It is convenient for each user to have her icon so that she won't have to read the username or type it in. Use different icons for quick access to the system.

**Sessions**—KDM enables you to control the behavior of shutting down the system and session types through the Sessions tab. The groups in this tab are as follows:

- **Allow to shutdown**—You can choose which people are allowed to shut down the system using KDM with the options available in this combo box. The selections are All: All users are allowed to shut down the system; Root Only: After the user clicks shutdown, she must enter the root password to shut down the system; Console Only: Users can shut down the system using the console; and None: No user is allowed to shut down the system using KDM.
- **Shutdown command**—In this field, you must enter the command KDM should use to shut down the system. If your system supports turning off the system—most ATX motherboards do—you can choose to use the command `/sbin/poweroff`. KDE comes with the command `/sbin/halt` by default. The latter command shuts down only the operating system, not the computer.
- **Restart command**—This field should contain the restart command. The restart command on SuSE Linux is `/sbin/reboot`. There isn't much that you can change in this field.
- **Session types**—This list contains the sessions that appear in the KDM session type combo box upon login. You can remove a session from the KDM list by selecting the session and clicking remove. If you want to add a session, type in the session name—the executable name of the window manager—and click Add. You can move sessions up and down in the list by selecting the session you want to move and using the up and down arrows next to the session list.

## File Manager

The File Manager node in the Applications branch is used to configure the look and feel of KFM when it's used as a file manager (see Figure 24.11). The File Manager configuration has the following tabs:

Fonts—You can set up the default font size for the file manager to be small, medium, or large by checking the corresponding box. The Fonts tab also has the following options:

- **Standard Font**—You can change the proportional font for your KFM by selecting a proportional font from this combo box.
- **Fixed Font**—You can select a non-proportional font for your KFM by selecting a font from this list.
- **Default Charset**—You can select a default charset to be used when displaying text in KFM by selecting one of the charsets in this combo box. If you set it to Use language charset, it automatically will be set to the language you use.

FIGURE 24.11
You can change the KFM fonts to suit your preferences.

![](img/659f91d9da7b29976c0625e2e9628511_482_0.png)

Color—From this tab, you can control the colors and configurations for your KFM. You can change the background color, normal text color, and link color by clicking the color button next to them. You can also choose to do the following:

- **Make your cursor shape change over links**—You can do this by checking the Change cursor over link check box. This is a good option to check.
- **Make links appear underlined**—You can do this by checking the Underline links check box. This is a good option to have turned on onscreen, but remember to turn off this option when printing.
- **Make KFM use the colors you specify**—You can do this by checking the Always Use my Colors check box and entering the color(s) you want in this dialog. The colors you specify will override any settings in the document.

## Konquerer, the Web Browser

KFM also can serve as a Web browser. Just as any other powerful Web browser does, KFM enables you to set up proxy settings, HTTP settings, browser identification settings, and cookies settings. In fact, the KFM Web browser called Konquerer will be the KDE file manager name of future versions. The following tabs include the settings for Konquerer:

Proxy—If you enable the Proxy check box, you will be able to edit the proxy settings for the KFM Web browser. Enter the values for your proxy settings and KFM will start using them immediately. You can enter the IP addresses you don’t want to use in the No Proxy For field.

HTTP—In this tab, you can enter the settings Konquerer should use when receiving documents using the HTTP protocol. The settings include the following:

- **Accept languages**—Some Web sites can send many versions of the same HTML page in many languages. You can specify which languages you want KFM to accept by typing them here. Abbreviations are used for the languages, such as “en” for English, “fr” for French, and so forth. You can set it to * to accept all languages.
- **Accept character sets**—You can set up Konquerer to accept or deny specific character sets. Using * will accept any character set.
- **Assume HTML**—Some sites send HTML data without sending the correct information that specifies the document as an HTML document. This option will assume that the received document is an HTML document unless otherwise specified by the Web site.

User agent—In many cases, Web sites will ask the browser to identify itself and its version before the site sends the data to the browser. In the User Agent tab, you can tell Konquerer to identify itself using other well-known browsers and browser versions so that the Web site is assured it is capable of viewing the page. Enter the Web site to which you want Konquerer to identify itself as another browser in the On Server field. Then enter how you want Konquerer to identify itself in the Login field. After you have entered the correct information, click Add to add it to the User Agent list.

The most famous Web browsers are

- **Mozilla**—Used by Netscape Navigator to identify itself. Append version 3 to ensure you can view frames.
- **Internet Explorer**—Used by Microsoft Internet Explorer to identify itself. Append version 3 to ensure you can view frames.

Note that Konquerer is not 100% compatible with either Mozilla or Internet Explorer. The page might not look the same if you see it using Netscape Navigator, for example.

Cookies—Some Web sites use cookies to store information about you so that you don’t have to enter this information each time you enter the site. Cookies are stored locally on your hard drive and do not require large disk space. You can control how KFM behaves with cookies. You can choose to disable cookies or have Konquerer ask you before it receives cookies. You also can delete a cookie by selecting it from the list and clicking Delete. You can choose to not accept cookies from a certain Web site by entering the Web site's address and clicking Reject.

## Panel

The Panel node includes both taskbar and panel settings. In this node, you can configure how your panel should look, how it should behave, the virtual desktops settings, and the disk navigator settings. The settings are configured through the following tabs:

Panel—The Panel tab enables you to set up the look of your panel and taskbar. You can set their placements by selecting the check boxes that correspond to the location of each. For example, you can set up your taskbar to be on top by selecting the Top check box in the Taskbar group box. Or, you can move the panel to the right side of the screen by selecting Right from the Location group box (see Figure 24.12).

FIGURE 24.12
Changing the placement of the panel in KDE is as easy as checking some radio buttons. You also can access this dialog by right-clicking the panel and selecting Configure.

![](img/659f91d9da7b29976c0625e2e9628511_484_0.png)

In addition, you can set the icon size of the panel to be Tiny, Normal, or Large by selecting the appropriate check box in the Style group. If you are running KDE on a high resolution, it's a good idea to configure this option to show large icons. People with KDE running on low resolution might prefer to have tiny icons.

Options—You can customize your panel to some extent by setting options for it. The options, as shown in Figure 24.13, include the following:

- Show Menu Tooltips—By showing menu tooltips, when you open the K menu, a tooltip will appear for each application in the menu. This is a good option for people using KDE for the first time. For example, if you open K, Internet and move the mouse over kppp, a tooltip will tell you this is an Internet dial-up tool.

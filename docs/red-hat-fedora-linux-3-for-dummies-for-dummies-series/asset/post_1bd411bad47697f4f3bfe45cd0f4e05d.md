
Your browser is now Java-capable. Clicking the Help::About Plug-ins menu will show the Java plug-ins.

The following list shows some more common plug-ins, available for Linux, that you should consider installing (all can be accessed from the plugin doc.mozilla.org page):

- **Acrobat (Adobe):** Reads the Adobe Portable Document Format (PDF) files. Many Web sites provide information via PDF files rather than via HTML or other formats. (Note that you can use the open-source xpdf or gpdf programs to view PDF files.)
- **Java (Sun Microsystems):** A programming language that many Web sites use to provide dynamic content.
- **MPlayer:** Allows Mozilla to play multimedia Internet audio/video streams. See Chapter 12 for a description of the standalone MPlayer (non-plug-in) application.
- **RealPlayer 10 (RealAudio):** Allows you to play the RealNetworks audio and video streams. Many Internet radio stations still use the RealNetworks protocols to stream their content.
- You can also use RealPlayer 10 to listen directly to RealAudio streams.
- **Shockwave (Macromedia):** Provides multimedia, graphics, and game-oriented support.

## Protecting your passwords

You can use Mozilla to save passwords that you use when you're browsing the Internet. When you start saving passwords, you should also start encrypting them. Encrypting passwords is optional, but we highly recommend it. Encrypting makes finding your passwords much more difficult for someone else. With all the business you may do on the Internet, you must protect your information as much as possible. Follow these steps:

1. From your Mozilla browser, choose **Preferences** from the **Edit** menu.
2. Click the plus sign (+) next to the **Privacy & Security** menu. A submenu opens.
3. Click the **Passwords** option. The Passwords dialog box opens.
4. Click the button labeled **Use encryption when storing sensitive data**.
5. Click **OK**.
6. Click the **Edit::Preferences** menu again.
7. Click the **Master Passwords** option in the Privacy & Security submenu.
8. Click the **Change Password** button. The Change Master Password dialog box opens.
9. Enter your **password** in the **New password** text box. The Password quality meter shows how “good” your password is.
10. Reenter your **password** in the **New password (again)** text box. When both passwords match, the OK button becomes active.
11. Click the **OK** button.

Mozilla will now encrypt any password that you save. You have to enter the master password just once the first time you access a password-protected object. This is a simple and effective security tool.

You can manage passwords whenever you want. Choose **Preferences** Privacy & Security from the Edit menu. Choose **Manage Passwords** and the Passwords dialog box opens. You can then remove passwords as desired.

## Come the Evolution Revolution

Evolution is a software system that provides a big step in the — sorry — evolution of the Linux desktop. Evolution provides an excellent e-mail-and-calendar client (along with other functions) to create a single, integrated package. Evolution provides these capabilities:

- Calendar
- Contact manager
- E-mail client
- Personal Digital Assistant (PDA) manager
- Task master (to-do list)

The following two sections describe how to configure the Evolution e-mail and PDA functions.

### E-mail Evolution

Fedora Core uses Evolution as its default e-mail client. Evolution makes it easy for you to configure one or more e-mail accounts. These steps describe how to configure Evolution to send messages to and receive messages from your ISP e-mail account:

Part III: Linux, Huh! What Is It Good For? Absolutely Everything!

> **TIP** Linux traditionally used the Mozilla e-mail client by default. Mozilla e-mail is still included in the Fedora Core distribution, on your DVD, but is not installed by default.

1. Click the Evolution Email icon (which looks like an envelope and stamp) on the GNOME Panel.
   - An information dialog box opens, telling you about the state of Evolution.
2. Click the OK button.
   - The first time you start Evolution — before you configure any e-mail accounts — the Evolution Setup Assistant opens.
3. Click the Forward button.
   - The Identity window opens.
4. Enter your name and e-mail address in the appropriate text boxes and click the Forward button.
   - You can (optionally) enter your organization and *signature file*, a file where you keep personal or business information to be appended to the end of every message you send.
   - Figure 11-2 shows some sample entries in the Identity window.

The Receiving Mail dialog box opens.

![](img/41feae212f5c6612ff709354891f7b39_163_0.png)

5. Click the **Server Type** drop-down menu and choose the option that matches your ISP's e-mail system.
   - Most ISPs use the Internet Message Access Protocol (IMAP) server type.
   - The **Receiving Mail** window expands so you can enter more information about your ISP's e-mail system.
6. Enter the host name of your ISP's e-mail server and your ISP user-name.

Figure 11-3 shows a sample screen in this dialog box.

- Your ISP provides you with the name of its incoming and outgoing e-mail servers when you first subscribe. You need to enter the incoming server name in the **Host** text box. For example, your ISP's incoming server may be `mail.mysp.com` or `imap.mysp.com`.
- Your ISP user name may be different from your user name on your Linux computer. For example, your ISP user name may be based on your first initial and last name — for example, `garagon` — but your home Linux computer user name may be just your first name, as in `gabe`.

![](img/41feae212f5c6612ff709354891f7b39_164_0.png)

7. **Click the Forward button.**

The second Receiving Mail window opens.

You can change options, such as having Evolution automatically look for incoming messages, by selecting the Automatically check for new mail option.

![](img/41feae212f5c6612ff709354891f7b39_165_0.png)

8. **Make any necessary or optional changes and click the Forward button.**

The Sending Mail window opens.

9. **Enter your ISP's outgoing mail server name and click the Forward button.**

Figure 11-4 shows a sample screen in this window.

- The default outgoing Evolution e-mail protocol is SMTP (which is used frequently by ISPs, so you may not need to change it). Your ISP should supply you with the protocol it uses.
- A few ISPs may use encrypted Secure Sockets Layer (SSL) connections and require authentication. Again, you need to obtain this information from your ISP and use those options, if necessary.

![](img/41feae212f5c6612ff709354891f7b39_165_1.png)

Figure 11-4: The Sending Mail dialog box.

10. Click the Forward button when the Account Management window opens.
    - Evolution uses your e-mail address as the default name for the account you create. You can change the name if you want, but it’s not necessary.
    - Your new account is the default account if it’s your only one. Otherwise, you can choose to make it the default by selecting the Make This My Default Account option.
11. The final configuration step requires you to pick your time zone. Click the dot closest to your location on the displayed map.
    - A bigger map appears, which enables you to fine-tune your location, if necessary. It’s the same system you use in Chapter 3 to set your computer’s time zone.
12. Click the Forward button.
    - The Done window pops up.
13. Click the Apply button.
14. An informational Evolution dialog window opens. Read the message and click the OK button.
    - An Enter Password dialog window also opens.
15. Enter your e-mail account password and click the OK button.
    - Optionally, you can click the Remember this password button.

Evolution opens and displays a Summary window; a separate dialog box also opens and displays information about itself (click the OK button after you finish reading the information in the dialog box). Shortcuts to the Evolution function are on the left side of the window. Click your e-mail account shortcut to see your new e-mail address listed. (You can also access your account by clicking the Summary button, toward the upper-left corner of the window.) Select your account to make it active. You can then send and receive messages. You can also perform any other typical actions on your account, such as sorting, moving, and deleting messages.

## Using Evolution with your PDA

You can use the Evolution calendar, to-do manager, and contact manager with your PDA. In this section, we concentrate on showing you how to use Evolution to back up your PDA because that’s one of more interesting and fun things you can do (among many). You can find out more about using the calendar by reading the online Evolution documentation (choose Help or visit www.gnome.org/gnome-office/evolution.shtml) or by simply experimenting with it.

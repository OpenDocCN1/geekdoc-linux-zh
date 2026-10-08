
## CHAPTER 14

### # Speeding Up the Logon Process

Ever wonder why it takes your computer so long to start up after you log on? After all, the system already loaded the majority of the operating system components. Does your computer take longer to load after you sign on than it used to take when you first brought it home? These are some of the questions this chapter answers. You can make your system load faster by using a number of cool tweaks and hacks. The previous chapter touched on how to make the system boot faster. This chapter concentrates on how to make the system load faster after the operating system has loaded and you are presented with the welcome sign-on screen.

After you turn on your computer, it goes through the boot-up process, which loads the main system components and drivers. When those are finished loading, the Windows shell is started and the lock screen is displayed. After the lock screen is displayed and you sign on, the system begins to load your user profile settings and the rest of the Windows shell. When that is finished loading, the system runs the applications that are in the startup folder as well as other sneaky registry startup programs. After these applications are finished loading, the busy icon no longer represents your cursor, and you are set to do whatever you want with your computer.

This chapter begins by examining ways to speed up the logon process. Then it discusses how to get rid of all those extra applications that run at startup that further slow down your computer. When you use the tips you learn in this chapter, your system will have a much faster loading time.

### Speeding Up the Logon

As I just mentioned, a lot occurs when you log on to your computer. Windows has to validate your password, load your profile settings, apply the settings, and then launch any additional applications that are registered to start automatically. Those are a lot of areas to fine-tune to allow for a faster logon. To get started, take a look at PIN logon.

### Using a PIN Instead of a Password

I always use a long password to protect my user accounts and data on my Windows 8 PC. Although this provides great security for my account, it is time-consuming every time I turn on my PC. The new account PIN feature in Windows 8 provides an alternative logon method. Instead of typing in your password, key in your four-digit PIN and you are logged in immediately. I found this feature to be a compromise that speeds up the logon of my PC, but still allows me to keep a strong password for remote access.

Setting a PIN for your account was discussed in Chapter 5. For your convenience, below is a recap of the steps to enable a PIN for your account:

- 1. Open the Start screen, type in **PIN**, click the Settings filter, and hit Enter.
- 2. Under Sign-in Options click on the Create A PIN button.
- 3. Enter your current password when asked.
- 4. Enter your PIN twice and click Finish.

### Enabling Automatic Logon

If you are the primary user of your computer and you do not have any other users, or if everyone in your household uses the same username, you are the perfect candidate for enabling automatic logon. Automatic logon is a great technique that saves you time by canceling the need for your computer to wait while you type your password. Even if you do not have a password assigned to your account, you are still required by the logon welcome screen to click your name to sign in. Having to do these tasks manually is an unnecessary waste of time when you can use automatic logon instead.

Enabling automatic logon is a quick and easy registry hack. Follow these steps to speed up your sign-on with automatic logon:

- 1. Open the Start screen, type **regedit**, and press Enter.
- 2. After Registry Editor has started, navigate through HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon.
- 3. Locate the AutoAdminLogon entry. If the key does not exist, create it by right-clicking the Winlogon folder and clicking New, and then String Value.
- 4. Right-click the AutoAdminLogon entry and click Modify. Set the Value to 1, as shown in Figure 14-1. Then click OK to save the new value.

> Automatic logon can be a great feature, but it can also create a security problem for your computer. If you use your computer for business, if you have data you prefer to keep safe from others, or, both, I strongly recommend that you do not enable this feature. If you happen to step out of your office or if your laptop is stolen, you have left the door to your computer wide open. By enabling automatic logon, you are trading convenience for physical access security. However, you are not changing your network security, so your data is still safe from network attackers. The risk of someone remotely connecting to your computer is the same as if you did not have automatic logon enabled.

![](img/ea75090cfee8ac890f64c8c4f62f7285_264_0.png)

Figure 14-1: Set AutoAdminLogon to 1 to activate automatic logon.

- 5. Locate the DefaultUserName entry or create a string value if it does not exist.
- 6. Right-click DefaultUserName and select Modify. Set the value to the username that you primarily use to sign in to Windows. Click OK.
- 7. Locate the DefaultPassword entry or create a string value if it does not exist.
- 8. Right-click the DefaultPassword entry and set the value to your password.
- 9. Close Registry Editor and restart your computer.

After you reboot your computer, Windows 8 should automatically sign on to your account. Your computer should now get to the desktop more quickly than before. If you ever want to disable automatic logon, go back into Registry Editor and set the AutoAdminLogon entry to 0. It’s also a good idea to delete the DefaultPassword string value so your password is not stored in plain text in the registry.

### Adjust the Startup Programs

After you sign on, the system loads your profile, finishes loading the Explorer shell, and then begins to load the startup programs. If you have ever purchased a computer, either online or from a retail store, I am sure that you have noticed all the annoying software programs that load automatically right after you sign on. Some computer manufacturers go so far overboard with startup applications that Windows has to hide them so that your taskbar has enough space to show open windows. If you are like me and have built your own computer, you do not have to deal with all the preloaded junk that comes from the big computer manufacturers. Nevertheless, you are still vulnerable to auto-start programs that are installed by many of the popular applications you use. Over time, as you install more applications, the automatic startup applications can get out of control and definitely slow down your logon.

Popular applications such as Adobe Photoshop, Skype, Java, iTunes, and many more install auto-start components. Consider all the extra auto-start components these applications add on top of the auto-start applications already installed on your computer, such as antivirus and anti-spyware applications. Your logon can slow to a crawl because of the dozens of applications that load after you sign on. This section helps you discover what programs are starting automatically and then shows you some great tricks to stop them all from starting up.

### Identifying and Disabling Auto-Start Applications

The first step in stopping the auto-start applications is to identify exactly what is starting up and whether it is needed. You can use two different utilities to find this information. The first is the enhanced Task Manager utility that comes with Windows 8. Task Manager now enables you to see which applications start on logon. Another great utility is called Autoruns by Microsoft Sysinternals. Autoruns is a more comprehensive utility that enables you to see all applications that run on logon, as well as other types of auto-starts such as browser or shell plug-ins.

First, I cover using Windows 8’s Task Manager to identify and disable unneeded auto-start applications. Then I dive into using Microsoft Sysinternal’s Autoruns to disable auto-start applications as well as other auto-start components.

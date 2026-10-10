
# Start It Up

Now you can get started with your whirlwind tour through KDE.

We're assuming that you've already located and installed KDE on your system, or that it was pre-installed when you arrived at the machine; if you haven't, jump to Appendix A to find out where to get KDE and information on installing it. As soon as you've got KDE set up, come back and start here.

Be sure that you use KDE as a normal user on your system. When you installed Linux, you should have created both user accounts and a special super-user account called root. Don't log in as root just to play with KDE — save root for when it's needed. The root account is the system administration account, and it has the authority to change everything about the operating system — even the basic processes that make the machine work. If you work with KDE in your user account, you can't break anything critical. One of the great features of Linux and other UNIX-based operating systems is that each user has a separate account with dedicated disk space to work in, and those user spaces are separate from the programs that really run the computer. If you're working in a user account, you really have to try hard to do anything that permanently harms the computer. If you're working as root, you can cause damage a lot more easily.

Your machine probably is turned on and waiting patiently for you at the login prompt. If not, go ahead and boot up now.

1. **Log into your machine using your user account name and password.**
   - Depending on the Linux distribution you chose while installing, or if you've already installed and configured KDE, you may see a graphical login instead of a shell login prompt. A graphical login is a more pleasing welcome from your computer than the white-on-black of a shell prompt. If you'd like to set up a graphical login for your system, we explain the procedure in Chapter 14. Log into a computer with a graphical login by typing your user account name and password, and skip ahead to the "Touring the Desktop" section.
   - If you haven't yet configured your system to use KDE as your default GUI, refer to Appendix D for more information on the usekde script. This script copies some basic files, which KDE needs in order to run properly, into your home directory.

2. **After you log in at the shell prompt, type startx.**
   - You use this command every time you want to open KDE. The startx command actually starts up the X Window System, but after you run the usekde script, you set X to run KDE as your default desktop environment. You can actually configure X to run KDE automatically, every single time you boot up the computer by changing a few lines of code deep in the guts of Linux. See Chapter 13 for a down and dirty discussion of run-level, or how your computer knows which programs to run first.

3. **Wait for the KDE desktop to appear, as shown in Figure 1-1.**
   - A bunch of text scrolls up the screen, and then everything goes dark, (well, goes gray, but that doesn't sound quite as dramatic). How long the screen stays dark depends on how much memory you've got installed in the computer. (Computer graphics, like employees, are easily cajoled into working faster and better if you throw money at them.)
   - If something went wrong in your KDE setup, or if you haven't run the usekde script yet to tell the X Window System that you want KDE as your default desktop environment, you may get a surprise after typing startx. Instead of KDE, you may get another window manager, such as Fvwm. If this happens, just exit out of the graphical environment (try right-clicking on the desktop — an Exit or Logout command is often in the context menu). Then go back to Appendix A and reconfigure KDE.

![](img/8dd43d91b80664e771e0c0a824d7392d_38_0.png)

# Touring the Desktop

The first time you run KDE, it appears with a basic desktop configuration (refer to Figure 1-1). (And yes, it sure does look a heck of a lot like Windows 95, doesn’t it?)

If you don’t like the default look, don’t worry. Chapters 6 and 7 are all about desktop design, theme management, and doing heavy-duty cosmetic surgery on your desktop. For now, though, work with the default KDE desktop.

That gray horizontal bar running along the bottom of the screen is the *panel*. Use the buttons on the panel to start programs, which find files, launch applications, or control KDE itself. You will get to know the panel very well, because it’s the central nervous system of KDE. Read Chapter 5 for more information about the panel and how to customize it.

KDE also puts some icons along the left side of your desktop. These icons enable you to run some common *utility programs*, or little programs that do important tasks behind the scenes. You can use the icons to create new files, remove old ones you don’t want any more, print, or move files between CDs, ROMs, diskettes, and your hard drive. See the “What Are All These Icons For?” section of this chapter for a description of each icon and its basic function.

Along the top of the screen, you see the *taskbar*. If you’ve used Windows 95 or Windows 98, you’re already familiar with taskbars. We discuss the KDE taskbar in the “Hanging Out at the (Task) Bar” section of this chapter. Basically, you can use the taskbar to manage various applications and windows that you have open at the same time.

All of these facets are customizable. You can move them to different places on the screen, collapse them so you don’t have to see them, or line them up neatly. Chapters 5, 6, and 7 contain a lot of information and ideas to help you tailor KDE to your own tastes.

One other feature that we should mention at this point is KFM, the KDE File Manager. KFM works like Windows Explorer or the Mac OS Finder. KFM is a graphical representation of the computer’s file system, and it shows all the files in your *home directory*, the directory associated with your user account. Like Explorer or Finder, KFM shows your directory as a collection of folders and files. Think of KFM as an electronic file cabinet, because that’s the way it was designed to work. You can drag files from one folder to another, or open windows that show the contents of various folders.

# What Are All These Icons For?

Take a closer look at the desktop. Along the left side, you see six icons (refer back to Figure 1-1). These icons are super-duper shortcuts to some frequently used commands, and using them well can really speed up your desktop management skills (one of those fancy terms that really means “keeping your desk clean”).

You can also create your own icons for programs that you use frequently by clicking the Template icon. Creating your own icons eliminates some of the searching that you have to do if you start programs from the KDE menu.

![](img/8dd43d91b80664e771e0c0a824d7392d_40_0.png)

Double-clicking the Autostart icon pops open a window where you can put links to programs on your hard drive. KDE makes sure that, after you start KDE, all the programs linked to the Autostart folder start automatically.

You need to remember two important aspects about Autostart, though.

- If you’re running a Linux system, and you’re the only user, you simply may not restart KDE very frequently. UNIX-based computers have amazing *uptimes* compared to Windows computers. It’s not unusual for a machine running Linux to go for a month or two without needing to be restarted. So, if you’re putting programs here that you need every day, you’re probably going to need to open them manually anyway. (If you don’t live alone, or you have multiple users on this machine, you log out of KDE every time you end a session, so that Autostart is more helpful for you. Logging out is a good habit anyway — you never know when your cat is going to learn to type and send spam out under your e-mail address.)
- You don’t have to link every single program to Autostart. We’ve heard of people who set up Autostart that way. Every time they launch KDE, the poor machine spends time just opening programs . . . the word processor, the calendar, the accounting program, the graphics program, all the utility programs, the database, all the games, and so forth. You can always open programs just by finding them in the panel and clicking, so that you really don’t need to add much to Autostart — maybe Netscape and your calendar, if those are the two programs you always open after you start a new session anyway.

![](img/8dd43d91b80664e771e0c0a824d7392d_40_1.png)

Double-clicking the Printer icon opens the printer configuration screen. On that screen, you can set up your printer for various kinds of paper, the direction you want text to print, and other basic printer information. Despite its name, the Printer icon doesn’t actually send your files to be printed. Commands such as that are usually sent from inside a particular program. For example, if you’re working on a letter or report, you tell the computer to print it by issuing the word processor’s print command.

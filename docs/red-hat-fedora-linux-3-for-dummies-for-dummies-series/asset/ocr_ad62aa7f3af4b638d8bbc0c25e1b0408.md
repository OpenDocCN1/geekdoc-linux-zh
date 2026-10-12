The use of unique identities helps to keep the actions of one person from affecting the actions of another because many people may be using the same computer system at the same time (for example, over a network). A benefit of this strategy is that Linux computers are essentially invulnerable to viruses simply because no user’s files and directories can be used to corrupt the system as a whole.

As Fedora Core boots, you see all sorts of messages scrolling by on the screen. After the scrolling stops, the login screen appears.

+   * **REMEMBER**

If you chose (during installation) not to have the X Window System start automatically whenever you boot your system, you see the login: prompt.

If you make a mistake while typing the password or your login, the system asks you to retype it.

+   * **WARNING!**

We strongly recommend that you do most of your experimentation with Fedora Core as a nonprivileged user — and that you log in as the root user only when necessary. If you operate as root, you can delete or change anything and everything — and you run the risk of corrupting your system, having to reinstall the operating system, or losing data. When you’re logged in as a regular user, you can accidentally erase your own files and data, but you cannot erase someone else’s files or system files.

Fortunately, Fedora Core provides many graphical administration utilities you can start as a nonprivileged user. Each Fedora Core administrative utility prompts you to enter the root password as it starts and then performs its specific function, but only that function, with root privileges. You’re prevented, therefore, from doing unintended damage to other systems. (See Appendix C for information about how file permissions work and how you can modify them.)

# ## Using Graphical and Text-Based Applications and Utilities

Fedora Core installs the graphical X Window System (also known simply as X) by default. You can perform most administrative tasks with the GUI-based tools (GUI stands for graphical user interface) that Fedora Core provides. Most of the how-to instructions in this book use the X-based applications and utilities. We do that because they’re generally easier to use — and because this book wasn’t written for techie systems administrators.

Occasionally a utility or program doesn’t run graphically. Believe it or not, some geeKier users prefer to use a text-based system. If you’re not familiar with doing some basic administrative tasks with a text-based system, we
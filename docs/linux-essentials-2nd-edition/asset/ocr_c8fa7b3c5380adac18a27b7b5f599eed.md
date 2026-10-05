# Chapter 6 • Getting to Know the Command Line

computer locally via a text-mode console. In addition, a shell is started when you log to the console remotely using a text-mode login protocol. However, that particular method goes beyond the scope of this book.

![](bbox=[0.065, 0.165, 0.215, 0.233])

The default shell in most Linux distributions is the Bourne Again Shell Bash or bash, which is based on an older shell called the Bourne Shell. Other shells are available. Most of them are similar to Bash in broad strokes, although some details differ. Each account specifies its own default shell, so individual users can change their shells if they like. (This is done with account management tools, such as usermod, which is described in Chapter 13, "Creating Users and Groups.")

Other shells include tcsh, ksh, and zsh. Shell choice is a matter of preference. If you're starting out, it's best to stick with Bash simply because it is popular.

# Launching a Terminal

Most Linux distributions allow you to install GUI terminal programs. Typically, a desktop environment comes with its own, so your terminal program choices also depend on the desktop environments that you install. (You can even run one desktop environment's terminal program within another.) Many terminal programs include the word terminal in their names, although some don't, such as the K Desktop Environment's (KDE) Console and the generic Xterm.

The details of how to launch a terminal program from one desktop environment to another. You can normally find an entry in your desktop environment's menus, as outlined in Chapter 4, "Using Linux Programs." For example, if you are using the KDE desktop environment, you can find the available terminals by following this menu-driven procedure:

+   1. Click the menu button, typically located at the lower-left corner of the screen.
2. Click All Applications > System > Terminal. You should see at least one terminal, and perhaps more than one, in a display similar to Figure 6.1. Three terminal programs are shown in Figure 6.1: Terminal (Console), Terminal - Super Mode, and Xterm.
3. Select the terminal that you want to, and it will launch.

Many desktop environments also provide a search method for terminal programs. For example, if you are using Ubuntu Unity desktop, follow this basic procedure:

+   1. Click the Dash (an icon with the Ubuntu symbol) located at the top of the application launcher.
2. In the search box, type term, as shown in Figure 6.2.
your screen. To remove it from the list of packages to be installed, press - on your keyboard while it is selected.

Pressing “u” will have Aptitude download the latest package information from your APT servers (equivalent to an apt-get update), then pressing “U” (capital “U”) will have it select for upgrade any packages for which updates are available. Once you have done that, as well as used + and – to select any other packages you want to install or remove, press “g” to have Aptitude show you a summary of what will change. This summary is color-coded so that packages to be removed are colored purple, packages to be installed are colored green, and packages to be upgraded are coloured cyan. Press “g” again to confirm the plan and have Aptitude start up apt-get to make your changes. If the summary is incorrect, press “q” to go back to the menu screen.

![](bbox=[0.14, 0.45, 0.68, 0.78])

FIGURE 34.1 The Aptitude package manager is text-based, but lets you use your mouse to access its menu bars.

You can at any time press ? to bring up a short list of common commands for Aptitude. The most popular commands are listed across the top, such as the Ctrl+T shortcut to get to the menu bars.

# NOTE

Aptitude, like apt-get, is not entirely devoid of humor. Whereas apt-get has Super Cow Powers, running aptitude moo prints out a short message that Aptitude has no such Easter eggs. However, if you run aptitude -v moo you'll see something else, if you run aptitude -v -v moo you'll see something else, and so on—just keep adding more -v parameters!

Once you are in Aptitude, you can while away some time by playing Minesweeper—it is under the Actions > Play Minesweeper menu option.
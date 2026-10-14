
It’s much more concise and clear. It assumes as its base the Linuxconf entry screen. The other advantage to this approach is that it’s not interface specific, so regardless of which interface you’re using, you know exactly where the information is. You’re happy, we’re happy, and the trees which lobbied against lengthy descriptions are happy. What could be better?

## Running Linuxconf

To run Linuxconf you must have root access. If you are logged in as something other than root, there is an easy way to handle this situation. Use the su command to become root. In case you aren’t familiar with it yet, type su at the shell prompt and hit [Enter]. The password it asks you for is the root account’s. Once you’ve entered that correctly you’ll have phenomenal cosmic power! Well, complete control of your system at any rate. Anyway, type linuxconf at the shell prompt to begin the program. Linuxconf has the following user interfaces:

- **Command line** — Linuxconf’s command-line mode is handy for manipulating your system’s configuration in scripts.
- **Character-Cell** — Using the same user interface style as the Red Hat Linux installation program, the character-cell interface makes it easy to navigate your way through Linuxconf, even if you aren’t running X.
- **X Window-Based** — Linuxconf can take advantage of X, and give you an easy-to-use "point and click" tree menu interface. This form of navigation is new in Linuxconf! Please see the Tree Menu Interface subsection for more information. This is the interface we’ll use for illustrations throughout this chapter.
- **Web-Based** — A Web-based interface makes remote system administration a breeze. The Web interface will even play nice with the Lynx character-cell Web browser!

Linuxconf will normally start in either character-cell or X mode, depending on the DISPLAY environment variable. The first time you run Linuxconf, an introductory message will be shown; although it is only displayed once, accessing help from the main screen will give you the same basic information.

Linuxconf has context-specific help available. For information on any specific aspect of Linuxconf, please select Help from the screen you'd like help with. Note that not all help screens are complete at this time; as help screens are updated, they will be included in subsequent versions of Linuxconf.

## Tree Menu Interface

The new version of Linuxconf comes complete with a tree menu interface.

![](img/46f4935125ba89e12897afbe9d77a097_177_0.png)

Figure 8-1: Linuxconf Entry Screen

Finding the appropriate panel should be simple and fast. You can collapse and expand sections by clicking on the menu item icons. Click the icon once to activate it for that particular sub-menu. A single click will then collapse it; another single click will expand it again. Selected entries will appear as tabs in the right-hand panel and will remain there until closed. This will greatly reduce the clutter of windows on your desktop that Linuxconf has typically caused. If you end up with more tabs open than you like, just hit Cancel on the bottom of each tab to close it without making any changes, or Accept to implement them.

> Please Note: If you've grown fond of your previous X Window System interface, it's still available. To return to it:

- 1. Start Linuxconf by typing linuxconf at the shell prompt
- 2. Open [Control] -> [Control files and systems] -> [Linuxconf modules]
- 3. De-select the "This module is active" check box for the treemenu module.
- 4. Click Accept
- 5. Click Quit
- 6. Restart Linuxconf

## Enabling Web-Based Linuxconf Access

For security reasons, Web-based access to Linuxconf is disabled by default. Before attempting to access Linuxconf with a Web browser, you'll need to enable access. Here's how to do it from the text-mode interface:

- 1. Start Linuxconf by typing linuxconf at the shell prompt
- 2. Open [Config] -> [Networking] -> [Misc] -> [Linuxconf network access]
- 3. In the Linuxconf html access control dialog box, enter the hostname of any computers that should be allowed access to Linuxconf. This would also include your own system, if you wish to use the Web-based interface locally. Web accesses related to Linuxconf may be logged to your system's htmlaccess.log file by selecting the check box shown.
- 4. Select the Accept button and press [Space]. Then select the Quit buttons on

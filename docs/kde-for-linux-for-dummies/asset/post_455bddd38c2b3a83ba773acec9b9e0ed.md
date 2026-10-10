
The tilde character (~) is a filename wildcard that is shorthand for your home directory. You can use it when typing pathnames to make it easier to enter the path to a file or subfolder in your home directory. For example, instead of typing the full path and filename /home/username/docs/MyDoc.txt, you can simply type ~/docs/MyDoc.txt.

## Navigating

Using KFM to navigate your file system is like using your car to drive around in a city. Driving the car is the easy part. Finding your way around on the city streets is the challenge. If you know the layout of the city and you're familiar with the streets, you can get from place to place easily, but if you're a stranger in the city, the streets seem like a confusing maze.

As with your car, KFM has a few simple controls that you'll master easily. (Finding out how to use KFM is a lot easier than learning how to drive. We show you how, and besides, you don't have to learn to parallel park KFM.) When you take KFM out for a spin around your file system, how easily you find your way among the files and folders depends on how well you know your file system. As soon as you venture beyond the local neighborhood of your home directory, the Linux file system can be as confusing to a new-comer as the streets of a strange city. As with some of the newest cars that include navigation aids such as GPS (global positioning satellite) receivers and moving map displays, KFM includes features to help you discover and explore your files and folders — but nothing takes the place of familiarity with the local streets and with your file-system layout.

Actually, using KFM to navigate your file system is similar to using a Web browser to navigate a Web site. If you can surf the Web, you already know the basics of surfing your file system. Here's a summary of the KFM navigation tools:

- Type a path name in the Location box below the KFM toolbar to display the contents of that directory in the KFM window. As with a Web browser, KFM always displays the full path name of the current directory in the Location box, even if you use another navigation technique to open the directory.
- Click a folder icon (or the underlined text name of the folder) to open the folder and display the contents of the selected directory in the KFM window.

![](img/8dd43d91b80664e771e0c0a824d7392d_87_0.png)

![](img/8dd43d91b80664e771e0c0a824d7392d_88_0.png)

- You can easily identify folders (directories) as opposed to files by their file-folder icons, which are visible in most KFM views. Files can have a variety of different icons, depending on the type of file, but directories are almost always represented by the file-folder icon. (A few special-purpose folders, such as desktop/, have custom icons.) In the Text view, KFM doesn't display icons, but you can still identify folders by the slash character (/) appended to the end of the directory name in true UNIX tradition.
- Click the Up button on the toolbar to move up one level in the directory tree and display the contents of the parent directory.
- Click the Back button on the toolbar to display the previous folder's contents.
- Click the Forward button on the toolbar to reverse the effects of the Back button and display the contents of the next directory in the history of directories viewed in the current KFM session. (The Forward button is grayed out until you use the Back button to step back through the list of previously viewed folders.)
- Click the Home button in the toolbar to display the contents of your home directory. No matter how far you venture into the dark alleys of your file system, you can always return to familiar territory with one click on this button.
- Click the Reload button in the toolbar to update the display to reflect changes in the files and folders you are viewing in KFM.
- Click Stop to halt loading (or reloading) the contents of a directory. Sometimes it takes a while to read the contents of a directory containing a large number of files and subdirectories and you may not want to wait for KFM to finish (especially when you realize that you clicked the wrong folder). The Stop button enables you to interrupt the loading process so you can go ahead and give KFM other commands.
- The gear icon on the right end of the toolbar spins while KFM is working reading the contents of a directory. When the gear stops spinning, KFM is idle, the display is complete, and the program is ready to accept new commands.

## Getting Different Views of Your Files

KFM gives you several ways to customize how the program represents the files and folders shown in the KFM window. You're not stuck with the default arrangement shown in Figure 4-2. You can choose from one of four different views and select other options to control such things as whether KFM displays hidden files.

![](img/8dd43d91b80664e771e0c0a824d7392d_89_0.png)

Figure 4-2: The large icons of the Icon View are easy to identify.

**Icon View** — When you first start the KDE file manager, the KFM window appears and displays the contents of your home directory as rows of large icons — one icon for each visible file and folder within the directory. (Refer back to Figure 4-2.) The icons are large and easy to see, which also makes them easy to click and drag with your mouse. Each icon is labeled with the file or folder name beneath the icon. If you're using a different KFM view and want to switch back to Icon View, choose View > Icon View.

**Long View** — If you need to see more detailed information about your files and folders, Long View (shown in Figure 4-3) is the way to go. Instead of rows of large icons, the display consists of a table-style listing of your directory's contents. Each file or folder appears on a separate line that starts with a small icon and the file or folder name on the left and includes the file's access permission mask, owner, group, size, and modification time and date. Choose View > Long View to switch KFM to this detailed display mode.

**Short View** — If you like the small icons and compact list style of the Long View, but don't need all the detailed information about each file or folder, then choose View > Short View to see a display similar to the one in Figure 4-4.

# Chapter 4: A Place for Your Stuff — the KFM File Manager

![](img/8dd43d91b80664e771e0c0a824d7392d_90_0.png)

Figure 4-3: The Long View shows more details.

![](img/8dd43d91b80664e771e0c0a824d7392d_90_1.png)

Figure 4-4: The Short View is a compromise between Icon View and Long View.

**Text View** — The Text View is essentially the same as the Long View, except without the icons at the left end of each row. The absence of icons enables KFM to render a long directory display a little faster, but the speed difference between Text View and other views is seldom a major issue. Basically, Text View is for purists who just prefer the traditional text-based file listing. To invoke Text View, choose View➔Text View.

No matter which view you choose, you still work with the files and folders in the KFM window the same way. You can click icons or filenames to open the selected files or folders and you can drag icons or filenames to copy and move files. (More on that in the “Copying and Moving Files” section of this chapter.) The view changes only how the files are displayed, not what you can do with them.

## Climbing the directory tree

Finding your way around city streets is easier with a good roadmap. In these days of fancy electronic gadgets, the premier luxury cars often come equipped with GPS receivers linked to electronic maps to show you where you are and how to reach your destination.

KFM includes a powerful navigation aid that serves its purpose in helping you find your way around your computer’s file system. If you choose View->Show Tree, a separate panel appears in the left side of the KFM window that displays a hierarchical listing of the file-system directory tree as shown in Figure 4-5. Repeat the same command to remove the tree panel from the KFM window.

![](img/8dd43d91b80664e771e0c0a824d7392d_91_0.png)

KFM’s tree display uses a collapsible outline format to show the nested directories and subdirectories that make up your computer’s file system. The arrowhead symbols to the left of each directory name enable you to expand or collapse the directory tree to show or hide the subdirectories within a given directory.

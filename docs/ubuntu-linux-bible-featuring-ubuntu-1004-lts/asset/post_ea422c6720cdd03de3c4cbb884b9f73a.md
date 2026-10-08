
# Part II: Ubuntu for Desktop Users

In addition to its speed and search capabilities, Tracker provides some cool features such as the ability to tag files so that you can find them later by searching for the tag, and provides some automatic capabilities to expand your searches using the root(s) of your search term(s)(known as stemming), increasing the chance of finding what you're looking for.

# Note

If you don't like Tracker or Beagle, you will still have plenty of options. Recoll is another excellent package (that is powerful and relatively easy on CPU resources). Strigi (http://strigi.sourceforge.net/) is a well-known desktop search application that is used on many KDE systems. The folks at Google are not at the wheel, either—they offer DEB packages for the Linux version of their application as part of their Desktop package, available at http://google.com/linux.

Tracker is written in C, and consists of a daemon that indexes your files, a graphical configuration, several command-line and graphical utilities that make it easy to query and monitor the Tracker daemon and its index. The easiest way to query is by installing its desktop app and selecting the Magnifying Glass icon in the upper GNOME panel, as discussed in more detail later in this chapter. (See the section later in this chapter titled "Customizing Panel Controls" for information on installing this aspect.) Tracker can be queried from the command line, which makes it handy for use in scripts.

Because of the number of desktop search solutions available, none of these are installed by default on an Ubuntu system. I suggest that you give Tracker a try by installing both the tracker-search-tool package (which installs Tracker and a GNOME front end) and the tracker-utils package (which installs command-line tools for accessing Tracker)

# Searching with Tracker

After installing the Tracker packages, the Tracker daemon, trackerd, is automatically started as part of each Ubuntu user's GNOME login session. By default, Tracker automatically searches and indexes all the files in your home directory. Once Tracker completes its initial scan of your files and directories, you can search the Tracker index in one of four basic ways:

- From the Tracker applet, which starts the Tracker Search Tool
- From the tracker-search-tool application, which you can start from the command line, or by selecting the Accessories menu's "Tracker Search Tool" menu option, or by creating a desktop launcher for this application
- From the command line using the tracker-search command. This tool is part of the tracker-utils package.
- As part of the Desktop app panel tool

Tracker provides its own panel applet that starts once the Tracker daemon is running. You can click its icon, a magnifying glass, to start the Tracker Tool, as shown in Figure 5-32.

However, the Deskbar panel applet, discussed in a later section, is the easiest way to submit a query to Tracker and other search sources at the same time.

# FIGURE 5-32
Initiating a search in the Tracker panel applet

![](img/1a233c34336fbf5a85d6eb785e401709_214_0.png)

Pressing Return then automatically starts the graphical Tracker Search Tool application with these as the search terms, as shown in Figure 5-33.

As you can see from Figure 5-33, a Tracker locates items whose filenames, pathnames, or content match the phrase that you're searching for. Double-clicking on any of the search results shown in the Tracker Search Tool window will open that result in the application with which files of that type are associated.

# Part II: Ubuntu Desktop Users

FIGURE 5-33

Search results in the Tracker Search Tool

![](img/1a233c34336fbf5a85d6eb785e401709_215_0.png)

The summary line above the list of matching items shown in Figure 5-33 lists the available matches for the search term Ubuntu. If you have a large number of search results, various results are located, the icons in the Categories section of the Tracker Search Tools can help you determine where are. Default categories include: All Files, Folders (a view of the folders in which search results were found), Documents (PDF, HTML, Tex, and related files), Images (images in various formats that match your query), Music (audio files in various formats that match your query), Text (text files only), and Development (source code in various languages, Makefiles, etc.).

Once started as part of the GNOME login session, the Tracker daemon automatically runs in the background, continuously checking for new files in the directories that it is monitoring, indexing new files as they appear, and updating the index entries for existing files when you modify them.

# Configuring Tracker

Tracker is a very powerful and flexible desktop search application whose behavior can be configured using the Tracker Preferences application. Per-user configuration information for Tracker is stored in the file ~/.config/tracker/tracker.cfg, which can be edited (carefully) using a text editor, or automatically by using the Tracker Preferences application. You can start the Tracker Preferences application from the command line (by executing tracker-preferences command) or by selecting the System Preferences -> Search and Indexing menu item. (This menu option is only available after you have installed the Tracker packages.) Figure 5-34 shows the initial dialog that displays when you start the application.

# FIGURE 5-34
Configuring the Tracker Search Tool

![](img/1a233c34336fbf5a85d6eb785e401709_216_0.png)

The different tabs in the Tracker Preferences application enable you to configure different aspects of how the Tracker daemon interacts with your system. These tabs are as follows:

- **General**: Enables/disables indexing and the delay after which indexing begins once you log in. This tab also enables you to set the language used when stemming, which is a mechanism for locating related words by identifying common roots, and enables you to configure how the Tracker daemon behaves on laptops that are running on battery power.
- **Files**: Lets you configure the directories that are indexed by the Tracker. This consists of two sets of directories—those that are indexed by the Tracker and those that are simply monitored. The settings on this tab also enable you to configure whether the Tracker daemon generates a thumbnail for each file (enabled by default), whether the Tracker daemon indexes file contents (disabled by default), and the maximum amount of text and words that should be in each file

# Ubuntu for Desktop Users

- **Ignored Files**: Enables you to identify directories and wildcard patterns that it will not index. For example, you can disable indexing anything by entering `/home/username/music` in the "Ignored Paths". To add a new path or file pattern to ignore, click Add beside the appropriate text area, enter the path of the file, and press Return. To remove an existing one, highlight it and Remove. or `*.mp3` to the Ignored File Patterns.
- **Email**: Enables you to specify indexing of e-mail stored in mbox format used by mail clients such as Evolution.
- **Performance**: Enables you to configure how the Tracker daemon operates on your system to minimize its impact. Options include Throttling (reducing the amount of CPU that the Tracker can use), Resource Usage (the amount of memory that the Tracker uses), and Index Limits (how the Tracker daemon handles merging entries)

As you can see, the configuration options provided by the Tracker Preferences give you a lot of control over Tracker's performance and behavior. In all in, find Tracker to be the best of the desktop search applications. However, one of the reasons for this is that Tracker is nicely complemented by other search mechanisms that are provided as part of the GNOME desktop in the GNOME Deskbar applet, which is described in the next section.

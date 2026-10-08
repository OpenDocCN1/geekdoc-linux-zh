
4. The Search tab has two separate sections. In the How To Search section, you can choose from two different settings: Find Partial Matches and an option to disable searching from the index.

The two settings here that you really want to pay attention to are the sub-folder search and natural language search options. The default settings are good for most users.

5. The final section—When Searching Non-indexed Locations—specifies what to do with compressed files and system folders that are not indexed or when index search is turned off. I leave these blank to speed up searches, but I strongly suggest that you do not turn on the compressed file option; it causes your searches to take forever and makes your hard drive go crazy with activity. Unless you have an SSD hard drive, stay away from these options.

6. When you are finished tweaking the search options, click OK to save your changes. You might have to reboot for all settings to start working.

## Customizing the Indexing Service

The indexing service runs in the background and reads and indexes your files when your computer is idle to speed up searches. This works by reading all the files and storing search keywords and other information in a single database that can be easily read instead of having to read all the file information again every time you perform a search.

In Windows 8, the scope of the indexing service is limited to the user folders by default. If you use search a lot, you might want to tweak the folders and types of files that are indexed. The following steps help you customize which folders are indexed as well as the file types so that you can control what is indexed and what is not:

1. Open the Start screen, type **Performance Information**, and then select the Settings filter. Run Performance Information and Tools.
2. After Performance Information and Tools loads, click **Adjust Indexing Options** on the left menu. When Indexing Options load, all the locations the indexing service is currently monitoring are displayed.
3. The Indexing Options window opens. First, tweak where the indexer looks. Click **Modify** and then click **Show All Locations** on the Indexed Locations window. Next, navigate through the list of your drives and folders, and simply check the boxes for the folders you want to be indexed. When you are finished, click **OK** and the indexer goes to work indexing the new locations.
4. Modify the file types that the indexer indexes. You can do this back on the Indexing Options window. This time, click the Advanced button and then click the File Types tab.
5. Scroll through the list of file extensions and select the file type that you would like to modify. Then, check the box and pick how the file should be indexed in the following section. If your file type is not listed, type the file extension in the box at the bottom of the window, as shown in Figure 9-3, and click Add to add a new extension.
6. When you are finished, click OK and then Close to exit the indexing options.

![](img/ea75090cfee8ac890f64c8c4f62f7285_150_0.png)

Figure 9-3: Add file extensions you want to be indexed.

Because the indexing service runs only when the computer is idle, it may take up to a few hours before your new files, folders, and file types are added to the index and show up in the search results.

## Customizing the Ribbon

The ribbon interface in File Explorer provides a new way to navigate the interface. First appearing in Microsoft office, the ribbon was intended to make it easier for users to access hard-to-find features. A similar version of the ribbon was included in File Explorer for the same reason, to make it easier to use. The next two sections will help you customize how the ribbon appears and the quick access menu.

### Visibility

Show the ribbon or collapse it and hide it from view. This is one of the more difficult preference questions. Even the folks at Microsoft took some time to make up their minds. For most of the preview builds of Windows 8, the ribbon was displayed by default but was hidden in the final release builds.

If you like minimalist user interfaces without distractions, hide that ribbon right away. But if you like having all of your options easily visible, the ribbon may be for you. Either way, changing the default behavior is very simple—just click the up or down arrow on the far right of the window next to the help icon. Your setting is automatically saved for the next time you open File Explorer.

### Quick Access Toolbar

Every Microsoft ribbon includes a quick access toolbar in the title bar of the application window. This toolbar provides you with easy access to your most popular items. In Windows 8 File Explorer you can add the following items to the toolbar:

- Undo
- Redo
- Delete
- Properties
- New Folder
- Rename

You can also select an option to display the quick access toolbar below the ribbon instead of on top.

You can access all of these options by clicking the down arrow to the right of the quick access toolbar on the title bar of any open File Explorer window. Then, check the item you want to display by selecting it.

### Modifying File Associations

Every time you click a file, Windows checks the registry to find the default program to open the file. Then, Windows loads that application and tells the application which file to open. This is something that you encounter almost all the time when you are using your computer. Often, when you install many programs on your computer, programs start to compete over which is going to be the default program to open a file.

One of the most common situations for this is when you install a bunch of similar applications. For example, I primarily use WinAmp for playing my music. When Apple releases a new version of iTunes, however, I usually install it to check out the new features. The next time that I try to play a CD or listen to an MP3, the music always opens in iTunes. My file association for my music has been stolen by iTunes. How do I take control of my file associations again? The following two sections show you how you can customize the default launch application for any file type on your computer, as well as how your file types look.

Windows Explorer uses information stored in the registry to find out what application is used to open a specific file type. This information is stored in the **HKEY_CLASSES_ROOT** section. With the Registry Editor, it is possible to browse to that key and find the file type that you want to change and edit some keys. However, there is a better way to do this in Windows 8.

Windows 8's Default Programs utility enables you to change file association information without having to deal with the registry class ID. Just follow these steps to change the default launch app for any file type:

1. Open the Start screen, type **Default Programs**, and hit Enter.
2. When the Default Programs utility loads, select **Associate A File Type Or Protocol With A Program**.
3. Scroll through the list and select the file type you want to change, as shown in **Figure 9-4**.
4. Click **Change Program**.
5. The program to which you want to change may be on the default Open With list. If not, just click **More Options**, scroll down, and then select **Look For Another App On This PC**.
6. Click **Close**.

Your changes to file launch apps are activated immediately after you click Close to save your changes. Now you know how to fix your file associations when apps attempt to hijack them.

![](img/ea75090cfee8ac890f64c8c4f62f7285_153_0.png)

**Figure 9-4:** Change your file associations.

## Customizing the Context Menu

What is the context menu? It's the menu that pops up when you right-click anywhere on your computer. Over the years, these menus have become more and more useful. However, with the extra entries in the context menu, they can become cluttered with options and features that you just don't need. These next few sections show you how to get your menus back under control as well as how you can take advantage of the new features to make your own context menu entries.

I start off by teaching you how to remove items from the context menus and then cover how to add and customize the menu components.

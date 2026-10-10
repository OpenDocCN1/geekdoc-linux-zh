
## Finding a File by More Complex Criteria

There are many categories you can use to make your search more precise. The more you know about the file, the better are your chances of finding it.

- **Date modified**: Here, you can specify that you only want to see files that were last touched in a given period of time or since a specified number of months or days ago.
- **File type**: If you know that the file was of a special type (e.g., a tar/gzip archive or a jpeg picture), you can tell KFind to find only this type of file.
- **Text string**: You can specify text that the file must contain.
- **Size**: If you know the file size, you can limit your search in this regard as well.

## Using Multiple Desktops

Using multiple desktops helps you organize your work. You can place your programs on different desktops, and name the desktops so you know what you do there. This increases and optimizes your workspace. It also helps you when you are surfing the net instead of doing your work and your boss comes in. But, of course, this is rare—at least in the office where I work.

You can switch between desktops by clicking the desktop buttons on the KDE panel. If you want to rename them, you can do so by double-clicking them.

You can use windows on multiple desktops. If you want to have a window present everywhere, just click the sticky button on the top-left of the window. To send a window to another desktop, click the title bar with the right mouse button, choose To Desktop, and select the desktop where you would like the window moved.

## Quitting KDE

To quit working with KDE, you can use the Logout entry in the Application Starter menu or the corresponding button on the panel. You will be asked if you really want to quit KDE. Quitting will close all windows and return you to your console or display manager. For information on how programs can save your work during logout, please read about the Logout button in the “Panel” section earlier in this chapter.

# All About Your Desktop

> *Grandma, what big eyes you have.*
> —Little Red Riding Hood
>
> *The better to see you with.*
> —The Wolf

The more you see, the more efficiently you can use your desktop. KDE gives you the opportunity to make the desktop look and work the way you prefer, enabling you to work faster and more productively. It even gives you the opportunity to be warned if a wolf is trying to eat you, or (if you happen to be a granny) alert you when Little Red Riding Hood is on her way to bring you the goodies. Now that’s service.

## The Autostart Folder

Before I discovered the Autostart folder, my daily startup routine with KDE consisted of starting KDE, starting KEdit, starting kvt, starting Netscape, and starting kscd. This took time I could have spent better. As of the first Beta release, native KDE programs left open at the end of a session will save their state and reappear when you login again, but there are some programs (like Netscape) that will not. You can use the Autostart folder for these programs.

To launch programs when KDE is started, do the following:

1. Open the Autostart folder found on the upper-left corner of your desktop.
2. Open a file manager window containing the program you want to add. If you do not know how to do this, see “The File Manager Screen” section earlier in this chapter.
3. Drag-and-drop the desired program from its source folder into the Autostart folder. When asked, choose Link to create a symbolic link instead of a full copy. This saves a great deal of disk space.
4. Repeat this step for every program you want started when KDE is launched. Of course, you may select applications not native to KDE, including Netscape, tin, pine and many others.
5. Restart KDE.

Your programs should now launch automatically when KDE is restarted. If you want to add something special (e.g., you want to see a certain Web site when your system goes up), read the “Using Templates” section later in this chapter. The procedures described there work for any folder, so you can also apply them to the Autostart folder.

## Adding Programs and Shortcut Icons to Your Panel

The KDE panel is not limited to the setup you find right after installing KDE. The KDE panel is designed to be extended, and there are two ways of doing that: Adding new programs and adding shortcut icons.

### Programs

To add your favorite programs to the KDE panel, you must use the KDE Menu Editor. To start it, use the Application Starter and choose Utilities ➔ Menu Editor. A window containing an empty button will appear. To change it, click it using the right mouse button and choose Change. Next, you should see another window with various options you can set. The Type dropdown menu contains some types of links you can create. Choose Application. Now choose the Name field and enter the description that will appear in the Application Starter. For example, you can type Netscape Communicator. Next, click the large and the small picture using the left mouse button and Select an Icon for the Application. In the Comment field you can optionally enter a remark about the application. Be sure to choose a helpful comment, because it will appear as tool-tip in the Application Starter. For Netscape, you might enter **WWW-Browser with Mail and News software**.

If not already selected, choose the Execute tab and enter the Execute field. Here, you must type the complete path to your application, for example `/usr/local/netscape/netscape`. Set the Working Directory to a value that makes sense, such as `/usr/local/netscape`. If your application runs in a terminal, you must select Run In Terminal and specify the Terminal Options. The terminal options are the command-line switches of `kvt`; you can see them by using

```
kvt --help
```

in a terminal window. After you have made all the adjustments needed, choose the Ok button and select File ➔ Save from the main menu. Next, restart your panel by choosing Panel ➔ Restart from the Application Starter. You should now find a new entry Personal with the new menu entries.

### Shortcut Icons

Although KDE is much more comfortable than the average Unix window manager, everyone wants a solution for a one-click way to start a program. Later, you will learn how to create links and files on your desktop, but this also has some disadvantages: sometimes all of your desktops are filled up with windows, and you cannot reach your icons without minimizing all of the windows that cover them. For commonly used programs, you can minimize this problem and speed access by creating shortcut icons on the KDE panel.

To create a shortcut on the KDE panel, do the following:

1. Click the *Application Starter* and choose Panel ➔ Add application.
2. You will see the top level of the Application Starter again. Go through the menus to find the program for which you want to create the shortcut, such as “Home Directory” or “kvt.” Click the program you want.

A new icon will appear on the KDE panel. Click it, and the program will start. If you want to move the icon, click it using the right mouse button and choose Move. Move the icon to the position you want and press the left mouse button. If you wish to remove the icon, click it using the right mouse button and choose Remove.

## Creating New Files on Your Desktop

Your desktop can be an efficient place to work. Every time you start KDE, you can see the complete files, folders, and URLs that you often use.

There are two ways to create and edit files on your desktop. In any application, you can say that you want to save your work in the desktop subfolder of your home directory. For example, my home directory is */home/stupiddog*, so my desktop directory is */home/stupiddog/Desktop*. Everything you save there will be put on your desktop.

If you want to move existing files to your desktop, the best way to achieve this is to use the K file manager (kfm). Open a file manager window and drag the files you need to your desktop. You can choose to copy them if you want to keep all your common stuff on the desktop now, or you can create symbolic links to the real files. Everything you change in the link files will be automatically updated in the originals. For more information on how to use drag-and-drop and the file manager, see the “Moving Files with Drag-and-Drop” section earlier in this chapter.

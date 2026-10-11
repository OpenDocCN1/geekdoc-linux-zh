# # Your first steps in Linux

Discover all the core skills you need to start using Linux Mint.

When you boot into Mint for the first time, you'll find it looks very similar to Windows. The default desktop is called Cinnamon, and is structured in a similar way to the Windows desktop: there's the equivalent of the Start menu, Taskbar and Notification area at the bottom of the screen, with desktop icons providing shortcuts to key locations.

Click the Menu button and up pops a menu with easy access to all your programs, grouped into categories. Speed things up by typing the first few letters of the program you're looking for into the Search box and it'll appear in the list of results, just one click away. On the left-hand side of the menu you'll see some rather handy shortcuts — at the top key programs like Firefox (web browser), Software Manager (for finding and installing new applications), System Settings (the Mint equivalent of the Control Panel). Terminal and Files manager. At the bottom are buttons for locking, logging out and shutting down or restarting your PC.

Add your own shortcuts by dragging and dropping items into the list from the desktop or right-hand side of the menu. You can also pin shortcuts to the panel (Mint's equivalent of the taskbar) at the bottom of the screen too — just right-click and choose 'Add to panel' to do so.

Mint's panel is actually more configurable than Windows' Taskbar — you'll see lots of useful options in the bottom right-hand corner, and you can customise these, plus add new panels, simply by right-clicking the panel and selecting from the options on show.

# ## Access drives

Mint works with a wide range of file systems, which means your existing NTFS and FAT32 partitions are visible from the moment you boot into the desktop. The best place to access your drives — and browse your files generally — is with Mint's equivalent of File Explorer. It's named Nemo, and is accessible via the Files shortcut you'll find on both the pane and the Menu. You can also open it by double-clicking the Computer or Home icons on the desktop.

The layout is similar to Windows 10's File Explorer, with your files displayed in the right-hand pane, and a series of shortcuts to key locations on the left. You can also bookmark favourite folders (select the folder in question and choose Bookmarks > Add to Bookmarks) for easy access from here too. Nemo also supports tabbed windows, which work in a similar way to your web browser, albeit with folders. Press Ctrl+T to add additional tabs, which make it easy to switch between multiple drives and folders without cluttering up your desktop with lots of open windows. You'll see an option for accessing your network in Nemo — click the Network shortcut in the left-hand pane to find other computers, and have your username and password ready if necessary

You should find your PC's hardware has been — for the most part — automatically detected and set up. Click the

![](bbox=[0.12, 0.45, 0.55, 0.62])

The Nemo file manager works in much the same way as File Explorer does in Windows 10, so you won't struggle to browse your hard drives.

# ### Share data with Windows

If you plan to continue using Windows and Ubuntu alongside each other, it pays to set up a dedicated **data** partition, then make it easily accessible to both operating systems. Use GParted from the Mint installer to set up a NTFS partition, then boot into Windows and browse to your user folder. Right-click each key data folder — Documents, Pictures etc — in turn and choose Properties > Location, then point them to the equivalent folder on your new data partition, moving the data across when prompted.

You should also disable hibernation in both Windows and Linux — data written to the shared partition while one OS is in hibernation may be wiped when that OS is next woken up. In Windows, open a Command Prompt (administrator), type `powercfg /hibernate off` and press Enter to enable this setting.

Once done, switch back to Mint. Disable hibernation by opening System Settings > Power Management and ensuring 'Never' is selected under the second drop-down menu. Next, open the Disks utility via the Dash. Select the disk containing the data partition in the left, then click on the partition on the right and make a note of where it's mounted (this tends to follow the format, /media/ <username> / <partition name>). Finally, go to www.ubuntu-tweak.com and install the Ubuntu Tweak (yes, parts of it work in Linux Mint!). Open it from the Administration section of the Menu, then select Admin > User folders.

![](bbox=[0.64, 0.73, 0.9, 0.87])

Share data between Windows and Linux using a dedicated NTFS partition. Folder to manually point your data folders to the folders stored on the data partition you created and identified earlier.
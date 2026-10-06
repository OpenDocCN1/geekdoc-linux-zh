# The User Menu

So far we have avoided discussion of the mysterious F2 command. This is the user menu, which may be Midnight Commander's most powerful and useful feature. The user menu is, as the name suggests, a menu of user-defined commands.

When we press the F2 key, Midnight Commander looks for a file named .mc.menu in the current directory. If the file does not exist, Midnight Commander looks for ~/.config/mc/menu. If file does not exist, then Midnight Commander falls back to a system-wide menu file named /usr/share/mc/mc.menu.

The next thing about this is that each directory can have its own set of user commands, so that we can create commands to the contents of the current directory. For example, if we have a "Pictures" directory, we can create commands for processing images; if we have a directory full of HTML files, we can create commands for managing a web site, and so on.

So, after we press F2 the first time, we are presented with the default user menu that looks like this:

| Left | File | Command | Options | Right | Size | Modify time |
|---|---|---|---|---|---|-|
| ^n Name | | UP-DIR | Modify time | ^> Name | Size UP-DIR | Feb 3:24 |
| .cache | @ | User menu edit the dont file | | | 3:30 | 3:30 |
| /config | 0 | Edit a report and send it to root | | | 3:30 | 3:30 |
| /documents | | Call the info help browser | | | 3:32 | 3:32 |
| /Pictures | | | Compress the current subdirectory (tar.gz) | | | 3:32 | 3:32 |
| /tmp | | | Compress the current subdirectory (tar.bz2) | | | 6:45 | 6:45 |
| .bash_h | 3 | Compress the current subdirectory (tar.xz) | | | 3:24 | 3:24 |
| .bashrc | | | | | | 3:54 | 3:54 |
| .lessmap | | | Inspect grid's newsfetch | | | 3:24 | 3:24 |
| .profile | | | Strip headers from current newsarticle | | | 3:54 | 3:54 |
| .viminfo | | | Copy file to rename host | | | |
| y | | | Gzip or bzip2 current file | | | |
| b | | | Bzip2 or bzip2 current file | | | |
| UP-DIR | | | | | | |

```
Hint: M-I will want to execute programs and see the output in the viewer.
midnightlinux $ 1Help 2Menu 3View 4Lit 5Copy 6GenMay 7Ndir 8Delete 9Quit 10Quit
```

# The User Menu

The default user menu contains several example entries. These are by no means in stone. We are encouraged to edit the menu and create our own entries. The menu is ordinary text and it can be edited with any editor, Midnight Commander provides
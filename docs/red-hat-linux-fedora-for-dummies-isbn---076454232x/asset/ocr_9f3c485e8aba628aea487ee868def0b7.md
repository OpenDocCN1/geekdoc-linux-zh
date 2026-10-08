![](bbox=[0.048, 0.106, 0.166, 0.19])

# # Delving deep into color depth

Color depth, the number of colors your system can have active on the window at any one time, is loosely a function of both the amount of video memory contained by your system and the window resolution.

If your system has a small amount of memory (such as 1MB), your screen can have a resolution of 1024 x 768 pixels (dots) with 256 colors (8 bits) on the screen at one time. If your system has 2MB, you can have 64K colors (16 bits) on the screen at the same time at the same resolution. If you have an older video board with a small amount of video memory but some additional video memory sockets, you may be able to upgrade the amount of video memory on the video card.

If you have only 1MB and want to see 64K colors on the screen at one time, you can reduce your resolution from 1,024 x 768 to 800 x 600 pixels. If you want true color (24 bits), you can set your resolution to 640 x 480 pixels. The picture you're viewing takes up more of the screen, but color depth versus resolution is a trade-off you can make by choosing the right options.

When you want to display an image and the color depth isn't correct, nothing drastic happens. The picture may look lackluster or not quite normal. X has an interesting capability to have virtual color maps, which allow the active window to utilize all the colors of the bits of color depth, even if other windows are using different colors. When this option is turned on (as it is with the Red Hat distribution on this book's companion DVD-ROM), the various windows turn odd colors as your mouse moves from window to window, but the window that your mouse activates is shown in the best color available. With newer video cards and larger video memories, which allow for true color at high resolutions in every window, this option is less useful.

+   5. Click the OK button and the Display Settings window closes.

An Information window opens, informing you that you need to log out and log back in to make the changes take effect.

Log out and log back in to make the changes take effect.

![](bbox=[0.129, 0.732, 0.208, 0.807])

You can also restart X in emergencies (for example, if it freaks out) by pressing Ctrl+Alt+Backspace. Your current X session is stopped and eventually restarted. You can then log back in.

# # Creating User Accounts with the Red Hat User Manager

If you have cause to add new users (if you have a home network, for example) or you forgot to create a nonroot user during installation, this section
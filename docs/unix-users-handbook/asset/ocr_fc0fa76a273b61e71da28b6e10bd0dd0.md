**xterm** might be a better choice for terminal emulation.

Automatic Saves

Some applications automatically save data at periodic intervals. Although this feature can be beneficial, you need to evaluate its effect in light of performance. If the application is central to your users' work, fine, but if not, you might want to disable the automatic save feature.

Scroll Buffers

Large scroll buffers in terminal emulators can be a real convenience, but they can also take up a lot of RAM. Even modestly sized scroll buffers, when multiplied by three or four terminal emulators, consume a lot of RAM.

Background Bitmaps

Avoid large bitmaps; they increase the X server size. Especially avoid switching large bitmaps frequently within a session. If you are hunting for a new background, be sure to restart the X server after you've found the one you want and have included it in the proper **sessionrc** file. The most efficient bitmaps are small ones that can be repeated to tile the background.

Front Panel

Reconfigure the front panel to minimize the number of buttons. Keep just enough to meet user needs. This tactic decreases the workspace manager size in RAM and speeds login and logout.

Pathnames

Whenever possible, use absolute pathnames for bitmap specifications. Although this approach decreases the
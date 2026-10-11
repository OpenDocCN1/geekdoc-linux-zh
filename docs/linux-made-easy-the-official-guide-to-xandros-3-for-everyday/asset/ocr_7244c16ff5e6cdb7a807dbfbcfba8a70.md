2. libsd-gfx1_2 (package size 38.16 KB) Remove Status: installed Description: drawing and graphical effects extension for SDL 3. libsd-image1_2 (package size 24.32 KB) Remove Status: installed Description: image loading library for Simple DirectMedia Layer 1.2 4. libsd-mixer1_2 (package size 117.83 KB) Remove Status: installed Description: mixer library for Simple DirectMedia Layer 1.2 5. libsd-net1_2 (package size 5.60 KB) Install Status: installed Description: network library for Simple DirectMedia Layer 6. libsd-sound (package size 42.52 KB) Remove

Figure 18-14: Installing the dependencies for Njam via Xandros Networks

# 18A-3: Running Njam

Once the three dependency files are installed, the only thing you really have to do is run Njam. Because there is no menu launcher for you, However, you will have to run it via the Run Command window (Launch ▶ Run Command). Once the window appears, type /home/yourusername/njam /njm -w in the Command box in that window (being sure to place your username in the appropriate spot within the string). After you've done that, click Run, and Njam will start right up.

In case you're wondering, that -w flag (you'll learn a bit more about flags in Chapter 20) causes Njam to open in a window (hence the w) rather than in full-screen mode. This is important, since running Njam in full-screen mode (without the -w flag) might cause some machines to freeze and then log out, which isn't something you would normally want to happen. No damage done if it does, of course, because all you have to do in that case is log in again, but why bother, right?

# 18A-4: Creating a Menu Launcher for Njam

Rather than typing in a command each and every time you want to run Njam, you might like to create a menu launcher for it in order to make things a tad more convenient. You can also use the same process to add menu launchers for any other applications you need, so it is indeed worth having a go. Here are the steps for creating a menu launcher for Njam:

+   1. Close the still-open Njam window by pressing the ESC key.
+   2. Next, go to the Launch menu and select Applications ▶ System ▶ Menu Editor.
+   3. When the Menu Editor appears, click the + symbol next to Games and then the + symbol next to Arcade.
# CHAPTER 5

# Working with
X-Windows

Chapter 4, “Your First Session with FreeBSD,” briefly introduced the X-Windows system. In this chapter, we will look at X-Windows in more detail. The X-Windows system basically has two parts—the X-Server and the window manager. The X-Server runs on your system and provides a graphical framework for applications to use. The window manager determines how X-Windows looks and feels. In this chapter, you learn about these parts of the system in more detail and how to work about and customize the WindowMaker window manager.

# The X-Server

The X-Server is the underlying framework that allows graphical applications to run. By itself, the X-Server is not very useful because it contains no window-management functions. Figure 5.1 shows an X-Server running with no window manager.

Several applications are running in the X-Windows session shown in Figure 5.1: an xterm, a clock, a calculator, and the GIMP image-processing program used to take this screenshot. Notice that the windows have no title bars and borders. They are not resizable or movable, and they cannot be minimized or maximized. Obviously, this lack of flexibility makes for a pretty useless graphical user interface. This is where the window manager comes in.

# IN THIS CHAPTER

+   - The X-Server
+   - Windows Managers
+   - The WindowMaker Window Manager
+   - Working with Windows
+   - WindowMaker Menus
+   - Working with the Dock
+   - Customizing WindowMaker
+   - The Preferences Utility
We showed several elementary sample client application programs for the X Window System, coded to call upon three standard and very common toolkit libraries, Xlib, XCB, and Qt. We stressed the two most important aspects of client application program creation for the beginner:

+   - A client application program has two parts: a data generation part that uses code in C, C++, or another high-level programming language to produce the numbers, text, files, and data structures; and a user interface (UI) part which produces the actual graphics that display the data generation part.
+   - A client application program is made up of initialization, event–request loop, and cleanup sections.

We also showed many detailed examples of the toolkit code itself and what the code accomplished in the context of the sample programs.

# QUESTIONS AND PROBLEMS

+   1. Give definitions, in your own words, for the following terms as they relate to the X Window System: window system, window manager, desktop manager, client, server, focus, iconify, maximize, minimize, xterm, application user interface, management interface.
+   2. Which X Window System window manager is used on your computer system? How can you identify and recognize which window manager you are using by default?
+   3. Make the following changes to your ~/.fvwm/config file to set DeskTopSize to 3×3. What effect does that have when you restart FVWM? Then, use the Root menu>Fvwm Simple Config Ops fly-out menu to change the focus of Click to Focus. What effect does that have?
+   4. Which command allows another user to have their windows displayed on your screen under the X Window System? What would be the advantages of doing this? What would be the disadvantages of doing this? Explain why this is even possible at all under the X Window System.
+   5. Identify the xterm options that are set on your computer system. What is the default size of an xterm window? What is the default background color for an xterm window? What do you think are the most useful xterm options for you?
+   6. Use the AppCafe on a PC-BSD system to download and install another window manager, such as Awesome or FVWM-Crystal. Then login and invoke that new window manager and compare its operability, functionality, and ease of use to FVWM. Which window manager do you like best and why?
+   7. a. When you hold down the left-most mouse button when the screen cursor is in the root window of your X Window System display, what appears on your screen?
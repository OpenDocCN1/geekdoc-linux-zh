A workbench window can have several separate *perspectives*, only one of which is visible at any given moment. Each perspective has its own views and editors that are arranged (tiled, stacked, or detached) for presentation on the screen, although some may be hidden. Several different types of views and editors can be open at the same time within a perspective. A perspective controls initial view visibility, layout, and action visibility. You can quickly switch perspectives to work on a different task, and can easily rearrange and customize a perspective to better suit a particular task. The platform provides standard perspectives for general resource navigation, on-line help, and team support tasks. Other plug-ins provide additional perspectives.

Plug-in tools may augment existing editors, views, and perspectives to:

+   - Add new actions to an existing view’s local menu and tool bar.
+   - Add new actions to the workbench menu and tool bar when an existing editor becomes active.
+   - Add new actions to the pop-up content menu of an existing view or editor.
+   - Add new views, action sets, and shortcuts to an existing perspective.

# **Installation**

There are two parts to Eclipse; Eclipse itself and the Java Runtime Engine (JRE). Download Eclipse from eclipse.org. There are several versions to choose from. Since we are interested in C development, get the Eclipse IDE for C/C++ Developers.

You can put Eclipse wherever you like. I chose to install it in /usr/local. After untarring, you will find a new subdirectory called, not surprisingly, eclipse/.

Since Eclipse is written primarily in Java, you’ll need a JRE to support it. Most contemporary Linux distributions install a JRE by default, but it may not be compatible with Eclipse. The version supplied with CentOS 7 works fine. If necessary, download the latest version from Oracle (formerly Sun Microsystems). The download is available either as a binary executable or an RPM package. Copy it wherever you like and execute it. /usr/local is a good place. You will be asked to read and accept the Binary Code License Agreement for the Java SE runtime environment (JRE) version 6. You will need to add thebin/ directory of the newly-installed JRE to your PATH.

That’s it! Eclipse is installed and ready to go. In a shell window, cd to the eclipse/ directory and execute ./eclipse. From anywhere else, enter the complete path to the eclipse executable. Or just double-click it in a K Desktop Environment file manager window.
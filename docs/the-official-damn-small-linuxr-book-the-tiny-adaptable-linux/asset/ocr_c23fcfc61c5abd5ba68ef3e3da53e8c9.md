Notice that the .tar.gz and the .uci extension-types are both installed under /opt. In fact, it is usually easy to convert from .tar.gz to .uci. Similarly, both .dsl and .unc extensions are installed under /. It is also easy to convert from .dsl to .unc. Later, I will discuss the DSL tools to help in building and converting extensions.

In the rest of this chapter, I will demonstrate how to create the four MyDSL extension types. I will use the common application of Zile. Zile is an Emacs-like command-line editor.

# COMMON ELEMENTS TO ALL MYDSL EXTENSIONS

Let's begin by discussing the common elements to all DSL extensions: the menu and icon. Being a live CD-ROM, and therefore not inherently a multiuser system, means the extensions are built for the default user ds1. Because you use a minimal window manager (as provided with Fluxbox) and a customized icon manager (called xtdesk), you need to provide your own menu and icon for each extension you create. Menus and icons are optional, but most users expect at least a menu item to be included.

> NOTE
> If the application is console based and commonly requires command-line options, a menu item is not very useful. The menu item is not required.

> NOTE
> Loading a Debian application using the standard Debian procedures does not provide a menu item or icon. Much of the Debian menu and icon supporting infrastructure was cut to reduce the size of DSL.

All other aspects of an extension—the actual files, directories, libraries, and paths—are common to any Linux distribution given the existing kernel, modules, and libraries.

# The Menu Element

The menu for a MyDSL extension is actually a fragment of the Fluxbox standard. This menu fragment is a simple text file and is created under the directory /tmp/myds1.menu. It must be the same name as the base extension name and must
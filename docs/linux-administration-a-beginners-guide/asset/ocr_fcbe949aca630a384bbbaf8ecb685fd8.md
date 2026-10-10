As users, we means that picking an environment over the other has the possibility of looking us out of getting to use certain applications. As of this writing, this hasn't been too much of an issue. In fact, there is work going on between both groups on improving the level of compatibility between them. That leaves us with having to make a choice. If you aren't sure about what you like better, try both. See which you like better rather than depend on the opinion of some Web page (or even worse this author)! What I use is irrelevant. What you like is what matters. And that's that having two competing systems is all about.

# ## ABOUT KDE

KDE is a desktop environment (the K Desktop Environment). It is slightly different from typical window managers that we have been describing. Instead of just describing how the interface should look, KDE also provides a set of libraries that, if used, allow an application to take advantage of some of the special features the window manager has to offer. This includes things like drag-and-drop support, standardized printing support, and so on.

The flip side to this technique of window management is that once an application is designed to run with KDE, it requires KDE in order to work. This is a big change to earlier window managers where applications were independent of the window manager.

From a programmer's point of view, KDE offers a library that is much easier to work with than directly working with the X interface. KDE also offers a standardized object-oriented framework that allows one set of tools to build on another, something that is not available with X-Windows alone.

For this section, we will assume that KDE has already been installed on your system. This is true for Caldera, since it only offers KDE, and, if you opted for using it during the install process, for Red Hat, too.

**NOTE:** For more details and information on KDE, visit their Web site at [http://www.kde.org](http://www.kde.org).

# ### Licensing Issues

Up until recently, there were some problems with the license restrictions imposed by the developers of the Qt library, which is what KDE is based on. This prohibited the commercial usage of KDE without paying fees to The Gnome Project started because of this restriction.

Recently, KDE's license was reversed. The revised license, known as the QPL, is now more open and does allow for commercial usage; however, it is different from the GPL and Berkeley-style licenses used by the majority of the packages that ship with Linux distributions. Like any documentation, it is worth taking a read if you think you may have issues with it.

You can find out more about this license by visiting KDE's Web site.
# Configuring X Fonts

# Real World Scenario

# Wayland: The Future?

An entirely new method of managing displays, known as Wayland (http://wayland.freedesktop.org), is being readiness as I write. Wayland is intended to address many of the problems with X, which suffers from a design dating back to the 1980s, before many modern video features became available. Thus, X is hobbled by legacy features such as a font model that's largely replaced by add-on font libraries.

Wayland-native applications won't use X at all, which will theoretically result in simpler application design, better speed, and fewer video problems, particularly for certain graphics-intensive applications. Existing Wayland applications will continue to run via an X server to be included in Wayland. Essentially, X will run as a process under Wayland, although this will be a stop measure.

The developers of major Linux distributions, including Fedora and Ubuntu, have expressed an intention to support Wayland, either as an option or as the default graphics system. The timetable for such a change is uncertain, though. Wayland has yet to be accepted by users; if Wayland presents unexpected problems, it may flounder. You should watch for future developments concerning this software.

# Configuring X Fonts

Fonts have been a long spot for Linux (or more precisely, for X). X was created at a time when font technologies were primitive by today's standards, although X has been updated in various ways to take advantage of newer technologies, these updates have been lacking compared to the font systems in most competing OSs. X's core system can be set up by the X configuration file. Alternatively, you can configure a font server—a program that delivers fonts to one or many computers using network protocols—to handle the fonts. The latest Linux font technology sets up fonts in a way that's more independent of X and produces more pleasing results, at least to most people.

> Some applications dont rely on either X or any other standard library to handle fonts; they manage their own fonts themselves. This practice is particularly common in word processors. If you configure your fonts as described here but find that an important program does not see the changes you've made, consult its documentation; you may need to tell the program where to look to use the fonts you've added.

![](bbox=[0.142, 0.763, 0.222, 0.803])
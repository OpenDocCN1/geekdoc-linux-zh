![](bbox=[0.258, 0.085, 0.742, 0.483])

# Desktop interprocess communication

Sometimes you want to control multiple applications from one authority. Or, perhaps you want to standardize on one programming language so that customizations do not need to be written in each of the various embedded languages. Many Linux-based applications support a form of interprocess communication, which allows you to control the application programmatically.

The GNOME developers originally used ORBIT2 (a highly optimized CORBA implementation), but lately, they have focused on D-BUS for future development projects.

DCOP the standard KDE Desktop Communication Protocol. You can use it for all kinds of KDE automation and scripting purposes. It is based on the Inter Client Exchange (ICE) protocol and uses UNIX sockets instead of method calls. It has its roots in a CORBA implementation, but it was completely redesigned for desktop needs because the KDE developers were not happy with the CORBA performance at that time. Let us take a closer look at DCOP, because this is a proven technology that is available today. You can also use DCOP for KDE applications running on the GNOME desktop.

> Figure F-1 Integrated DCOP development with Komander

326 Linux Client Migration Cookbook, Version 2
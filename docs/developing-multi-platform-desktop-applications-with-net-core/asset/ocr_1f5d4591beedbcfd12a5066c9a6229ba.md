# 8.5.2 GTK Install

As you understood GTK is a Linux native tool but need to be install on the others system (Windows and macOS). Since the third version the setup of GTK is not a simple binary to launch. The process for the install on Windows and macOS consists in the setup of a Linux emulated environment (the size used on disk for this environment could be as huge as an original ubuntu distribution).

GTK need to be installed on the machine you plane to deploy or test your GTK application too (at least the runtime). We will review in details how you can do this setup on each system.

# 8.5.2.1 On Windows (for the development station)

This description for the setup of GTK come from the gtk.org (see the references web sites) web site. This is the recommended procedure for performing the install of GTK on your Windows platform. Another solution is to build the GTK toolkit from the source code but it will require a prior installation of a C building environment (that’s not our purpose here).

# A) Install MSYS2

For the setup of GTK you will need to setup an environment for this type of application: mingw.

MingGW is the contraction of “Minimalist GNU for Windows”, it provides the Opensource environment for the development of application for Microsoft Windows.

MSYS2 is a project who provide a Unix like environment on a Windows station (mingwin). This project furnishes the foundation for the development of a GTK application on Windows, it will allow the setup of the GTK runtime and the tools (like Glade) you will need for developing your .NET Core 3 GTK application.
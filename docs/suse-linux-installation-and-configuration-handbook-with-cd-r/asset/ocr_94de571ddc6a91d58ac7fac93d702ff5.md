# Upgrading GNOME from Source

This process is similar to the one used with KDE, except for a few slight differences. One difference is that you have a lot more packages to compile. When you attempt to compile GNOME from source, it is advisable to remove the current version of GNOME if it was installed using RPM. So, the first thing you will want to do is use YaST to uninstall all the packages for GNOME from your system.

Installing GNOME from source is a bit more complicated than KDE. If you are not using the correct versions of all the libraries, GNOME might not compile or might act funny. This is why if you are doing this for the first time, it is advisable to download all the required packages and compile them. Then, when you do this again, you will know what you have on your system and can decide what to compile again.

You can get the source packages for GNOME from their site at http://www.gnome.org. Click Getting GNOME and then click Installing From Tarballs. The following are the absolute minimum required files:

+   - audiofile
+   - esound
+   - glib
+   - gtk+
+   - imlib
+   - gtk-engines
+   - ORBit
+   - gnome-libs
+   - libgtop
+   - control-center
+   - gnome-core
+   - mc

These are the absolute minimum packages you will need to compile to have a running GNOME system. You will need more packages as you attempt to compile more components. If you have a previous copy of GNOME installed on your system via RPM, please remove any RPM files for the above files before you compile them to avoid conflicts. The order in which you compile GNOME is very important. You have to compile the files in the same order as they are shown in the preceding list.

Compiling GNOME is no different from compiling KDE. Be sure you read the README files for every package for installation instructions. You use the exact same procedure—follow these steps:
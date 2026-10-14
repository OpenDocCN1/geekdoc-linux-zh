This will take quite a bit of time, depending on your machine's speed and amount of RAM. You should see lines scrolling by, which are source files being compiled to build KDE. After the lines stop scrolling and you are back at the prompt, and there were no error messages reported, you can start installing the package.

Install the package with the following command:

```
# make install
```

This will take some time, but not as much as the previous step. You will see lines scrolling very quickly this time. Your package is being installed in the default place for KDE, which is /opt/kde. This is okay because it's where SuSE puts KDE by default. It is good practice to run the command ldconfig after every compilation to make sure that any new libraries have been registered with Linux:

```
# ldconfig
```

That's all! The package is compiled and installed. You can remove the source directory now and start with another package. When you are done with all the packages, your new KDE will be ready to run. From then on, when you start KDE, it will tell you that a new version has been installed and that it will synchronize its files with it.

# Upgrading GNOME

GNU Network Object Model Environment (GNOME) is another powerful desktop environment similar to KDE. GNOME offers the user an attractive desktop, full of eye candy. The SuSE 6.2 full version comes with GNOME, but the evaluation version does not. SuSE offers RPMs for GNOME through its site for those who want to install it.

# Checking Your Version of GNOME

As with KDE, the first thing that you need to do is check the version of GNOME that you are currently running. To do that, simply click About in the GNOME menu. A window appears with information about the currently installed version of GNOME.

SuSE offers packages for GNOME. If there are any newly updated packages, you should be able to find them by following the instructions in the section “Upgrading SuSE Linux” at the beginning of this chapter. To check for the absolute latest version of GNOME, you will probably need to check its site at http://www.gnome.org. The GNOME site is very well-organized so it is easy to find what you want. If there is a new version of GNOME, you can find out by opening the page, as shown in Figure 7.8.
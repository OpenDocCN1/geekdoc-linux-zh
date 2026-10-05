# 19.6 Configuration

LyX and KLyX can be widely adapted to your own requirements. This section gives an overview of the configuration files and shows how, with little effort, work with LyX can be made even more comfortable. (More information can be obtained with HELP/CUSTOMIZATION.)

# Configuration files

LyX and KLyX differentiate between global and local (that is user-specific) configuration files. The global configuration files can be found in the LyXD directory. Where this directory is located, at least in LyX, can be easily determined by checking the HELP/VERSION dialog. On the author's computer, the directories were these for LyX and KLyX:

```
/usr/share/lyx
/opt/kde/share/apps/lyx/
```

The central configuration file in this directory is lyrc (and the rest of this section is exclusively dedicated to it). Further important files are contained in subdirectories bind (keyboard shortcuts) and kbd (keyboard layout).
If homogenous local configuration files exist, they are automatically used instead of the global files. The local configuration directories for LyX and KLyX are:

```
~.lyx
./kde/share/apps/lyx
```

The configuration files for LyX and KLyX are stored in different locations but fortunately enough, their format is identical. However, KLyX has an additional configuration file: "./kde/share/config/lyrc is used to store user-specific settings that can be adjusted directly in LyX dialogs (as the zoom factor in SETTINGS/SCREEN OPTIONS). These settings take precedence over the settings stored in lyrc. In this regard, KLyX follows the KDE paradigm that programs should be configured directly by the user interface (and not through laborious modifications of configuration files).

# Keyboard shortcuts

The keyboard shortcuts available under LyX/KLyX (as long as they do not concern the menu) are specified through the *.bind files in the bind directory. The two main files are cua.bind with the keyboard shortcuts common in the Windows world, to emacs.bind and emacs.bind with shortcuts as defined in (X)Emacs. In addition, all of these files resort to menus.bind and math.bind.

The choice of keybind scheme you wish to employ is default by means of the ind.file in lyrc. The factory default is cua, the alternatives are emacs and emacs.
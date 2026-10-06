
## 214 Chapter 7 GNOME Desktop Manager

## Menus

GNOME has many menus. Table 7-4 lists all the common menus and where to find information on each.

| Menus | | |
| --- | --- |
| Context | Refer to "Context Menu" on page 184. |
| Desktop | Refer to "Desktop Menu" on page 212. |
| Generic Icon | Right click any icon that is not on a panel (page 208). |
| Help | Refer to "Help Menu/Toolbar Selection" on page 205. |
| Main | Refer to "GNOME Menu" on page 208. |
| Menu | Refer to "Menu Menu" on page 253. |
| Menu panel | Refer to "Menu Panel" on page 246. |
| Nautilus menubar | Refer to "Menubar" on page 220. |
| Panel | Refer to "Panel Menu" on page 250. |
| Panel Icon | Right click any object on a panel (page 212). |
| Sawfish | Refer to "Sawfish Menu" on page 258. |
| Window List | Refer to "Window List and Workspace Switcher Applets" on page 211. |
| Window Operations | Refer to "Window Operations Menu" on page 256. |

## Nautilus: File Manager

Nautilus is many things.² This section discusses Nautilus the file manager. When Nautilus is not open, double-click the Home icon in the upper-left of the workspace or choose the GNOME menu: Home Folder to open a Nautilus window displaying the contents of the home directory (Figure 7-6, page 217), using icons (by default) to represent files.

² As of the release of Red Hat version 8.0, Mozilla had not been ported to GTK 2, so Mozilla could not be linked with Nautilus, depriving Nautilus of most Web browsing capabilities. Open the Side Pane while browsing websites; Nautilus gives you the option of opening the URL in another browser.

## Optional

### URI

URI is an acronym for Uniform Resource Identifier. The format of a URI is familiar because URLs (page 407), such as http: and ftp:, are a subset of URIs. Nautilus uses URIs to specify special locations. The part of a URI preceding the colon is called a scheme and is handled by the gnome-vfs (virtual filesystem) module. The gnome-vfs works, each scheme can have its own code to handle it. Standard code handles standard URI schemes, such as http: and ftp:. Special code, of which it introduced by Red Hat, handles nonstandard URIs.

When you log in, many systems display a Nautilus window showing the Start Here (start-here); Following are the locations for the entries that Start Here displays:

- start-here: /etc/X11/startherse
- server-settings: /etc/X11/serverconfig
- system-settings: /etc/X11/systemconfig

All files in /etc/X11/startherse are Desktop files. With other information, each of these files contains a line that begins with URL (URI):

```
$ cd /etc/X11/startherse; grep URL *
applications.desktop:URL=applications://
preferences.desktop:URL=preferences://
serverconfig.desktop:URL=server-settings://
systemconfig.desktop:URL=system-settings://
```

Each of these URIs points somewhere; the preceding list tells you where you are. In general, there is no correspondence between URIs and filesystem locations.

## Desktop Files

Files with a .desktop filename extension store information about how they should be displayed and what they point to. The following, abbreviated file displays the system_settings icon (Icon-system_settings.png) in the Start Here window. It is a link (Type=Link) to Preferences: (URL=preferences:). The Italian name is Preferenze (Name[it]=Preferenze). The comment also has default and Italian values. When you look at the file on your system, you will see that many more languages are included in the file.

```
cat /etc/X11/starthere/sysconfig.desktop
Type=Link
Name=System Settings
Name[it]=Impostazioni di sistema
```

Type=Link
Name=System Settings
Name[it]=Impostazioni di sistema
Comment=Change system settings
Comment[it]=Modifica impostazioni del sistema
Icon=system-settings.png
Encoding=UTF-8
URL=preferences://

```

```

**Start Here** (Figure 7-5)

When you log in, many systems display a Nautilus window showing the Start Here (start-here); Following are the locations for the entries that Start Here displays:

- start-here: /etc/X11/startherse
- server-settings: /etc/X11/serverconfig
- system-settings: /etc/X11/systemconfig

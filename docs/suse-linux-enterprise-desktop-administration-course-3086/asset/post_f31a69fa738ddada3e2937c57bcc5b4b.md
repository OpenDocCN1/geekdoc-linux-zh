
The same effect can be achieved with gconf-editor. Open a terminal window, type gconf-editor, and press Enter. The various options available are displayed in a treelike structure shown in Figure 14-5.

![](img/9129877170834ca9d5fdac5319bf5f12_574_0.png)

## Figure 14-5

To change the value of a key, double-click on the key in the right part of the window and change its value in the dialog that opens up.

Depending on the application, gconf-editor might offer more settings than the preference dialog of the respective application itself.

You can also use the gconftool-2 command-line tool to change the GConf settings. To change the default click policy to single, enter the following on the command line:

```
geeko@da10:~> gconftool-2 --set --type string
/apps/nautilus/preferences/click_policy single
```

The /apps/nautilus/preferences/click_policy key corresponds to the tree structure in gconf-editor. The --set and --type string options indicate that this key will take the new single string value. The type depends on the key and is defined in the schema file for that key. Schemas are covered in “Default Values” below.

You can also use gconftool-2 to view the current value of a key:

```
geeko@da10:~> gconftool-2 --get /apps/nautilus/preferences/click_policy
single
geeko@da10:~>
```

## Default Values

Default values are used for any preferences that are not set specifically by the user. Default values are set in /etc/opt/gnome/gconf/gconf.xml.defaults/. As an example, the following shows the file desktop/gnome/background/%gconf.xml in that directory, listing the default values for the background properties:

```
<?xml version="1.0"?>
<gconf>
<entry name="color_shading_type" mtime="1168258353"
schema="/schemas/desktop/gnome/background/color_shading_type"/>
<entry name="secondary_color" mtime="1168258353"
schema="/schemas/desktop/gnome/background/secondary_color"/>
<entry name="primary_color" mtime="1168258353"
schema="/schemas/desktop/gnome/background/primary_color"/>
<entry name="picture_opacity" mtime="1168258353"
schema="/schemas/desktop/gnome/background/picture_opacity"/>
<entry name="picture_filename" mtime="1169115045"
schema="/schemas/desktop/gnome/background/picture_filename"/>
<entry name="picture_options" mtime="1168258353"
schema="/schemas/desktop/gnome/background/picture_options"/>
<entry name="draw_background" mtime="1168258353"
schema="/schemas/desktop/gnome/background/draw_background"/>
</gconf>
```

In this example, the file does not specify the actual default values; instead, the file points to a schema. GConf schemas are contained in files in /etc/opt/gnome/gconf/schemas/. Schemas list

the possible preferences for applications or desktop settings. For the GNOME desktop background, the respective file is called desktop_gnome_background.schemas:

```
<gconfschemfile>
  <schemalist>
    <schema>
      <key>/schemas/desktop/gnome/background/draw_background</key>
      <applyto>/desktop/gnome/background/draw_background</applyto>
      <owner>gnome</owner>
      <type>bool</type>
      <default>true</default>
      <locale name="C">
        <short>Draw Desktop Background</short>
        <long>Have GNOME draw the desktop background</long>
      </locale>
      <locale name="ar">
      ...
```

This file contains keys, their type (integer, Boolean, string, float, or list), default value, and descriptions in several languages.

## Change Default Values

You can change the systemwide default values using either gconf-editor or gconftool-2.

To use gconf-editor for this purpose, make sure you are logged in as root when you start it. Then select File > New Defaults Window. A new window opens and lets you change settings as explained in “User-Defined Settings.”

To change systemwide defaults with gconftool-2, you must be logged in as root. You must specify the repository you want to change. Otherwise, by default, changes apply to the directory ~/.gconf/ in the user’s home directory. They will not apply to the directories beneath /etc/opt/gnome/gconf/gconf.xml.defaults. You also have to make sure gconfd-2 is not running.

The command to change the default for the background image file looks similar to the following example (the gconftool-2 command line needs to be entered in one line):

```
da10:~# killall gconfd-2
da10:~# gconftool-2 --direct --config-source
xml:readwrite:/etc/opt/gnome/gconf/gconf.xml.defaults --set --type
string /desktop/gnome/background/picture_filename
/usr/share/wallpapers/SpringFlowers.jpg
Resolved address "xml:readwrite:/etc/opt/gnome/gconf/gconf.xml.defaults"
to a writable configuration source at position 0
da10:~#
```

In the example, --direct indicates that the configuration repository is altered directly without using gconfd-2, and --config-source specifies the source to change.

The command changes the /etc/opt/gnome/gconf/ gconf.xml.defaults/desktop/gnome/background/%gconf.xml file, which now lists the new default value:

```
<entry name="picture_filename" mtime="1169120984" schema="/schemas/desktop/gnome/background/picture_filename" type="string">
  <stringvalue>/usr/share/wallpapers/Springflowers.jpg</stringvalue>
</entry>
```

Users who do not have an entry in their ~/.gconf/ directory trees defining a different background image will see the new background image the next time they log in. They are still able to change their own background images.

Setting preferences that cannot be changed by the user are covered in “Define Mandatory Settings with GConf and Desktop Profile Editor.”

![](img/9129877170834ca9d5fdac5319bf5f12_577_0.png)

## Exercise 14-2: Customize the GNOME User Interface

In this exercise, you set the preference for the mouse click to single click to launch programs that have an icon on the desktop and change the default for the background image.

Start the Nautilus file manager and set the preferences for the mouse click to single. Undo that change using gconftool-2. As user root, set a new default for the background image using gconf-editor started from a terminal window.

## Detailed Steps to Complete This Exercise

- 1. Start Nautilus with a double-click on the folder icon representing the home directory, and select Edit > Preferences > Behavior > Single Click to Activate Items.
- Close the File Management Preferences dialog by selecting Close.
- 2. Open a terminal window and, using less, view the entry:
  `~/.gconf/apps/nautilus/preferences/%gconf.xml`.
  Quit less by pressing q.
- 3. In the terminal window, type `gconf-editor &`, and press Enter.
- 4. Find the key you just changed in the tree structure to the left by expanding the apps, nautilus, and preferences sections.
- 5. View its value in the upper-right part of the dialog. Close gconf-editor.
- 6. To undo the change you made in Step 1, use gconftool-2 and enter the following (in one line):
  `gconftool-2 --set --type string /apps/nautilus/preferences/click_policy double`
- 7. In a terminal window, switch to user root by entering su - (password n0v311).
- 8. Kill any running gconfd-2 by entering killall gconfd-2.
- 9. If a user configuration exists for the background image, the default defined in the following steps won't take effect. Therefore, remove any background configuration that might already exist in geeko's home directory using the following command:
  rm -r /home/geeko/.gconf/desktop/gnome/background/
- 10. Start gconf-editor and select File > New Defaults Window. This opens a new window to change the default settings.
- 11. In the tree on the left, navigate to Desktop > GNOME > Background.
- 12. On the right, select the picture_filename entry with a double-click.
- 13. Change the filename to /usr/share/wallpapers/SpringFlowers.jpg.
- 14. Select OK.
- 15. Close all gconf-editor windows.
- 16. Log out; then log in as geeko again and notice the changed background.

## Objective 3—Define Mandatory Settings with GConf and Desktop Profile Editor

It is sometimes desirable from the desktop administrator’s point of view to limit what users can configure or change on their desktops. Reasons for this could be corporate policies or an effort to reduce help desk calls because of misconfiguration caused by users.

Even greater restraints are frequently imposed on desktops used in public places like trade shows.

You can set mandatory preferences using the following approaches:

- Use GConf to Set Mandatory Preference Values
- Use the Desktop Profile Editor
- Lock Down the Desktop

## Use GConf to Set Mandatory Preference Values

As covered in the previous objective, GConf is used to store user-defined preferences or to set systemwide defaults. It can also be used by the administrator to set preferences that cannot be changed by the user.

You can use the following tools:

- gconf-editor
- gconftool-2

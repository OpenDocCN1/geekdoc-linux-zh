The xorg.conf configuration file contains several sections, each defining a different element of the input and output system. Each section itself may contain one or more subsections that further define the input or output device. The basic format of a section looks like this:

```
# Comment for a section
Section "Name"
EntryName EntryValue
--
--
Subsection "Subname"
EntryName EntryValue
--
--
EndSubsection
EndSection
```

The section and subsection areas consist of a name/value pair that defines a setting for the device, such as the type of mouse or the available viewing modes of a monitor.

# Defining Sections

Nine predefined section names are used in the xorg.conf file:

+   Device: Describes the characteristics of a video card.
+   DRI: Includes information about the direct rendering infrastructure, which contains the hardware acceleration features found in many video cards.
+   Files: Lists pathnames of font files along with the file containing the color database used for the display.
+   InputDevice: Lists information about the keyboard and mouse or other pointing devices such as trackballs, touchpads, or tablets.
+   Module: Defines X server extension modules and font modules to load.
+   Monitor: Lists the monitor specifications.
+   ServerFlags: Lists X server options for controlling features of the X Windows environment.
+   ServerLayout: Combines one or more InputDevice and Screen sections to create a layout for an X Windows environment.
+   Screen: Defines a video card and monitor combination used by the X server.

The sections appear on an as-needed basis. That is, you'll only see the sections defined in the X.Org configuration file that are actually used to describe devices on your workstation. Thus, if you don't have any special font or color files defined, you won't see a Files section in the configuration file on your Ubuntu workstation.

# Example Configuration

To demonstrate the X.Org configuration file layout, let's take a look at an example configuration file from an Ubuntu workstation.

```
Section "InputDevice"
Identifier "Generic Keyboard"
Driver "kbd"
Option "XkbRules" "xorg"
```
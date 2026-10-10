Several key points in this section should be emphasized:

+   * The **Identifier** specifies an overall configuration. A configuration file can hold multiple Screen sections, as described shortly.
+   * The Device and Monitor lines point to specific Device and Monitor sections, respectively.
+   * The DefaultDepth line specifies the number of bits per pixel to be used by default. For instance, the preceding example sets this value to 16, so a 16-bit color depth is used, resulting in 2<sup>16</sup>, or 65,536, possible colors.
+   * Each Subsection defines a particulary display type. They have associated color depths (specified by the Depth line) and a series of resolutions (specified by the Modes line). The system tries each resolution specified by the Modes line in turn, until it finds one that works. There are also various optional parameters, such as Virtual (which defines a virtual screen that can be larger than the one that’s actually displayed) and ViewPort (a point within that virtual display at which the initial display is centered).

One final section is required: the ServerLayout section. This section consists of lines that identify the default Screen section and link it to mouse and keyboard definitions. For instance, a typical configuration will include a ServerLayout section resembling the following:

```
Section "ServerLayout"
    Identifier    "layout1"
    Screen        "screen1"
    InputDevice   "Mouse1" "CorePointer"
    InputDevice   "Keyboard1" "CoreKeyboard"
EndSection
```

> Although I describe the ServerLayout section last because it ties together all the other sections, it can appear earlier in the file—perhaps even first. The order of sections in the xorg.conf file is arbitrary.

Normally, an xorg.conf file will have just one ServerLayout section, but by passing the -layout *name* parameter to the server program, you can tell the server to use a different ServerLayout section, if one is present. You might use this to start X using a different mouse, for instance—say, a USB mouse on a notebook rather than the built-in PS/2 touch pad.

# Managing GUI Logins

Linux can boot into a purely text-based mode in which the console supports text-based logins and text-mode commands. This configuration is suitable for a system that runs as a server computer or for a desktop system for a user who dislikes GUIs. Most desktop users, though, expect their computers to boot into a friendly GUI. For such users, Linux supports a login system that starts X automatically and provides a GUI login screen. Configuring and managing this system requires you to understand a bit of how it works, how to run it, and how to change the configuration.
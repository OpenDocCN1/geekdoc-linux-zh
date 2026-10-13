+   - VendorName. Used to specify the vendor name.
+   - BoardName. Used to specify the name of the video card. Typically, the X server detects the features installed on your video card, including the amount of RAM, the chipset, and so on.
+   - Screen section. Used to specify how the video hardware (monitor and video card) should be used by the X server. Here is an example of this section:

```
Section "Screen"
    Driver      "accel"
    Device      "Trio32/Trio64"
    Monitor     "My Monitor"

    Subsection "Display"
        Depth       8
        Modes       "640x480" "800x600" "1024x768"
        "1280x1024"
        ViewPort    0 0
        Virtual     1280 1024
    EndSubsection

    Subsection "Display"
        Depth       16
        Modes       "640x480" "800x600" "1024x768"
        ViewPort    0 0
        Virtual     1024 768
    EndSubsection

    Subsection "Display"
        Depth       32
        Modes       "640x480" "800x600"
        ViewPort    0 0
        Virtual     800 600
    EndSubsection
```
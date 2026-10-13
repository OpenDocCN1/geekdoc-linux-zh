# OTHER RESOURCE FILE ISSUES

Line 9 demonstrates a comment in a resource file (such as .Xdefaults). A line beginning with an exclamation point will be ignored by the X Resource Manager. Note that this is in contrast to most other Linux configuration files, which generally use # to denote a comment.

Lines 12–16 demonstrate a multiline entry. Note the trailing backslashes on each line. These indicate the entry continues to the next line. No other characters (including spaces) can come after the backslash.

# FONT DEFINITIONS

Often resource files are used to define font use, as in the following example:

```
Vim*font: -misc-fixed-medium-r-normal--20-200-75-75-c-100-iso8859-15
```

This font definition is called an *X Logical Font Description (XLFD)* and is made up of 14 parts:

+   - **Foundry**—This is the provider of the font. These providers are registered with the X Consortium and include groups and companies like Adobe and Bitstream.
+   - **Family Name**—This identifies the family of typeface such as Helvetica or Times Roman.
+   - **Weight Name**—This identifies the typographic weight such as bold or demibold. Note that bold for one font family could be very similar to demibold for another family, so these entries should only be taken as a rough guide.
+   - **Slant**—This indicates the slant of the font as follows:
+     - R — Roman (upright)
+     - I — Italic
+     - O — Oblique
+     - RI — Reverse Italic
+     - RO — Reverse Oblique
+     - OT — Other
+   - **Set Width Name**—This indicates the nominal width of the font in the foundry’s judgment. Examples are normal, condensed, narrow, or double-wide.
+   - **Add Style Name**—This indicates additional style information such as serif, sans serif, informal, or decorated.
+   - **Pixel Size**—This indicates the size of the font in pixels for a nominal point size and Resolution Y.
+   - **Point Size**—This indicates the designed point size of the font, or 0 for a scalable font.
+   - **Resolution X and Resolution Y**—These indicate the resolution that the font was designed for. By giving both X and Y resolutions, the font server can determine the aspect ratio of the font, and by comparing these with the pixel size and point size, can determine what font will be the appropriate size for your particular display. Generally users want a particular point size or dots per inch. To determine whether a 10-point font will appear as 10 point on your screen, the server needs to match your resolution
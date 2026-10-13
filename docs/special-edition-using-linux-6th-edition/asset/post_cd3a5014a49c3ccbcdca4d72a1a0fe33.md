
## OTHER RESOURCE FILE ISSUES

Line 9 demonstrates a comment in a resource file (such as .Xdefaults). A line beginning with an exclamation point will be ignored by the X Resource Manager. Note that this is in contrast to most other Linux configuration files, which generally use # to denote a comment.

Lines 12–16 demonstrate a multiline entry. Note the trailing backslashes on each line. These indicate the entry continues to the next line. No other characters (including spaces) can come after the backslash.

## FONT DEFINITIONS

Often resource files are used to define font use, as in the following example:

```
Vim*font: -misc-fixed-medium-r-normal--20-200-75-75-c-100-iso8859-15
```

This font definition is called an *X Logical Font Description (XLFD)* and is made up of 14 parts:

- **Foundry**—This is the provider of the font. These providers are registered with the X Consortium and include groups and companies like Adobe and Bitstream.
- **Family Name**—This identifies the family of typeface such as Helvetica or Times Roman.
- **Weight Name**—This identifies the typographic weight such as bold or demibold. Note that bold for one font family could be very similar to demibold for another family, so these entries should only be taken as a rough guide.
- **Slant**—This indicates the slant of the font as follows:
  - R — Roman (upright)
  - I — Italic
  - O — Oblique
  - RI — Reverse Italic
  - RO — Reverse Oblique
  - OT — Other
- **Set Width Name**—This indicates the nominal width of the font in the foundry’s judgment. Examples are normal, condensed, narrow, or double-wide.
- **Add Style Name**—This indicates additional style information such as serif, sans serif, informal, or decorated.
- **Pixel Size**—This indicates the size of the font in pixels for a nominal point size and Resolution Y.
- **Point Size**—This indicates the designed point size of the font, or 0 for a scalable font.
- **Resolution X and Resolution Y**—These indicate the resolution that the font was designed for. By giving both X and Y resolutions, the font server can determine the aspect ratio of the font, and by comparing these with the pixel size and point size, can determine what font will be the appropriate size for your particular display. Generally users want a particular point size or dots per inch. To determine whether a 10-point font will appear as 10 point on your screen, the server needs to match your resolution and aspect ratio to a font that was designed with similar values. Otherwise, it might need to select an applicable scalable font to get the desired effect.
- **Spacing**—This indicates the spacing class of the font as follows:
  - P — Proportional
  - M — Monospaced
  - C — Char Cell (every character fits in a rectangle)
- **Average Width**—This is the arithmetic mean of the widths of all the characters in the font. If it begins with a tilde (~), the font is dominantly right to left.
- **Character Set Registry and Character Set Encoding**—These fields indicate the character set used to encode the font. Often these are ISO-registered tables such as ISO8859-1 for Latin-1.

Note that none of these values are case sensitive. Font definitions always start with a leading hyphen and each field is separated by a hyphen.

### Requesting a Font

Fonts are always defined with all 14 fields. These definitions are made in the font.dir files in the font libraries. The font libraries are generally found in /usr/X11R6/lib/X11/fonts, but other directories can be defined through XF86Config by using the FontPath command in the Files section.

When using a font, however, you do not have to specify all 14 fields. In fact, it is often easiest not to define all the fields. The Font Server will then pick a font that most closely matches your request. To skip a field, use an asterisk instead of a value. Consider, for example, the following font definition:

```text
-misc-fixed-medium-r-normal--20-200-75-75-c-100-iso8859-1
```

You probably don’t care about most of these entries. You probably just want a fixed, medium-weight, Roman font of an appropriate size for your current resolution. You can probably get this with the following:

```text
-*-fixed-medium-r-normal--*-*-*-*-*-*-*
```

I say *probably* because it can depend on the order of your font definitions. The font server will select the first font that matches your request, so if you had a font with a non-Latin encoding early in your search, you might have to include iso8859-1 in this definition to get the font you want.

Using wildcards can be especially helpful when using the same resource files between different machines, especially machines running different distributions of Linux or non-Linux machines altogether. Not all flavors of Linux have the same fonts installed by default. If you are too specific in your font definition, you might discover that the machine you are on doesn’t have that font at all, in which case the font server will guess what font you want (unfortunately the font server is not always a good guesser). If you provide some leeway by specifying only the fields you really care about, you are much more likely to get an acceptable font.

On the other hand, the advantage of specifying exactly the font you want is that you will always get exactly that font. This will save you some grief if you ever install new fonts that can come earlier in the search path.

## FONTSEL

Selecting a font purely by name and metrics can be fine for publishing professionals, but it’s not a major task for most of the world. For the rest of us, we have xfontsel. xfontsel provides a GUI interface for selecting just the font you want (see Figure 6.3).

**Figure 6.3**  
xfontsel helps you find the font you want.

![](img/c741b1b6b6eccaba2ad43454c979a7f8_158_0.png)

After running xfontsel from the command line, click each of the fields (such as foundry or family) to select available options. The second line will show the font selector you can use to choose the font displayed in the lower box. When you get the font you want, you can click the Select button and paste the selector into another application.

xfontsel has several handy command-line options, shown in Table 6.3.

**TABLE 6.3 — XFONTSEL COMMAND-LINE OPTIONS**

| Option | Description |
|---|---|
| `-pattern fontname` | Limits listed fonts. This is an XLFD pattern. |
| `-print` | If this option is selected, the font selector will be printed to the terminal when you click the Quit button. |
| `-sample text` | Usually, xfontsel uses an alphabet sample to test the font. This option lets you choose specific sample text for linear addressed fonts. Most fonts are linearly addressed, so this is usually the option you want. |
| `-sample16 text16` | This option provides sample text for 16-bit matrix-encoded fonts. These are generally glyph fonts. See the xfontsel man page for more information. |
| `-sampleucs textUCS` | This option provides sample text for UTF-8 encoded text. See the xfontsel man page for more information. |
| `-scaled` | This option allows you to choose arbitrary point-sizes for scalable fonts. |

## CONNECTING TO A FONT SERVER

Generally, your own workstation will provide your fonts, but in some environments it can be convenient to centralize your fonts onto a single server. Although there is seldom a need to set font servers up, your network might already have one that you would like to use.

To select a font server, add entries in the following form to the FontPath entry in the Files section:

```
transport/hostname:port
```

Generally this will be something like the following:

```
tcp/myserver:7100
```

In this example, tcp is the protocol, which is the usual protocol for fonts. myserver is your font server, and 7100 is the port. This is the normal font server port.

For more information on setting up a font server, see the xfs man page.

## LOADING AND QUERYING RESOURCES

Generally, resource definitions are put in a file called ~/.Xresources. If you want to update your resources after you’ve logged in, update this file and run the following:

```
$ xrdb -merge ~/.Xresources
```

If you want to see what resources are currently in use, run this:

```
$ xrdb -query
```

![](img/c741b1b6b6eccaba2ad43454c979a7f8_159_0.png)

## PROJECT: AUTO-SHRINKING XTERM

Most people just use X resources to make simple modifications to colors or fonts. Even then, they generally just copy the X resources from another user without ever really understanding what the resources are doing. In this short project, we’ll investigate an interesting set of resources in xterm: Translations.

Translations in xterm enable you to execute certain actions in response to events. Often these events are key presses or mouse clicks (a good way to build macros), but there are other events such as when the mouse enters or leaves the window.

Say you want the xterm to shrink whenever the mouse leaves it and then grow when the mouse enters. This way, you could have many xterms on the screen and could somewhat watch what they were doing without having them take over your entire desktop. This can be very handy when you have a lot of compilations going on. You might want to watch them all to see when one completes, but you don’t really care what the output looks like most of the time.

To get this effect, you can instruct xterm to change its font in response to mouse actions. The following X resource would do this:

```
shrinkerterm*VT100.Translations: <EnterWindow>: set-vt-font(d)  \n\
                              <LeaveWindow>: set-vt-font(l)  \n
```

| Part | Description |
| :--- | :--- |
| vertical dpi | A number of vertical pixels per inch of resolution. |
| spacing | This can be m (for monospace), p (for proportional), or c (for character cell). A monospace font is one that has all its characters the same width. A proportional font has characters of various widths (for example, the letter *w* is wider than the letter *i*). A character cell font is a fixed-width font based on the way typewriter fonts are spaced. |
| - | - |
| pixel width | The average width, in tenths of a pixel, of all the characters in the font. |
| character set | This is the version of the standard used to define the character set. The ISO (International Organization for Standardization) has established standards for the sets of characters that are included in the alphabet of various languages. |

Not only are the long-font names descriptive, but they also are in a form that enables you to use wildcard characters in searching for a font. This way, you only need to specify the things you care about and let the rest of it default. For example, you can use the following as the name of a font in a call to `gtk_font_load()`:

```
```
-* bookman-light-r-normal--14-*-*-*-*-iso8859-1
```
```

The parts specified in the name must be an exact match with an actual font, while the asterisks can match any value. Of course, several fonts may match, but the first match encountered is the one returned. The above example could select this font:

```
```
-adobe-bookman-light-r-normal--14-135-75-p-82-iso8859-1
```
```

When specifying a font name, you should be specific only with the parts you need. This way you have a better chance of matching an actual font name. If your specifications do not match the name of a font, the default font named `fixed` is used, and it is almost never the one you want.

# ## The Font Picker Widget

There is a GNOME widget that enables you to select and display fonts. The widget is placed in your application as a button on a dialog box or in a menu. The following program shows how you can use the widget to select a font, and then how that font can be applied to the text of another widget.

```
```
1 /* fontpicker.c */
2 #include <gnome.h>
3
```
```
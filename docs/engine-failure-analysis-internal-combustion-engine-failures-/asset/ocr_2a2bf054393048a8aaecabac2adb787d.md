450 Linux Command Instant Reference

# # ttf2pt1

```
**ttf2pt1** [ option | truetype font type] font
```

Converts the specified TrueType font into a Type 1 font file (PFA or PFB format). To obtain ttf2pt1, visit http://www. netspace. net. au/ ~mheath/ttf2pt1.

# ## OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| -A | Create a font metrics (AFM) file. |
| -b | Create a PFB file. |
| -e | Create a PFA file. |
| -f | Skip trying to guess the ForceBold parameter. |
| -h | Disable the autogeneration of hints. |
| -l language | Extract the characters for the specified language. You can use the following options: latin1, latin2, latin4, latin5, bulgarian, and russian. |
| -o | Disable outline code optimization. |
| -r | Disable outline di_action reversal. |
| -s | Disable outline smoothing. |
| -t | Disable auto-scaling. |
| -v n | Rescale the font to the specified size (n) of an upper- case letter. |
| -w | Attemp to correct the glyph widths. |

# ## EXAMPLE

| This Command | Does the Following |
| :--- | :--- |
| ttf2pt1 myfont.ttf myfont.pfa | Converts the specified TrueType font (myfont.ttf) into a Type 1 font (myfont.pfa). |
# ttmkfdir

**ttmkfdir [ option ] –o fonts.scale**
Creates a fonts.scale file listing available TrueType fonts in the working directory. The TrueType font filenames must not contain uppercase letters. Run mkfontdir after using this utility. XFree86 cannot work with TrueType fonts directly. To use TrueType fonts on your system, you must install and run a TrueType font server. If you do not wish to install a TrueType-compatible font server, you can use TrueType fonts by converting them to Type 1 (PostScript) fonts.

See also *tf2pt1*.

# OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| –c | Use less strict completeness tests for encoding tables. |
| –d directory | Scan the specified directory for TrueType files, or the working directory if directory is not specified. |
| –f name | Use the specified foundry name for unknown font vendors. The default is misc. |
| –m n | Specify the maximum number (n) of missing characters per encoding. The default is 5. |
| –o filename | Write output to the specified filename. Use fonts.scale. |
| –P | Use panose information. |

# EXAMPLE

| This Command | Does the Following |
| :--- | :--- |
| **ttmkfdir –o fonts.scale** | Creates the fonts.scale file containing information about the TrueType fonts in the working directory. |
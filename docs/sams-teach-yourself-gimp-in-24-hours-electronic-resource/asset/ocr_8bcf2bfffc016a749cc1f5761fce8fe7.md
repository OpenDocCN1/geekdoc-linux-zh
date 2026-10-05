# Getting Started

![](bbox=[0.08333, 0.11667, 0.15666999999999998, 0.18333000000000002])

# A Word About UNIX and File Format Extensions

Because you're no longer working in Windows, I should mention that Linux
deals with file formats and extensions a little differently than you might be
acustomed to. For the most part, you should follow the standard naming
conventions for graphics files, appending the usual three or four letter
extension to the end of the name, such as gif for GIF files, .eps for post-script files, .tif or .tiff for TIFF graphics, and so on. You do this in order to\stay compatible with your files, as well as a convention of habit, so that
You can remember what kinds of files you're dealing with. But you should
keep in mind that UNIX files are not defined by their extension.
it is entirely possible to save a GIF with no extension whatsoever, as long
as you specify to the application it what kind of file it is. So if,
of the sake of obfuscation, you have a GIF named picture.jpg, you can
easily open it with GIMP. In the Determine File Type menu in the
dialog box, the Automatic option is selected by default. Nine times out of
time, GIMP will not be fooled and will open it for the GIF it really is.\oes by more or less looking at the file itself, not at the filename
extension. If, for some reason, GIMP does not autodetect the type of a file
 no extension (or a mislabeled one) correctly, you must select the
correct file type from the menu to tell the GIMP what kind of file
you're dealing with.

Take a laundry-list out what files GIMP can handle by default.

# Table 2.1 FILE FORMATS IN GIMP

| Format | Open | Save | Information |
|---|---|---|---|
| ASCII | X | X | ASCII text (such as this nifty BBS, for example). |
| bitmap | X | X | Windows and OS/2 bitmap. A popular uncompressed format. |
| bzip2 | X | X | bzip2 is a compression utility. GIMP allows you to open and save compressed images directly within the program. |
| CEL | X | X | KISS indexed file format. |
| Fax G3 | X | | The format used by fax machines. |
| FITSX | X | | The Flexible Image Transport system. |
| FLC, FLI | X | | Popular animation formats. |
| GBR | X | X | GIMP Brush (GIMP's native brush format). |

continues
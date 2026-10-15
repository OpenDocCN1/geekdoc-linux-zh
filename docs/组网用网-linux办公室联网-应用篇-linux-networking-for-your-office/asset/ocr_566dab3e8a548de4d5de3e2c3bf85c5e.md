This converts the Macintosh-style SuperPrint 1000 PS PPD file into one that's usable by Netatalk and that's called superprint.ppd. This command also places the converted file in the destination directory for the PPD files. You can use unix2mac to reverse this process if you have need of reading Linux-style text files on a Macintosh.

If you specify the options=crif parameter to a share in the AppleVolumes.default configuration file, Netatalk performs this translation automatically on files it can identify as text files when you copy them from the Macintosh to Linux, using Netatalk. Unfortunately, Netatalk doesn't identify all PPD files as text files, so this feature doesn't always work.

If you don't know which form of end-of-line characters a text file uses, try viewing it in Linux by using less. If the file appears properly formatted in reasonable-looking lines, it's got Linux-style end-of-line characters. If, instead, you get a file with the characters ^M scattered throughout it where you would normally expect line breaks, as in Figure 17.1, the file is in Macintosh format and needs to be converted.

![](bbox=[0.35, 0.55, 0.75, 0.75])

# FIGURE 17.1

Linux doesn't cope well with Macintosh-style text files.

# NOTE

DOS, Windows, and OS/2 use a third type of end-of-line code. Fortunately, Netatalk can cope with this style of end-of-line code, and it looks like Linux-style coding when you use less, so you needn't concern yourself with DOS-style end-of-line codings.
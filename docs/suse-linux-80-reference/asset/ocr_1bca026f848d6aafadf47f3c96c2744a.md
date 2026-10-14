The user must then — depending on the language used — select the matching encoding. Especially when transferring texts between different computers, the encoding used must also be transferred. The advantage of this procedure is obvious: To receive support for regional special characters, you only need to select the correct encoding and immediately most programs will be able to portray these special characters, since almost all programs use an 8-bit value (one byte) to represent a text character. If the wrong encoding is chosen, the special characters will be wrongly depicted. With most X applications, as well as with the KDE desktop, you can usually select the coding of the character set when you are configuring the font to use. In X applications, the encoding is usually referred to as Encoding.

The disadvantage of this method is that some language combinations are impossible: You cannot, for example, easily write a German text with umlauts in which you mention Russian place names in Cyrillic.

This dilemma can only be solved using a different approach — with the use of Unicode. Unicode codes characters, unlike ASCII, with two or even more bytes, allowing considerably more characters to be represented. Only if you use Unicode can you depict Asian languages with more than 127 characters, such as Chinese, Japanese, or Korean, on the computer. The disadvantage of this method is that most existing software cannot handle these characters and that you can only read or write texts yourself with Unicode characters using special software. For more information on using Unicode fonts in Linux, see `http://www.unicode.org`. It is expected that, in the future, more and more programs will support Unicode characters. SuSE Linux offers the program yudit to enter texts in Unicode. The program yudit can be found in the package yudit, series xap and, after installation, via the SuSE menu, under Office → Editors.

After these observations, we now have a step-by-step description of the installation of additional fonts, using the example here of True Type fonts.

Locate the fonts to install in your X Window System. If you have licensed True Type fonts, you can simply use these on your system. Mount the partition containing these fonts.

You should create a font directory — if this does not yet exist — and change to it. SuSE Linux already has a directory called `/usr/X11R6/lib/X11/fonts/truetype`. You can copy the relevant fonts to this directory.

```
earth:/root # cd /usr/X11R6/lib/X11/fonts/truetype
```
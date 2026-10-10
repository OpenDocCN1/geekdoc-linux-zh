shortcut to start up xterm.

The xterm package allows you to set individual features using command-line parameters. The following sections discuss these features and how to change them.

# Command-line parameters

The list of xterm command-line parameters is extensive. You can control lots of features to customize the terminal emulation features, such as enabling or disabling individual VT emulations.

> **NOTE**
> 
> xterm has a huge number of configuration options — so many that they cannot all be covered here. Extensive documentation is available via the Bash manual. Accessing the Bash manual is covered in *Chapter 3*. In addition, the xterm development team provides some excellent help on its website: `invisible-island.net/xterm`.

You can invoke certain configuration options by adding a parameter to the `xterm` command. For example, to have the xterm emulate a DEC VT100 terminal, at the CLI type the command `xterm -ti vt100` and press Enter. *Table 2-16* shows some parameters you can include when invoking the xterm terminal emulator software from the command line.

**TABLE 2-16** xterm Command-Line Parameters

| Parameter | Description |
| --- | --- |
| -bg *color* | Specifies the color to use for the terminal background |
| -fb *font* | Sets the font to use for bold text |
| -fg *color* | Specifies the color to use for the foreground text |
| -fn *font* | Sets the font to use for text |
| -fw *font* | Specifies the font to use for wide text |
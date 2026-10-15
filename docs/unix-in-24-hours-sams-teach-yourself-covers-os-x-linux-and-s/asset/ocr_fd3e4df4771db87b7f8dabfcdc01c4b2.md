# Printers

Search in Printers:

Showing 1 of 1 printer.

| Queue Name | Description | Location | Make and Model | Status |
|---|---|---|---|---|
| Samsung_ML_191x_252x_Series___MiniMe | Samsung ML-191 | MiniMe | Samsung ML-191x 252x Series | Idle |

FIGURE 18.3 A Samsung printer ready to go in the CUPS interface.

4. Can’t get things to work correctly with your printer? You might need to install a PostScript interpreter (GhostScript is the most popular) or similar. You can learn about how to troubleshoot your particular printer configuration by going to http://www.openprinting.org.

However hardcore your command-line zeal for Unix, there are still a few tasks that are more easily accomplished from a graphical interface like GNOME. And while CUPS is now extraordinarily powerful and flexible, I recommend that you try to get any new Unix printer configured and online through the Unix or Linux GUI tools, not the command line. Once you’ve done so, they become available for both command-line and graphical interface interaction, fortunately.

# Task 18.3: Printing Files with lpr or lp

Now that you have identified the name of the printer to use, how do you send information to the printer? If you are on a BSD system, the command to do this is lpr. You can print the results of a pipe command by adding lpr at the end of the pipeline, or you can print files directly by specifying them to the program. You can even use < to redirect input.
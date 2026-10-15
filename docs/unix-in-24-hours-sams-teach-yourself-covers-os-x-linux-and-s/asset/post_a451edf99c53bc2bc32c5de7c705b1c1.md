
# Web Interface is Disabled

The web interface is currently disabled. Run "cupsctl WebInterface=yes" to enable it.

FIGURE 18.1 Accessing CUPS through a Web browser: permission denied.

2. Oops! As you can see, you'll need to go back to the command line and invoke the following command:

```
$ cupsctl WebInterface=yes
$
```

Now try that browser access to localhost:631 again, as shown in Figure 18.2.

## CUPS 2.0.0

CUPS is the standards-based, open source printing system developed by Apple Inc. for OS X® and other UNIX®-like operating systems.

## CUPS for Users

- Overview of CUPS
- Command-Line Printing and Options
- User Forum

## CUPS for Administrators

- Adding Printers and Classes
- Managing Operation Policies
- Using Network Printers
- cupsd.conf Reference

## CUPS for Developers

- Introduction to CUPS Programming
- CUPS API
- Filter and Backend Programming
- HTTP and IPP APIs

FIGURE 18.2 CUPS is easiest to work with via a Web browser.

3. Click on the Printers tab to see what printers, if any, you have configured (see Figure 18.3).

## Printers

Search in Printers:

Showing 1 of 1 printer.

| Queue Name | Description | Location | Make and Model | Status |
|---|---|---|---|---|
| Samsung_ML_191x_252x_Series___MiniMe | Samsung ML-191 | MiniMe | Samsung ML-191x 252x Series | Idle |

FIGURE 18.3 A Samsung printer ready to go in the CUPS interface.

4. Can’t get things to work correctly with your printer? You might need to install a PostScript interpreter (GhostScript is the most popular) or similar. You can learn about how to troubleshoot your particular printer configuration by going to http://www.openprinting.org.

However hardcore your command-line zeal for Unix, there are still a few tasks that are more easily accomplished from a graphical interface like GNOME. And while CUPS is now extraordinarily powerful and flexible, I recommend that you try to get any new Unix printer configured and online through the Unix or Linux GUI tools, not the command line. Once you’ve done so, they become available for both command-line and graphical interface interaction, fortunately.

## Task 18.3: Printing Files with lpr or lp

Now that you have identified the name of the printer to use, how do you send information to the printer? If you are on a BSD system, the command to do this is lpr. You can print the results of a pipe command by adding lpr at the end of the pipeline, or you can print files directly by specifying them to the program. You can even use < to redirect input.

### Note

If you’re using a System V version of Unix, you will need to use the lp command instead. As you read through this hour, you will see the differences between lpr and lp indicated. Note how the philosophies of the two vary.

Numerous flags are available for lpr and lp; the most valuable ones are listed in Table 18.1 and Table 18.2. Notice the different meanings of the -P flag with the two commands.

| Flag | Meaning |
|------|---------|
| -h | Do not print the header page. |
| -i | Indent the entire file eight spaces before printing. |
| -l | Print in landscape (sideways) mode, if the printer is capable of doing so. |
| -Pprinter | Send the print job to printer printer. |
| -R | Print pages in reverse order. |

# TABLE 18.1 Useful Flags for lpr

| Flag | Meaning |
|------|---------|
| -dprinter | Send the print job to the printer named printer. |
| -Pn | Print only page n. |
| -ttitle | Use title as the cover page title, where title is any string. |

# TABLE 18.2 Useful Flags for lp

1. Here’s a demonstration of what happens if you try to use lp or lpr without specifying a printer and without having the PRINTER environment variable set. First, remove the environment variable definition for PRINTER by setting it to an empty string:

```
$ PRINTER=""
$ who | lpr
lpr: No printer specified
Broken pipe
```

Some systems default to a printer named lp in this situation, so if you don’t get an error message, that’s what happened. If you have lpstat (a command for checking the status of a printer), the -d flag will result in lpstat listing your default printer.

To specify a printer, use the -P flag with lpr or the -d flag with lp, followed immediately by the name of the printer:

```
$ who | lpr -Pattic3
```

Specifying a printer with the -P flag (or -d with lp) will always override the environment variable specified in PRINTER; therefore, you can specify the default printer with PRINTER and specify other printers as needed without any danger.

Notice that I printed the output of the who command but received absolutely no

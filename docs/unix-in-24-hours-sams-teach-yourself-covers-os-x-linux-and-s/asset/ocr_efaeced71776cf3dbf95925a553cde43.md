# Note

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

+   1. Here’s a demonstration of what happens if you try to use lp or lpr without specifying a printer and without having the PRINTER environment variable set. First, remove the environment variable definition for PRINTER by setting it to an empty string:

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
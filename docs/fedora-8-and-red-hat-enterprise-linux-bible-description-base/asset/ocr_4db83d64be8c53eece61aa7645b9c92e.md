> **CROSS-REFERENCE:** For information on configuring local and remote printers for Fedora and RHEL, see Chapter 17.

As a non-administrative user, you don’t have a lot of control over how the printers are configured. You can, however, check which printers are available to print to, check the status of print queues (documents waiting to print), and remove any of your own queued print jobs.

# # Printing to the default printer

When your system administrator (or you) configured printers for your computer, one of those printers was defined as the default printer. If you are not sure which printer is your default, type `system-config-printer` and look for the printer with the check by it.

Most graphical word processors, such as StarOffice and OpenOffice.org, enable you to choose a printer from those available. Some of the less sophisticated Linux utilities that run from the command line, however, use only the default printer. For example, `dvips` (to print a PostScript file) and `groff -l` (to print a troff/nroff file) automatically send the output to the default printer.

As a regular user, you can override the default printer using the `PRINTER` environment variable. For example, if the default printer on your computer is `lp0` and you want to print regularly to `lp1`, change your default printer by setting the `PRINTER` variable as follows:

```
$ export PRINTER=lp1
```

To have this take effect all the time, you could add this line to one of your shell configuration files (such as `$HOME/.bashrc`, if you use the bash shell).

# # Printing from the shell

The `lpr` command is used to print files from the shell. You can use `lpr` to print whether the LPRng or CUPS print service is being used. If you have a file already formatted, use `lpr` to print it. For example, if you have a PostScript output file (`file.ps`) and you want to print it to your PostScript printer, use the following command line:

```
$ lpr file.ps
```

If you want to specify a particular printer (other than the default), add the `-P*printer*` option. For example, to print to the `lp0` printer, you could type the following:

```
$ lpr -Plp0 file.ps
```

If you want to print more than one copy of a document, use the `-#*num*` option, where `num` is replaced by the number of copies you want. For example, to print five copies of a file, use:

```
$ lpr -#5 file.ps
```
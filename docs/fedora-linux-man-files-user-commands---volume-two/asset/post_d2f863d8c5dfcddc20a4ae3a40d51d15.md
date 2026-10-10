
## DIRECT, SPOOLER-LESS PRINTING

### Options

- **-v**
  verbose mode for debugging. **WARNING**: This will create a file in `/tmp` that contains the debugging information. This opens a security loophole and should not be used in production.
- **-q**
  quiet mode - minimal information output
- **-P** `<printer>`
  `<printer>` is the configured printer which should be used for this job.
- **--ppd** `<ppdfile>`
  The PPD file `<ppdfile>` should be applied for processing this job.
- **-o** `<option>=<value>`
  Option settings for this job.
- `<files>`
  The file(s) to be printed.

**foomatic-rip** will print from standard input unless at least one file to be printed is specified on the command line. If your printer PPD file is stored as `/etc/direct/<printer>.ppd` or `~/.foomatic/direct/<printer>.ppd` you can use it by simply specifying “-P `<printer>`”.

Put a line

```
*FoomaticRIPPostPipe: “| <command>”
```

into the PPD file, right after *PPD-Adobe: “4.3”, where `<command>` is a command into which you want to re-direct the output data. Due to the restrictions of PPD files `<`, `>`, and `“` are not allowed in the `<command>`, replace them as follows:

```
Character Replacement ----------------------
```

This way you can print directly to your printer, use

```
*FoomaticRIPPostPipe: “| cat &gt; /dev/lp0”
```

or

```
*FoomaticRIPPostPipe: “| cat &gt; /dev/usb/lp0”
```

for local parallel or USB printers. To make normal users able to print this way add them to the group `lp` and make sure that the appropriate printer device file `/dev/...` is group-writable for the `lp` group.

for a TCP/Socket/JetDirect printer with the host name **printer** listening on port **9100** you need this:

```
*FoomaticRIPPostPipe: “| /usr/bin/nc -w 1 printer 9100”
```

Note the “-w 1” in the “nc” command line, it makes “nc” exiting immediately after the data is transferred to the printer.

```
*FoomaticRIPPostPipe: “| rlpr -Plp@printserver”
```

directs your jobs to the LPD printer queue **lp** on the machine named **printserver**.

See also http://www.openprinting.org/direct-doc.html

## PRINTING WITH SPOOLER

See the documentation on the OpenPrinting Web site: http://www.openprinting.org/

## CONFIGURATION FILE

The file /etc/foomatic/filter.conf is read whenever foomatic-rip is executed. It allows to configure the behavior of foomatic-rip as follows (lines beginning with # are comments and therefore get ignored):

- **debug: 0|1**
  Turns on (1) or off (0) the debug mode. This is equivalent to supplying the `--debug` command line option. Default setting is `0`.
- **ps_accounting: 0|1**
  Turns on (`1`) or off (`0`) inserting PostScript code for page accounting into PostScript jobs. The inserted PostScript code makes Ghostscript generating accounting output on stderr and CUPS can this way log each page which got printed. The code will only be inserted if CUPS is the spooler. Default setting is `1`.
- **echo: [_<path>_/<executable>]**
  Sets the path to an `echo(1)` executable which supports `-n`.
- **gs path: [_<path>_/<executable>]**
  Sets the path to the Ghostscript (`gs(1)`) executable. To be used if Ghostscript is at a non-standard location or if an alternative Ghostscript should be used.
- **execpath: _<path>_[:_<path>_]...**
  Sets the `$PATH` variable to be used by foomatic-rip.
- **cupsfilterpath: _<path>_[:_<path>_]...**
  Sets the directories (colon-separated) in which foomatic-rip searches for CUPS filters.
- **preferred_shell: [_<path>_/<executable>]**
  Sets the preferred shell to use when executing FoomaticRIPCommandLine and friends. Several PPD files use shell constructs that require a more modern shell like `bash, zsh, or ksh`.

## FILES

- /etc/cups/ppd/\<printer>.ppd
- /etc/direct/\<printer>.ppd

  The PPD files of the currently defined printers

- /etc/foomatic/filter.conf

  Configuration file for foomatic-rip

## EXIT STATUS

**foomatic-rip** returns 0 unless something unexpected happens.

## AUTHOR

Till Kampeter `<till.kampeter@gmail.com>` with parts of Manfred Wassmanns's `<manolo@NCC-1701.B.Shuttle.de>` man pages for the Foomatic 2.0.x filters.

## BUGS

None so far.

Please send bug reports to the OpenPrinting bug tracker:

http://bugs.linuxfoundation.org/

Use “OpenPrinting” as the product and “cups-filters” as the component.

## NAME

foomatic-searchprinter - Search Foomatic database

## SYNOPSIS

foomatic-searchprinter [-mM] [-dFID] SEARCHTERM

foomatic-searchprinter -h

## DESCRIPTION

This command displays Foomatic database entries matching SEARCHTERM.

### Options

- **-mM**
  - Search mode:
    - *M = 0*
      Match everything (default)
    - *M = 1*
      No matches on only the manufacturer
    - *M = 2*
      No matches on only the manufacturer or only the model
    - *M = 3*
      Exact matches of device ID, make/model, or Foomatic ID plus matches of the page description language in the device ID to appropriate “Generic” printers
    - *M = 4*
      Exact matches of device ID, make/model, or Foomatic ID only
- **-dD**
  - Display results:
    - *D = 0*
      Everything
    - *D = 1*
      Only best match class (default)
    - *D = 2*
      Only best match
- **-h**
  Show help message and exit.

## BUGS

None so far.

Please post bug reports on
http://lists.freestandards.org/mailman/listinfo/printing-foomatic

## NAME

fpaste - A cli frontend for the fpaste.org paste bin

## SYNOPSIS

```
fpaste [OPTION]... [FILE]...
```

## DESCRIPTION

It is often useful to be able to easily paste text to the Fedora Pastebin at http://fpaste.org and this simple utility will do that and return the resulting URL so that people may examine the output. This can hopefully help folks who are for some reason stuck without X, working remotely, or any other reason they may be unable to paste something into the pastebin using a web browser.

## OPTIONS

- -version
  show program's version number and exit
- -h, -help
  show help message and exit
- -n "NICKNAME"
  your nickname; default is ""
- -d "PASSWORD", -password="PASSWORD"
  password for paste; default is ""
- -l "LANGUAGE"
  language of content for syntax highlighting; default is "text"; use "list" to show all 200+ supported langs
- -x "EXPIRES"
  time before paste is removed; default is 2592000 seconds; valid options: 1800, 21600, 86400, 604800, 2592000
- -U, -URL "URL"
  URL of fpaste server; default is http://fpaste.org
- -P, -private
  make paste private; default is yes; valid options: yes, no
- -i, -clipin
  read paste text from current X clipboard selection
- -o, -clipout
  save returned paste URL to X clipboard
- -selection=CLIPBOARD
  specify which X clipboard to use. valid options: "primary" (default; middle-mouse-button paste), "secondary" (uncommon), or "clipboard" (ctrl-v paste)
- -fullpath
  use pathname VS basename for file description(s)
- -pasteself
  paste this script itself
- -sysinfo
  paste system information
- -printonly
  print paste, but do not send
- -confirm
  print paste, and prompt for confirmation before sending

## EXAMPLES

Paste file foo.txt at fpaste.org

```
fpaste foo.txt
```

Paste output of ifconfig to fpaste.org with description “my network config”

```
ifconfig | fpaste
```

Paste mycode.py to fpaste.org with description as “problem with foo”, nickname “codemonkey”, and language “python”

```
fpaste -n codemonkey -l pthon mycode.py
```

Paste mouse-selected text from the primary X selection clipboard, and then overwrite the same clipboard with the returned fpaste URL

```
fpaste -io
```

To manually paste clipboard contents, run fpaste without file arguments so that it waits for input, then paste using mouse middle-click, <Ctrl-V>, or other, then press <Enter> followed by <Ctrl-D> to finish (EOF).

To paste the output of more than one program and/or file at a time, use the following example forms:

```
(lsusb; lspci) | fpaste
fpaste <(lsusb) <(lspci)
```

```
fpaste <(fdisk -l) /etc/grub.conf
(fdisk -l; cat /etc/grub.conf) | fpaste
```

```
(uname -a; yum repolist) | fpaste
```

Gather and paste various information about the running system. The info collected should be practically anonymous, and you may use the `--printonly` or `--confirm` options to preview what would be sent. fpaste.org URLs are also practically anonymous ([a-zA-Z0-9]**4 = 14,776,336 combinations), so you may also preview it instead before giving the link out.

```
fpaste --sysinfo
fpaste --sysinfo --confirm
fpaste --sysinfo --printonly | less
```

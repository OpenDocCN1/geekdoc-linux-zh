
## AUTHOR

Written by Ross Paterson.

## REPORTING BUGS

GNU coreutils online help: <http://www.gnu.org/software/coreutils/> Report fmt translation bugs to <http://translationproject.org/team/>

## COPYRIGHT

Copyright © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>. This is free software: you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.

## SEE ALSO

Full documentation at: <http://www.gnu.org/software/coreutils/fmt> or available locally via: info ‘(coreutils) fmt invocation’

# FONT2C

## NAME

font2c - Write PostScript Type 0 or Type 1 font as C code

## SYNOPSIS

`font2c fontnames`

## DESCRIPTION

This script invokes `gs(1)` with the following options:

    -q -dNODISPLAY -dWRITESYSTEMDICT

followed by the arguments from the command line. This will write out a PostScript Type 0 or Type 1 font as C code that can be linked with the interpreter.

## SEE ALSO

`gs(1)`

## VERSION

This document was last revised for Ghostscript version 9.16.

## AUTHOR

Artifex Software, Inc. are the primary maintainers of Ghostscript. This manpage by George Ferguson.

# FONTTOSFNT

## NAME

fonttosfnt - Wrap a bitmap font in a sfnt (TrueType) wrapper

## SYNOPSIS

`fonttosfnt [ options ] -o file.ttf [ --- ] font...`

## DESCRIPTION

Wrap a bitmap font or a set of bitmap fonts in a sfnt (TrueType or OpenType) wrapper.

## OPTIONS

- `-v`
  Be verbose.
- `-c`
  Do not crop glyphs. This usually increases file size, but may sometimes yield a modest decrease in file size for small character cell fonts (terminal fonts).
- `-b`
  Write byte-aligned glyph data. By default, unaligned data is written, which yields a smaller file size.
- `-r`
  Do not reencode fonts. By default, fonts are reencoded to Unicode whenever possible.
- `-g n`
  Set the type of scalable glyphs that we write. If n is 0, no scalable glyphs are written; this is legal but confuses most current software. If n is 1, a single scalable glyph (the undefined glyph) is written; this is recommended, but triggers a bug in current versions of `FreeType`. If n is 2 (the default), a sufficiently high number of blank glyphs are written, which works with `FreeType` but increases file size.
- `-m n`
  Set the type of scalable metrics that we write. If n is 0, no scalable metrics are written, which may or may not be legal. If n is 1, full metrics for a single glyph are written, and only left sidebearing values are written for the other glyphs. If n is 2, scalable metrics for all glyphs are written, which increases file size and is not recommended. The default is 1.

---

End of options.

## BUGS

Some of the font-level values, notably sub- and superscript positions, are dummy values.

## SEE ALSO

`X(7)`, `Xserver(1)`, `Xft(3x)`. *Fonts in X11*.

## AUTHOR

The version of `Fonttosfnt` included in this X.Org Foundation release was originally written by Juliusz Chroboczek <jch@freedesktop.org> for the XFree86 project.

# FOOMATIC-CLEANUPDRIVERS

## NAME

foomatic-cleanupdrivers - Remove driver entries with no command line

## SYNOPSIS

`foomatic-cleanupdrivers [DBDIR]`

## DESCRIPTION

The `foomatic-cleanupdrivers` command removes all driver XML files which have an empty command line.

It is not intended to be called directly by the user.

# FOOMATIC-COMBO-XML

## NAME

foomatic-combo-xml - <put a short description here>

## SYNOPSIS

`foomatic-combo-xml [OPTION]...`

## DESCRIPTION

The Foomatic acceleration engine written in C (by Till), it computes printer/driver combo XML files and the printer overview XML file.

## EXIT STATUS

`foomatic-combo-xml` returns ???

## AUTHOR

Manfred Wassmann <manolo@NCC-1701.B.Shuttle.de> for the foomatic project using output from the associated binary.

## BUGS

This manpage needs editing.

Please post bug reports on
<http://lists.freestandards.org/mailman/listinfo/printing-foomatic>

# FOOMATIC-COMPILEDB

## NAME

foomatic-compiledb - Compile the Foomatic printer/driver database

## SYNOPSIS

`foomatic-compiledb [ -t type ] [ -f ] [ -j n ] [ driver ... ]`

## DESCRIPTION

`foomatic-compiledb` generates all PPD files or Foomatic combo XML files for all possible printer/driver combos, or only for a selected range of drivers. It generally should not be necessary except for people who want to generate a set of Foomatic data files for distribution. For configuring single printers `foomatic-ppdfile(1)` and especially `foomatic-configure(1)` will automagically compute just what they need.

### Options

- `-t type`
  Output file type, either ppd or xml.
- `-f`
  Force: Write into the destination directory even if it already exists.
- `-j n`
  n = number of work processes to run
- `driver ...`
  only generate data files for these driver(s)

## SEE ALSO

`foomatic-ppdfile(1)`, `foomatic-configure(1)`

## EXIT STATUS

`foomatic-compiledb` returns 0 unless something unexpected happens.

## AUTHORS

Manfred Wassmann <manolo@NCC-1701.B.Shuttle.de> and Till Kampeter <till.kampeter@gmail.com> for the foomatic project using output from the associated binary.

## BUGS

Existing files are always conserved instead of older files being overwritten. So deleting the destination directory (`rm -rf dir`) and calling `foomatic-compiledb` without the `-f` option is recommended.

Please post bug reports on

<http://lists.freestanders.org/mailman/listinfo/printing-foomatic>

# FOOMATIC-CONFIGURE

## NAME

foomatic-configure – the main configuration program of the foomatic printing system.

## SYNOPSIS

`foomatic-configure [OPTION]...`

`foomatic-configure -n queue name [ -N description ][ -L location ][ -c connect ][ -d driver ][ -p printer ][--ppd ppdfile ][ -s spooler ][ -C [ sourcespooler ] sourcequeue ][ -o option1=value1 -o ... ][ -q]`

`foomatic-configure -D -n queue name [ -s spooler ][ -q ]`

`foomatic-configure -R -n queue name [ -s spooler ][ -q ]`

`foomatic-configure -Q [ -s spooler ][ -n queue name ][ -r ]`

`foomatic-configure -P [ -s spooler ][ -n queue name ][ -d driver ][ -p printer ][-- ppd ppdfile ][ index ]`

`foomatic-configure -X -p printer | -d driver | -p printer -d driver`

`foomatic-configure -O`

`foomatic-configure -h`

`foomatic-configure --help`

## DESCRIPTION

`foomatic-configure` is a program to set up and configure print queues for every known spooler (CUPS, LPing, LPD, GNUlpr, PPR, PDQ. CPS, no spooler) and every valid printer/driver combo in the Foomatic database or every PPD file coming with PostScript printers. As RIP filter (Raster Image Processor, translation from PostScript to the native language of the printer) always `foomatic-rip(1)` will be used, except for PPD files of PostScript printers under CUPS or PPR, they will be used without RIP filter.

It also comprises half of a programatic API for user tools: you can learn and control everything about the static properties of print queues here. With the sister program `foomatic-printjob(1)`, you can do everything related to the print queue’s dynamic state: submit jobs, and query, cancel, reorder, and redirect them.

### Options

- `-n queuename`
  Configure this print queue
- `-N Name/Description`
  Use this proper human-readable name/description
- `-L Location`
  Short phrase describing this printer’s location
- `-c connection`
  Printer is connected thusly (ex file:/dev/lp0)
- `-d driver`
  Foomatic database name for desired printer driver
- `-p printer`
  Foomatic id for printer
- `--ppd ppdfile`
  PPD file, for example the one supplied by the manufacturer of a PostScript printer
- `-s spooler`
  Explicit spooler type (cups, lpd, lprng, pdq, ppr, direct)
- `-o option=value`
  Set the default of option to value
- `-o option`
  Turn on option by default
- `-D`
  Set this queue as the default queue (just give `-n queuename`)
- `-R`
  Remove this whole queue entirely (just give `-n queuename`)
- `-C [ sourcespooler ] sourcequeue`
  Copy sourcequeue from sourcespooler (or the current one if sourcespooler is not given) into the queue given by `-n queuename` (of the current spooler).

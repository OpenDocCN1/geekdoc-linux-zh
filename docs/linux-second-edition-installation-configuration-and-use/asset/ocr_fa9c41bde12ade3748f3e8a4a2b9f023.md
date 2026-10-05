dvips for the generation of missing character sets). Corresponding printer modes are only preset for the listed resolution steps. The following listing shows the relevant section of mktexpk:

```
# /usr/bin/mktexpk
...
if test -z "$MODE" || test "$MODE" = xdefault; then
  case "$DBPI" in
    85) MODE=sun;
    100) MODE=nextscrn;
    180) MODE=toshiba;
    300) MODE=cx;
    400) MODE=nexthi;
    600) MODE=Ljfour;
    1270) MODE=lineone;
    *) echo "$sproname: Can't guess mode for $DBPI dpi devices." >&2
      echo "$sproname: Use a config file, or update me." >&2
      exit 1
  esac
fi
```

The Metafont program expects not only the required resolution as a parameter for the generation of a character set, but also additional information about the printer type. If the printer type is known, Metafont can evaluate .mf files in the /usr/share/texmf/metafont/misc directory. These files are listed, together with printer-specific data which allows the character sets to be optimized to the printer's peculiarities. For example, printers which make single pixels too thick generate thinner character sets to compensate for this fault. A typical entry in modes.mf looks more or less like this (which is for a Canon ink jet printer for 360 dpi):

```
% /usr/share/texmf/metafont/misc/modes.mf
% From sjwright@ci.compulink.co.uk, 9 February 1994.
mode_def btexen = % Canon BubbleJet 10ex
mode_param (pixels_per_inch, 360);
mode_param (thicker, .6);
mode_param (fillin, 0);
mode_param (o_correction, .6);
mode_common_setup_;
endef;
```

To generate a proper printout with this printer, you must insert the following line into the case statement in mktexpk:

```
# insert into /usr/bin/mktexpk
360) MODE=btexen;
```
# notify — Control Process Execution

Synopsis

```
csh
notify [%@job-id]...
```

Description

See jobs(1).

# nroff — Format Documents for Display or Line Printer

Synopsis

```
/usr/bin/nroff [-ehq] [-mname] [-nM] [-opag] [-raM] [-sM] [-Tname]
```

Description

nroff formats text in the named files for typewriter-like devices. See troff(1).
If you specify no argument, nroff reads the standard input. An argument
of of a dash (-) is taken to be a file name corresponding to the standard input.

Notes

Previous documentation incorrectly described the numeric register yr as being the "Last
two digits of current year". yr is in actually the number of years since 1900. To correctly
obtain the last two digits of the current year through the year 2099, you can include the
following definition of string register yy in a document to display a two-digit year. Note
that you can substitute any other one- or two-character register for yy.

+   * definition of string register yy--last two digits of yr
* use yr (# of years since 1900) if it is < 100
ie \n(yr<100 .ds yy \* else, subtract 100 from yr, store in ny
el \
nr ny \n(yr-100)
ie \n(yr>9) . \* use ny if it is two digits
ds yy \n(ny\)
* remove temporary number register yy
rr ny \}
el.ds yy 0
el \* if ny is one digit, append it to 0
as yy \n(ny
rr ny \}
\
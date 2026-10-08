# Appendix N. Converting DOS Batch Files to Shell Scripts

Quite a number of programmers learned scripting on a PC running DOS. Even the crippled DOS batch file language allowed writing some fairly powerful scripts and applications, though they often required extensive kludges and workarounds. Occasionally, the need still arises to convert an old DOS batch file to a UNIX script. This is generally not difficult, as DOS batch file operators are only a limited subset of the equivalent shell primitives.

Table N-1. Batch file keywords / variables / operators, and their shell equivalents

| Batch File Operator | Shell Script Equivalent | Meaning |
| --- | --- | --- |
| % | $ | command-line parameter prefix |
| / | - | command option flag |
| \ | / | directory path separator |
| == | = | (equal-to) string comparison test |
| ! == ! | != | (not equal-to) string comparison test |
| | | | pipe |
| @ | set +v | do not echo current command |
| * | * | filename "wild card" |
| > | > | file redirection (overwrite) |
| >> | >> | file redirection (append) |
| < | < | redirect stdin |
| %VAR% | $VAR | environmental variable |
| REM | # | comment |
| NOT | ! | negate following test |
| NUL | /dev/null | "black hole" for burying command output |
| ECHO | echo | echo (many more option in Bash) |
| ECHO. | echo | echo blank line |
| ECHO OFF | set +v | do not echo command(s) following |
| FOR %%VAR IN (LIST) DO | for in [list]; | "for" loop |
| :LABEL | none (unnecessary) | label |
| GOTO | none (use function) | jump to another location in the script |
| PAUSE | sleep | pause or wait an interval |
| CHOICE | case or select | menu choice |
| IF | if | if-test |
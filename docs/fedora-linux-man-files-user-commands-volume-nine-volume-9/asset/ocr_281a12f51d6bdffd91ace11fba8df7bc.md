compress temporaries with PROG; decompress them with PROG -d

+   -—debug

annotate the part of the line used to sort, and warn about questionable usage to stderr

+   —files0-from=F

read input from the files specified by NUL-terminated nas in file F; If F is - then read nas from standard input

+   -k, —key=KEYDEF

sort via a key; KEYDEF gives location and type

+   -m, —rgE

rgE already sorted files; do not sort

+   -0, —output=FILE

write result to FILE instead of standard output

+   -s, —stable

stabilize sort by disabling last-resort comparison

+   -S, —buffer-size=SIZE

use SIZE for main mory buffer

+   -t, —field-separator=SEP

use SEP instead of non-blank to blank transition

+   -T, —temporary-directory=DIR

use DIR for temporaries, not $TMPDIR or /tmp; multiple options specify multiple directories

+   —parallel=N

change the nuer of sorts run concurrently to N

+   -u, —unique

with -c, check for strict ordering; without -c, output only the first of an equal run

+   -z, —zero-terminated

line delimiter is NUL, not newline

+   —help

display this help and exit

+   —version

output version information and exit

KEYDEF is F[.C][OPTS][,F[.C][OPTS]] for start and stop position, where F is a field nuer and C a character position in the field; both are origin 1, and the stop position defaults to the line's end. If neither -t nor -b is in effect, characters in a field are counted from the beginning of the preceding whitespace. OPTS is one or more single-letter ordering options [bdfgiMhnRrV], which override global ordering options for that key. If no key is given, use the entire line as the key.

SIZE may be followed by the following lIpcative suffixes: % 1% of mory, b 1, K 1024 (default), and so on for M, G, T, P, E, Z, Y.

*** WARNING *** The locale specified by the environnt affects sort order. Set LC_ALL=C to get the traditional sort order that uses native byte values.
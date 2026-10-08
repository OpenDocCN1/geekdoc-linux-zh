# look — Find Words in the System Dictionary or Lines in Sorted List

# Synopsis

```
/usr/bin/look [-d] [-f] [-tc] string [filename]
```

# Description

The look command consults a sorted filename and prints all lines that begin with string. If you specify no file name, look uses /usr/share/lib/dict/words with collating sequence -cd. look limits the length of a search to 256 characters.

# Options

+   -d Dictionary order. Use only letters, digits, Tabs, and space characters in comparisons.

+   -f Fold case. Do not distinguish uppercase letters from lowercase letters in comparisons.

+   -tc Set termination character. Ignore all characters to the right of c string.

# Examples

The following example uses the default dictionary to list all lines that begin with the string sun.

```
castle@ look sun
sun
sunbeam
sunbonnet
sunburn
sunburnt
Sunday
sunder
sundew
sundial
sundown
sundry
sfish
sunflower
sung
sunglasses
sunk
sunken
sunlight
sunlit
sunny
Sunnyvale
sunrise
screens
```
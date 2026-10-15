
# CRUNCH(1)
General Commands Manual
CRUNCH(1)

## NAME
`crunch` - generate wordlists from a character set

## SYNOPSIS
`crunch <min-len> <max-len> [<charset string>] [options]`

## DESCRIPTION
Crunch can create a wordlist based on criteria you specify. The output from crunch can be sent to the screen, file, or to another program. The required parameters are:

### `min-len`
The minimum length string you want crunch to start at. This option is required even for parameters that won't use the value.

### `max-len`
The maximum length string you want crunch to end at. This option is required even for parameters that won't use the value.

### `charset string`
You may specify character sets for crunch to use on the command line or if you leave it blank crunch will use the default character sets. The order MUST BE lower case characters, upper case characters, numbers, and then symbols. If you don't follow this order you will not get the results you want. You MUST specify either values for the character type or a plus sign.

NOTE: If you want to include the space character in your character set you must escape it using the `\` character or enclose your character set in quotes i.e. `"abc "`. See the examples 3, 11, 12, and 13 for examples.

## OPTIONS

### `-b number[type]`
Specifies the size of the output file, only works if `-o START` is used, i.e.: `60MB` The output files will be in the format of starting letter-ending letter for example: `./crunch45-b 20mb -o START` will generate 4 files: `aaaa-gfved.txt`, `gfzee-omgbw.txt`, `omgbz-wcydu.txt`, `wcydu-zzzzz.txt` valid values for type are `kb`, `mb`, `gb`, `kib`, `mib`, and `gib`. The first three types are based on 1000 while the last three types are based on 1024. NOTE There is no space between the number and type. For example `500mb` is correct `500 mb` is NOT correct.

### `-t @%,$" `
Specifies a pattern, eg: `@@@@@@@%@@@` where the only the `@`'s, `,'`s, `$`'s, and `^`'s will change.
`@` will insert lower case characters
`,` will insert upper case characters
`%` will insert numbers
`"` will insert symbols

尽管这里显示了一些关于 `crunch` 的基本信息，但我们确实需要查看 man 页面来理解如何使用 `crunch`。

```bash
kali > man crunch
```

在这里，我们可以看到为了高效使用 `crunch` 的所有关键选项。如果我们往下滚动一点，可以看到用于与 `-t` 选项配合使用的模式指定通配符。

## EXAMPLES

### Example 1
`crunch 1 8`
`crunch` will display a wordlist that starts at a and ends at zzzzzzzz

### Example 2
`crunch 1 6 abcdefg`
`crunch` will display a wordlist using the character set `abcdefg` that starts at a and ends at gggggg

### Example 3
`crunch 1 6 abcdeg\`
`crunch 1 6 abcdeg\`
there is a space at the end of the character string. In order for crunch to use the space you will need to escape it using the `\` character. In this example you could also put quotes around the letters and not need the `\"`, i.e. `"abcdefg"`. Crunch will display a wordlist using the character set abcdefg that starts at a and ends at (6 spaces)

### Example 4
`crunch 1 8 -f charset.lst mixalpha-numeric-all-space -o wordlist.txt`
`crunch` will use the `mixalpha-numeric-all-space` character set from `charset.lst` and will write the wordlist to a file named `wordlist.txt`. The file will start with a and end with "                "

### Example 5
`crunch 8 8 -f charset.lst mixalpha-numeric-all-space -o wordlist.txt -t @dgg@@@ -s cbdogaaa`
`crunch` should generate a 8 character wordlist using the `mixalpha-number-all-space` character set from `charset.lst` and will write the wordlist to a file named `wordlist.txt`. The file will start at `cbdogaaa` and end at " dog "

### Example 6
`crunch 2 3 -f charset.lst walpha -s BB`
`crunch` with start generating a wordlist at `BB` and end with `ZZZ`. This is useful if you have to stop generating a wordlist in the middle. Just do a tail `wordlist.txt` and set the `-s` parameter to the next word in the sequence. Be sure to rename the original wordlist BEFORE you begin as crunch will overwrite the existing wordlist.

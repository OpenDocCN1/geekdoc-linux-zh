tcsh. Compared to csh, tcsh added additional command history features, Emacs and vi-style command editing editing, spelling correction, other improvements intended for interactive use. Early versions of Apple's OS used tcsh as the default shell. It is still the default root shell on several BSD distributions.

tcsh, like the C shell, is not POSIX compliant as we can see here:

```
#!/usr/bin/tcsh

# longest-word.tcsh : find longest string in a file

foreach i ($argv)
    set max_word=""
    set max_len=0
    foreach j ($strings $i)
        set len=$j
        if [$len > $max_len] then
            set max_word=$j
            set max_len=$len
        fi
    end
echo "$1 $max_word ($max_len characters)""
```

Our tcsh version of the script demonstrates many differences from Bourne syntax. In C shell, most of the flow control statements are different. We see for example, that the outer loop starts with a foreach statement incrementing the variable $i with succeeding values from the list $argv.argv, taken from the C programming language, refers to an array containing the list of command arguments.

While this script works, tcsh is not very capable when things get complicated. It has two major weaknesses. First, it does not support user-defined functions. As a workaround, separate scripts can be called from the main script to carry out the individual functions. Second, many complex constructs is easily accomplished with the POSIX shell, such as:

```
{ if [ "Sa" ]; then
grep "string1"
else
grep "string2"
fi
}< file.txt
```

are not possible because the C shell parser cannot handle redirection with flow control statements. The parser also allows making quoting very troublesome.

# ksh - Korn Shell

The Korn shell comes in several different flavors. Basically, there are two groups, ksh88 and ksh93, reflecting the year of their release. There is a public domain version of ksh88 pdksh, and more official versions of both ksh88 and ksh93. All three are available for Linux. ksh93 would be the preferred version for most users, as it is the version found

144 Other Shells
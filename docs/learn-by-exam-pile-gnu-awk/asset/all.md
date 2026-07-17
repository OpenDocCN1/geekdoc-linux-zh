![](media/gawk.png)

1.  [Cover](text/cover.xhtml)
2.  [Table of contents](#nav.xhtml_toc)

# Preface

When it comes to command line text processing, from an abstract point of view, there are three major pillars — `grep` for filtering, `sed` for substitution and `awk` for field processing. These tools have some overlapping features too, for example, all three of them have extensive filtering capabilities.

Unlike `grep` and `sed`, `awk` is a full blown programming language. However, this book intends to showcase `awk` one-liners that can be composed from the command line instead of writing a program file.

This book heavily leans on examples to present options and features of `awk` one by one. It is recommended that you manually type each example and experiment with them. Understanding both the nature of sample input string and the output produced is essential. As an analogy, consider learning to drive a bike or a car — no matter how much you read about them or listen to explanations, you need to practice a lot and infer your own conclusions. Should you feel that copy-paste is ideal for you, [code snippets are available chapter wise on GitHub](https://github.com/learnbyexample/learn_gnuawk/tree/master/code_snippets).

## Prerequisites

*   Prior experience working with command line and `bash` shell, should know concepts like file redirection, command pipeline and so on
*   Familiarity with programming concepts like variables, printing, functions, control structures, arrays, etc
*   Knowing basics of `grep` and `sed` will help in understanding similar features of `awk`

If you are new to the world of command line, check out my curated resources on [Linux CLI and Shell scripting](https://learnbyexample.github.io/curated_resources/linux_cli_scripting.html) before starting this book.

My [Command Line Text Processing](https://github.com/learnbyexample/Command-line-text-processing) repository includes a chapter on `GNU awk` which has been edited and restructured to create this book.

## Conventions

*   The examples presented here have been tested on `GNU bash` shell with **GNU awk 5.1.0** and includes features not available in earlier versions.
*   Code snippets shown are copy pasted from `bash` shell and modified for presentation purposes. Some commands are preceded by comments to provide context and explanations. Blank lines have been added to improve readability, only `real` time is shown for speed comparisons, output is skipped for commands like `wget` and so on.
*   Unless otherwise noted, all examples and explanations are meant for **ASCII** characters.
*   `awk` would mean `GNU awk`, `grep` would mean `GNU grep` and so on unless otherwise specified.
*   External links are provided for further reading throughout the book. Not necessary to immediately visit them. They have been chosen with care and would help, especially during re-reads.
*   The [learn_gnuawk repo](https://github.com/learnbyexample/learn_gnuawk) has all the code snippets and files used in examples, exercises and other details related to the book. If you are not familiar with `git` command, click the **Code** button on the webpage to get the files.

## Acknowledgements

*   [GNU awk documentation](https://www.gnu.org/software/gawk/manual/) — manual and examples
*   [stackoverflow](https://stackoverflow.com/) and [unix.stackexchange](https://unix.stackexchange.com/) — for getting answers to pertinent questions on `bash`, `awk` and other commands
*   [tex.stackexchange](https://tex.stackexchange.com/) — for help on [pandoc](https://github.com/jgm/pandoc/) and `tex` related questions
*   [LibreOffice Draw](https://www.libreoffice.org/discover/draw/) — cover image
*   [pngquant](https://pngquant.org/) and [svgcleaner](https://github.com/RazrFalcon/svgcleaner) for optimizing images
*   [softwareengineering.stackexchange](https://softwareengineering.stackexchange.com/questions/39/whats-your-favourite-quote-about-programming) and [skolakoda](https://skolakoda.org/programming-quotes) for programming quotes
*   [Warning](https://commons.wikimedia.org/wiki/File:Warning_icon.svg) and [Info](https://commons.wikimedia.org/wiki/File:Info_icon_002.svg) icons by [Amada44](https://commons.wikimedia.org/wiki/User:Amada44) under public domain
*   [arifmahmudrana](https://github.com/arifmahmudrana) for spotting an ambiguous explanation

Special thanks to all my friends and online acquaintances for their help, support and encouragement, especially during these difficult times.

## Feedback and Errata

I would highly appreciate if you'd let me know how you felt about this book, it would help to improve this book as well as my future attempts. Also, please do let me know if you spot any error or typo.

Issue Manager: [https://github.com/learnbyexample/learn_gnuawk/issues](https://github.com/learnbyexample/learn_gnuawk/issues)

E-mail: [learnbyexample.net@gmail.com](mailto:learnbyexample.net@gmail.com)

Twitter: [https://twitter.com/learn_byexample](https://twitter.com/learn_byexample)

## Author info

Sundeep Agarwal is a freelance trainer, author and mentor. His previous experience includes working as a Design Engineer at Analog Devices for more than 5 years. You can find his other works, primarily focused on Linux command line, text processing, scripting languages and curated lists, at [https://github.com/learnbyexample](https://github.com/learnbyexample). He has also been a technical reviewer for [Command Line Fundamentals](https://www.packtpub.com/application-development/command-line-fundamentals) book and video course published by Packt.

**List of books:** [https://learnbyexample.github.io/books/](https://learnbyexample.github.io/books/)

## License

This work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-nc-sa/4.0/)

Code snippets are available under [MIT License](https://github.com/learnbyexample/learn_gnuawk/blob/master/LICENSE)

Resources mentioned in Acknowledgements section are available under original licenses.

## Book version

1.3

See [Version_changes.md](https://github.com/learnbyexample/learn_gnuawk/blob/master/Version_changes.md) to track changes across book versions.

# Installation and Documentation

The command name `awk` is derived from its developers — Alfred V. **A**ho, Peter J. **W**einberger, and Brian W. **K**ernighan. Over the years, it has been adapted and modified by various other developers. See [gawk manual: History](https://www.gnu.org/software/gawk/manual/gawk.html#History) for more details. This chapter will show how to install or upgrade `awk` followed by details related to documentation.

## Installation

If you are on a Unix like system, you are most likely to already have some version of `awk` installed. This book is primarily for `GNU awk`. As there are syntax and feature differences between various implementations, please make sure to follow along with what is presented here. `GNU awk` is part of [text creation and manipulation](https://www.gnu.org/manual/manual.html) commands provided by `GNU`. To install newer or particular version, visit [gnu: software gawk](https://www.gnu.org/software/gawk/). Check [release notes](https://lists.gnu.org/archive/cgi-bin/namazu.cgi?query=gawk+released&submit=Search%21&idxname=info-gnu&max=20&result=normal&sort=date%3Alate) for an overview of changes between versions.

```
[](#cb1-1)$ # use a dir, say ~/Downloads/awk_install before following the steps below
[](#cb1-2)$ wget https://ftp.gnu.org/gnu/gawk/gawk-5.1.0.tar.xz
[](#cb1-3)$ tar -Jxf gawk-5.1.0.tar.xz
[](#cb1-4)$ cd gawk-5.1.0/
[](#cb1-5)$ ./configure
[](#cb1-6)$ make
[](#cb1-7)$ sudo make install
[](#cb1-8)
[](#cb1-9)$ type -a awk
[](#cb1-10)awk is /usr/local/bin/awk
[](#cb1-11)awk is /usr/bin/awk
[](#cb1-12)$ awk --version | head -n1
[](#cb1-13)GNU Awk 5.1.0, API: 3.0
```

> ![info](media/file0.svg) See also [gawk manual: Installation](https://www.gnu.org/software/gawk/manual/html_node/Installation.html) for advanced options and instructions to install `awk` on other platforms.

## Documentation

It is always a good idea to know where to find the documentation. From command line, you can use `man awk` for a short manual and `info awk` for full documentation. The [online GNU awk manual](https://www.gnu.org/software/gawk/manual/) has a better reading interface and provides the most complete documentation, examples and information about other `awk` versions, POSIX standard, etc.

Here's a snippet from `man awk`:

```
[](#cb2-1)$ man awk
[](#cb2-2)GAWK(1)                        Utility Commands                        GAWK(1) 
[](#cb2-3) 
[](#cb2-4)NAME
[](#cb2-5)       gawk - pattern scanning and processing language
[](#cb2-6)
[](#cb2-7)SYNOPSIS
[](#cb2-8)       gawk [ POSIX or GNU style options ] -f program-file [ -- ] file ...
[](#cb2-9)       gawk [ POSIX or GNU style options ] [ -- ] program-text file ...
[](#cb2-10)
[](#cb2-11)DESCRIPTION
[](#cb2-12)       Gawk  is  the  GNU Project's implementation of the AWK programming lan‐
[](#cb2-13) guage.  It conforms to the definition of  the  language  in  the  POSIX
[](#cb2-14) 1003.1  Standard.   This version in turn is based on the description in
[](#cb2-15) The AWK Programming Language, by Aho, Kernighan, and Weinberger.   Gawk
[](#cb2-16) provides  the additional features found in the current version of Brian
[](#cb2-17) Kernighan's awk and numerous GNU-specific extensions.
```

## Options overview

For a quick overview of all the available options, use `awk --help` from the command line.

```
[](#cb3-1)$ awk --help
[](#cb3-2)Usage: awk [POSIX or GNU style options] -f progfile [--] file ...
[](#cb3-3)Usage: awk [POSIX or GNU style options] [--] 'program' file ...
[](#cb3-4)POSIX options:                  GNU long options: (standard)
[](#cb3-5)    -f progfile                 --file=progfile
[](#cb3-6)    -F fs                       --field-separator=fs
[](#cb3-7)    -v var=val                  --assign=var=val
[](#cb3-8)Short options:                  GNU long options: (extensions)
[](#cb3-9)    -b                          --characters-as-bytes
[](#cb3-10)    -c                          --traditional
[](#cb3-11)    -C                          --copyright
[](#cb3-12)    -d[file]                    --dump-variables[=file]
[](#cb3-13)    -D[file]                    --debug[=file]
[](#cb3-14)    -e 'program-text'           --source='program-text'
[](#cb3-15)    -E file                     --exec=file
[](#cb3-16)    -g                          --gen-pot
[](#cb3-17)    -h                          --help
[](#cb3-18)    -i includefile              --include=includefile
[](#cb3-19)    -l library                  --load=library
[](#cb3-20)    -L[fatal|invalid|no-ext]    --lint[=fatal|invalid|no-ext]
[](#cb3-21)    -M                          --bignum
[](#cb3-22)    -N                          --use-lc-numeric
[](#cb3-23)    -n                          --non-decimal-data
[](#cb3-24)    -o[file]                    --pretty-print[=file]
[](#cb3-25)    -O                          --optimize
[](#cb3-26)    -p[file]                    --profile[=file]
[](#cb3-27)    -P                          --posix
[](#cb3-28)    -r                          --re-interval
[](#cb3-29)    -s                          --no-optimize
[](#cb3-30)    -S                          --sandbox
[](#cb3-31)    -t                          --lint-old
[](#cb3-32)    -V                          --version
```

# awk introduction

This chapter will give an overview of `awk` syntax and some examples to show what kind of problems you could solve using `awk`. These features will be covered in depth in later chapters, but don't go skipping this chapter.

## Filtering

`awk` provides filtering capabilities like those supported by `grep` and `sed` plus some nifty features of its own. And similar to many command line utilities, `awk` can accept input from both `stdin` and files.

```
[](#cb4-1)$ # sample stdin data
[](#cb4-2)$ printf 'gate\napple\nwhat\nkite\n'
[](#cb4-3)gate
[](#cb4-4)apple
[](#cb4-5)what
[](#cb4-6)kite
[](#cb4-7)
[](#cb4-8)$ # same as: grep 'at' and sed -n '/at/p'
[](#cb4-9)$ # print all lines containing 'at'
[](#cb4-10)$ printf 'gate\napple\nwhat\nkite\n' | awk '/at/'
[](#cb4-11)gate
[](#cb4-12)what
[](#cb4-13)
[](#cb4-14)$ # same as: grep -v 'e' and sed -n '/e/!p'
[](#cb4-15)$ # print all lines NOT containing 'e'
[](#cb4-16)$ printf 'gate\napple\nwhat\nkite\n' | awk '!/e/'
[](#cb4-17)what
```

Similar to `grep` and `sed`, by default `awk` automatically loops over input content line by line. You can then use `awk`'s programming instructions to process those lines. As `awk` is primarily used from the command line, many shortcuts are available to reduce the amount of typing needed.

In the above examples, a regular expression (defined by the pattern between a pair of forward slashes) has been used to filter the input. Regular expressions (regexp) will be covered in detail in the next chapter, only simple string value is used here without any special characters. The full syntax is `string ~ /regexp/` to check if the given string matches the regexp and `string !~ /regexp/` to check if doesn't match. When the string isn't specified, the test is performed against a special variable `$0`, which has the contents of the input line. The correct term would be input **record**, but that's a discussion for a later chapter.

Also, in the above examples, only the filtering condition was given and nothing about what should be done. By default, when the condition evaluates to `true`, the contents of `$0` is printed. Thus:

*   `awk '/regexp/'` is a shortcut for `awk '$0 ~ /regexp/{print $0}'`
*   `awk '!/regexp/'` is a shortcut for `awk '$0 !~ /regexp/{print $0}'`

```
[](#cb5-1)$ # same as: awk '/at/'
[](#cb5-2)$ printf 'gate\napple\nwhat\nkite\n' | awk '$0 ~ /at/{print $0}'
[](#cb5-3)gate
[](#cb5-4)what
[](#cb5-5)
[](#cb5-6)$ # same as: awk '!/e/'
[](#cb5-7)$ printf 'gate\napple\nwhat\nkite\n' | awk '$0 !~ /e/{print $0}'
[](#cb5-8)what
```

In the above examples, `{}` is used to specify a block of code to be executed when the condition that precedes the block evaluates to `true`. One or more statements can be given separated by `;` character. You'll see such examples and learn more about `awk` syntax later.

Any non-zero numeric value and non-empty string value is considered as `true` when that value is used as a conditional expression. Idiomatically, `1` is used to denote a `true` condition in one-liners as a shortcut to print the contents of `$0`.

```
[](#cb6-1)$ # same as: printf 'gate\napple\nwhat\nkite\n' | cat
[](#cb6-2)$ # same as: awk '{print $0}'
[](#cb6-3)$ printf 'gate\napple\nwhat\nkite\n' | awk '1'
[](#cb6-4)gate
[](#cb6-5)apple
[](#cb6-6)what
[](#cb6-7)kite
```

## Substitution

`awk` has three functions to cover search and replace requirements. Two of them are shown below. The `sub` function replaces only the first match whereas `gsub` function replaces all the matching occurrences. By default, these functions operate on `$0` when the input string isn't provided. Both `sub` and `gsub` modifies the input source on successful substitution.

```
[](#cb7-1)$ # for each input line, change only first ':' to '-'
[](#cb7-2)$ # same as: sed 's/:/-/'
[](#cb7-3)$ printf '1:2:3:4\na:b:c:d\n' | awk '{sub(/:/, "-")} 1'
[](#cb7-4)1-2:3:4
[](#cb7-5)a-b:c:d
[](#cb7-6)
[](#cb7-7)$ # for each input line, change all ':' to '-'
[](#cb7-8)$ # same as: sed 's/:/-/g'
[](#cb7-9)$ printf '1:2:3:4\na:b:c:d\n' | awk '{gsub(/:/, "-")} 1'
[](#cb7-10)1-2-3-4
[](#cb7-11)a-b-c-d
```

The first argument to `sub` and `gsub` functions is the regexp to be matched against the input content. The second argument is the replacement string. String literals are specified within double quotes. In the above examples, `sub` and `gsub` are used inside a block as they aren't intended to be used as a conditional expression. The `1` after the block is treated as a conditional expression as it is used outside a block. You can also use the variations presented below to get the same results.

*   `awk '{sub(/:/, "-")} 1'` is same as `awk '{sub(/:/, "-"); print $0}'`
*   You can also just use `print` instead of `print $0` as `$0` is the default string

> ![info](media/file0.svg) You might wonder why to use or learn `grep` and `sed` when you can achieve same results with `awk`. It depends on the problem you are trying to solve. A simple line filtering will be faster with `grep` compared to `sed` or `awk` because `grep` is optimized for such cases. Similarly, `sed` will be faster than `awk` for substitution cases. Also, not all features easily translate among these tools. For example, `grep -o` requires lot more steps to code with `sed` or `awk`. Only `grep` offers recursive search. And so on. See also [unix.stackexchange: When to use grep, sed, awk, perl, etc](https://unix.stackexchange.com/q/303044/109046).

## Field processing

As mentioned before, `awk` is primarily used for field based processing. Consider the sample input file shown below with fields separated by a single space character.

> ![info](media/file0.svg) The [learn_gnuawk repo](https://github.com/learnbyexample/learn_gnuawk/tree/master/example_files) has all the files used in examples.

```
[](#cb8-1)$ cat table.txt
[](#cb8-2)brown bread mat hair 42
[](#cb8-3)blue cake mug shirt -7
[](#cb8-4)yellow banana window shoes 3.14
```

Here's some examples that is based on specific field rather than entire line. By default, `awk` splits the input line based on spaces and the field contents can be accessed using `$N` where `N` is the field number required. A special variable `NF` is updated with the total number of fields for each input line. There's more details to cover, but for now this is enough to proceed.

```
[](#cb9-1)$ # print the second field of each input line
[](#cb9-2)$ awk '{print $2}' table.txt
[](#cb9-3)bread
[](#cb9-4)cake
[](#cb9-5)banana
[](#cb9-6)
[](#cb9-7)$ # print lines only if the last field is a negative number
[](#cb9-8)$ # recall that the default action is to print the contents of $0
[](#cb9-9)$ awk '$NF<0' table.txt
[](#cb9-10)blue cake mug shirt -7
[](#cb9-11)
[](#cb9-12)$ # change 'b' to 'B' only for the first field
[](#cb9-13)$ awk '{gsub(/b/, "B", $1)} 1' table.txt
[](#cb9-14)Brown bread mat hair 42
[](#cb9-15)Blue cake mug shirt -7
[](#cb9-16)yellow banana window shoes 3.14
```

## awk one-liner structure

The examples in previous sections used a few different ways to construct a typical `awk` one-liner. If you haven't yet grasped the syntax, this generic structure might help:

`awk 'cond1{action1} cond2{action2} ... condN{actionN}'`

If a condition isn't provided, the action is always executed. Within a block, you can provide multiple statements separated by semicolon character. If action isn't provided, then by default, contents of `$0` variable is printed if the condition evaluates to `true`. When action isn't present, you can use semicolon to terminate a condition and start another `condX{actionX}` snippet.

Note that multiple blocks are just a syntactical sugar. It helps to avoid explicit use of `if` control structure for most one-liners. The below snippet shows the same code with and without `if` structure.

```
[](#cb10-1)$ awk '{
[](#cb10-2) if($NF < 0){
[](#cb10-3) print $0
[](#cb10-4) }
[](#cb10-5) }' table.txt
[](#cb10-6)blue cake mug shirt -7
[](#cb10-7)
[](#cb10-8)$ awk '$NF<0' table.txt
[](#cb10-9)blue cake mug shirt -7
```

You can use a `BEGIN{}` block when you need to execute something before the input is read and a `END{}` block to execute something after all of the input has been processed.

```
[](#cb11-1)$ seq 2 | awk 'BEGIN{print "---"} 1; END{print "%%%"}'
[](#cb11-2)---
[](#cb11-3)1
[](#cb11-4)2
[](#cb11-5)%%%
```

There are some more types of blocks that can be used, you'll see them in coming chapters. See [gawk manual: Operators](https://www.gnu.org/software/gawk/manual/gawk.html#All-Operators) for details about operators and [gawk manual: Truth Values and Conditions](https://www.gnu.org/software/gawk/manual/gawk.html#Truth-Values-and-Conditions) for conditional expressions.

## Strings and Numbers

Some examples so far have already used string and numeric literals. As mentioned earlier, `awk` tries to provide a concise way to construct a solution from the command line. The data type of a value is determined based on the syntax used. String literals are represented inside double quotes. Numbers can be integers or floating point. Scientific notation is allowed as well. See [gawk manual: Constant Expressions](https://www.gnu.org/software/gawk/manual/gawk.html#Constants) for more details.

```
[](#cb12-1)$ # BEGIN{} is also useful to write awk program without any external input
[](#cb12-2)$ awk 'BEGIN{print "hi"}'
[](#cb12-3)hi
[](#cb12-4)
[](#cb12-5)$ awk 'BEGIN{print 42}'
[](#cb12-6)42
[](#cb12-7)$ awk 'BEGIN{print 3.14}'
[](#cb12-8)3.14
[](#cb12-9)$ awk 'BEGIN{print 34.23e4}'
[](#cb12-10)342300
```

You can also save these literals in variables and use it later. Some variables are predefined, for example `NF`.

```
[](#cb13-1)$ awk 'BEGIN{a=5; b=2.5; print a+b}'
[](#cb13-2)7.5
[](#cb13-3)
[](#cb13-4)$ # strings placed next to each other are concatenated
[](#cb13-5)$ awk 'BEGIN{s1="con"; s2="cat"; print s1 s2}'
[](#cb13-6)concat
```

If uninitialized variable is used, it will act as empty string in string context and `0` in numeric context. You can force a string to behave as a number by simply using it in an expression with numeric values. You can also use unary `+` or `-` operators. If the string doesn't start with a valid number (ignoring any starting whitespaces), it will be treated as `0`. Similarly, concatenating a string to a number will automatically change the number to string. See [gawk manual: How awk Converts Between Strings and Numbers](https://www.gnu.org/software/gawk/manual/gawk.html#Strings-And-Numbers) for more details.

```
[](#cb14-1)$ # same as: awk 'BEGIN{sum=0} {sum += $NF} END{print sum}'
[](#cb14-2)$ awk '{sum += $NF} END{print sum}' table.txt
[](#cb14-3)38.14
[](#cb14-4)
[](#cb14-5)$ awk 'BEGIN{n1="5.0"; n2=5; if(n1==n2) print "equal"}'
[](#cb14-6)$ awk 'BEGIN{n1="5.0"; n2=5; if(+n1==n2) print "equal"}'
[](#cb14-7)equal
[](#cb14-8)$ awk 'BEGIN{n1="5.0"; n2=5; if(n1==n2".0") print "equal"}'
[](#cb14-9)equal
[](#cb14-10)
[](#cb14-11)$ awk 'BEGIN{print 5 + "abc 2 xyz"}'
[](#cb14-12)5
[](#cb14-13)$ awk 'BEGIN{print 5 + " \t 2 xyz"}'
[](#cb14-14)7
```

## Arrays

Arrays in `awk` are associative, meaning they are key-value pairs. The keys can be numbers or strings, but numbers get converted to strings internally. They can be multi-dimensional as well. There will be plenty of array examples in later chapters in relevant context. See [gawk manual: Arrays](https://www.gnu.org/software/gawk/manual/gawk.html#Arrays) for complete details and gotchas.

```
[](#cb15-1)$ # assigning an array and accessing an element based on string key
[](#cb15-2)$ awk 'BEGIN{student["id"] = 101; student["name"] = "Joe";
[](#cb15-3) print student["name"]}'
[](#cb15-4)Joe
[](#cb15-5)
[](#cb15-6)$ # checking if a key exists
[](#cb15-7)$ awk 'BEGIN{student["id"] = 101; student["name"] = "Joe";
[](#cb15-8) if("id" in student) print "Key found"}'
[](#cb15-9)Key found
```

## Summary

In my early days of getting used to the Linux command line, I was intimidated by `sed` and `awk` examples and didn't even try to learn them. Hopefully, this gentler introduction works for you and the various syntactical magic has been explained adequately. Try to experiment with the given examples, for example change field number to something other than the number used. Be curious, like what happens if field number is negative or a floating-point number. Read the manual. Practice a lot.

Next chapter is dedicated solely for regular expressions. The features introduced in this chapter would be used in the examples, so make sure you are comfortable with `awk` syntax before proceeding. And, do solve the exercises coming up in the next section.

## Exercises

> ![info](media/file0.svg) Exercise related files are available from [exercises folder of learn_gnuawk repo](https://github.com/learnbyexample/learn_gnuawk/tree/master/exercises). All the exercises are also collated together in one place at [Exercises.md](https://github.com/learnbyexample/learn_gnuawk/blob/master/exercises/Exercises.md). For solutions, see [Exercise_solutions.md](https://github.com/learnbyexample/learn_gnuawk/blob/master/exercises/Exercise_solutions.md).

**a)** For the input file `addr.txt`, display all lines containing `is`.

```
[](#cb16-1)$ cat addr.txt
[](#cb16-2)Hello World
[](#cb16-3)How are you
[](#cb16-4)This game is good
[](#cb16-5)Today is sunny
[](#cb16-6)12345
[](#cb16-7)You are funny
[](#cb16-8)
[](#cb16-9)$ awk ##### add your solution here
[](#cb16-10)This game is good
[](#cb16-11)Today is sunny
```

**b)** For the input file `addr.txt`, display first field of lines *not* containing `y`. Consider space as the field separator for this file.

```
[](#cb17-1)$ awk ##### add your solution here
[](#cb17-2)Hello
[](#cb17-3)This
[](#cb17-4)12345
```

**c)** For the input file `addr.txt`, display all lines containing no more than 2 fields.

```
[](#cb18-1)$ awk ##### add your solution here
[](#cb18-2)Hello World
[](#cb18-3)12345
```

**d)** For the input file `addr.txt`, display all lines containing `is` in the second field.

```
[](#cb19-1)$ awk ##### add your solution here
[](#cb19-2)Today is sunny
```

**e)** For each line of the input file `addr.txt`, replace first occurrence of `o` with `0`.

```
[](#cb20-1)$ awk ##### add your solution here
[](#cb20-2)Hell0 World
[](#cb20-3)H0w are you
[](#cb20-4)This game is g0od
[](#cb20-5)T0day is sunny
[](#cb20-6)12345
[](#cb20-7)Y0u are funny
```

**f)** For the input file `table.txt`, calculate and display the product of numbers in the last field of each line. Consider space as the field separator for this file.

```
[](#cb21-1)$ cat table.txt
[](#cb21-2)brown bread mat hair 42
[](#cb21-3)blue cake mug shirt -7
[](#cb21-4)yellow banana window shoes 3.14
[](#cb21-5)
[](#cb21-6)$ awk ##### add your solution here
[](#cb21-7)-923.16
```

**g)** Append `.` to all the input lines for the given `stdin` data.

```
[](#cb22-1)$ printf 'last\nappend\nstop\ntail\n' | awk ##### add your solution here
[](#cb22-2)last.
[](#cb22-3)append.
[](#cb22-4)stop.
[](#cb22-5)tail.
```

# Regular Expressions

Regular Expressions is a versatile tool for text processing. It helps to precisely define a matching criteria. For learning and understanding purposes, one can view regular expressions as a mini programming language in itself, specialized for text processing. Parts of a regular expression can be saved for future use, analogous to variables and functions. There are ways to perform AND, OR, NOT conditionals, features to concisely define repetition to avoid manual replication and so on.

Here's some common use cases.

*   Sanitizing a string to ensure that it satisfies a known set of rules. For example, to check if a given string matches password rules.
*   Filtering or extracting portions on an abstract level like alphabets, numbers, punctuation and so on.
*   Qualified string replacement. For example, at the start or the end of a string, only whole words, based on surrounding text, etc.

This chapter will cover regular expressions as implemented in `awk`. Most of `awk`'s regular expression syntax is similar to Extended Regular Expression (ERE) found with `grep -E` and `sed -E`. Unless otherwise indicated, examples and descriptions will assume ASCII input.

> ![info](media/file0.svg) See also [POSIX specification](https://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap09.html) for regular expressions. And [unix.stackexchange: Why does my regular expression work in X but not in Y?](https://unix.stackexchange.com/q/119905/109046)

## Syntax and variable assignment

As seen in previous chapter, the syntax is `string ~ /regexp/` to check if the given string satisfies the rules specified by the regexp. And `string !~ /regexp/` to invert the condition. By default, `$0` is checked if the string isn't specified. You can also save a regexp literal in a variable by prefixing `@` symbol. The prefix is needed because `/regexp/` by itself would mean `$0 ~ /regexp/`.

```
[](#cb23-1)$ printf 'spared no one\ngrasped\nspar\n' | awk '/ed/'
[](#cb23-2)spared no one
[](#cb23-3)grasped
[](#cb23-4)
[](#cb23-5)$ printf 'spared no one\ngrasped\nspar\n' | awk 'BEGIN{r = @/ed/} $0 ~ r'
[](#cb23-6)spared no one
[](#cb23-7)grasped
```

## String Anchors

In the examples seen so far, the regexp was a simple string value without any special characters. Also, the regexp pattern evaluated to `true` if it was found anywhere in the string. Instead of matching anywhere in the string, restrictions can be specified. These restrictions are made possible by assigning special meaning to certain characters and escape sequences. The characters with special meaning are known as **metacharacters** in regular expressions parlance. In case you need to match those characters literally, you need to escape them with a `\` (discussed in [Matching the metacharacters](#ch004.xhtml_matching-the-metacharacters) section).

There are two string anchors:

*   `^` metacharacter restricts the matching to the start of string
*   `$` metacharacter restricts the matching to the end of string

```
[](#cb24-1)$ # string starting with 'sp'
[](#cb24-2)$ printf 'spared no one\ngrasped\nspar\n' | awk '/^sp/'
[](#cb24-3)spared no one
[](#cb24-4)spar
[](#cb24-5)
[](#cb24-6)$ # string ending with 'ar'
[](#cb24-7)$ printf 'spared no one\ngrasped\nspar\n' | awk '/ar$/'
[](#cb24-8)spar
[](#cb24-9)
[](#cb24-10)$ # change only whole string 'spar'
[](#cb24-11)$ # can also use: awk '/^spar$/{$0 = 123} 1' or awk '$0=="spar"{$0 = 123} 1'
[](#cb24-12)$ printf 'spared no one\ngrasped\nspar\n' | awk '{sub(/^spar$/, "123")} 1'
[](#cb24-13)spared no one
[](#cb24-14)grasped
[](#cb24-15)123
```

The anchors can be used by themselves as a pattern. Helps to insert text at the start or end of string, emulating string concatenation operations. These might not feel like useful capability, but combined with other features they become quite a handy tool.

```
[](#cb25-1)$ printf 'spared no one\ngrasped\nspar\n' | awk '{gsub(/^/, "* ")} 1'
[](#cb25-2)* spared no one
[](#cb25-3)* grasped
[](#cb25-4)* spar
[](#cb25-5)
[](#cb25-6)$ # append only if string doesn't contain space characters
[](#cb25-7)$ printf 'spared no one\ngrasped\nspar\n' | awk '!/ /{gsub(/$/, ".")} 1'
[](#cb25-8)spared no one
[](#cb25-9)grasped.
[](#cb25-10)spar.
```

> ![info](media/file0.svg) See also [Behavior of ^ and $ when string contains newline](#ch016.xhtml_behavior-of--and--when-string-contains-newline) section.

## Word Anchors

The second type of restriction is word anchors. A word character is any alphabet (irrespective of case), digit and the underscore character. You might wonder why there are digits and underscores as well, why not only alphabets? This comes from variable and function naming conventions — typically alphabets, digits and underscores are allowed. So, the definition is more programming oriented than natural language.

Use `\<` to indicate start of word anchor and `\>` to indicate end of word anchor. As an alternate, you can use `\y` to indicate both the start of word and end of word anchors.

> ![info](media/file0.svg) Typically `\b` is used to represent word anchor (for example, in `grep`, `sed`, `perl`, etc), but in `awk` the escape sequence `\b` refers to the backspace character.

```
[](#cb26-1)$ cat word_anchors.txt
[](#cb26-2)sub par
[](#cb26-3)spar
[](#cb26-4)apparent effort
[](#cb26-5)two spare computers
[](#cb26-6)cart part tart mart
[](#cb26-7)
[](#cb26-8)$ # words starting with 'par'
[](#cb26-9)$ awk '/\<par/' word_anchors.txt
[](#cb26-10)sub par
[](#cb26-11)cart part tart mart
[](#cb26-12)
[](#cb26-13)$ # words ending with 'par'
[](#cb26-14)$ awk '/par\>/' word_anchors.txt
[](#cb26-15)sub par
[](#cb26-16)spar
[](#cb26-17)
[](#cb26-18)$ # only whole word 'par'
[](#cb26-19)$ # note that only lines where substitution succeeded will be printed
[](#cb26-20)$ # as return value of sub/gsub is number of substitutions made
[](#cb26-21)$ awk 'gsub(/\<par\>/, "***")' word_anchors.txt
[](#cb26-22)sub ***
```

> ![warning](media/file1.svg) See also [Word boundary differences](#ch016.xhtml_word-boundary-differences) section.

`\y` has an opposite too. `\B` matches locations other than those places where the word anchor would match.

```
[](#cb27-1)$ # match 'par' if it is surrounded by word characters
[](#cb27-2)$ awk '/\Bpar\B/' word_anchors.txt
[](#cb27-3)apparent effort
[](#cb27-4)two spare computers
[](#cb27-5)
[](#cb27-6)$ # match 'par' but not as start of word
[](#cb27-7)$ awk '/\Bpar/' word_anchors.txt
[](#cb27-8)spar
[](#cb27-9)apparent effort
[](#cb27-10)two spare computers
[](#cb27-11)
[](#cb27-12)$ # match 'par' but not as end of word
[](#cb27-13)$ awk '/par\B/' word_anchors.txt
[](#cb27-14)apparent effort
[](#cb27-15)two spare computers
[](#cb27-16)cart part tart mart
```

Here's an example for using word boundaries by themselves as a pattern. It also neatly shows the opposite functionality of `\y` and `\B`.

```
[](#cb28-1)$ echo 'copper' | awk '{gsub(/\y/, ":")} 1'
[](#cb28-2):copper:
[](#cb28-3)$ echo 'copper' | awk '{gsub(/\B/, ":")} 1'
[](#cb28-4)c:o:p:p:e:r
```

> ![warning](media/file1.svg) Negative logic is handy in many text processing situations. But use it with care, you might end up matching things you didn't intend.

## Combining conditions

Before seeing the next regexp feature, it is good to note that sometimes using logical operators is easier to read and maintain compared to doing everything with regexp.

```
[](#cb29-1)$ # string starting with 'b' but not containing 'at'
[](#cb29-2)$ awk '/^b/ && !/at/' table.txt
[](#cb29-3)blue cake mug shirt -7
[](#cb29-4)
[](#cb29-5)$ # if the first field contains 'low' or the last field is less than 0
[](#cb29-6)$ awk '$1 ~ /low/ || $NF<0' table.txt
[](#cb29-7)blue cake mug shirt -7
[](#cb29-8)yellow banana window shoes 3.14
```

## Alternation

Many a times, you'd want to search for multiple terms. In a conditional expression, you can use the logical operators to combine multiple conditions. With regular expressions, the `|` metacharacter is similar to logical OR. The regular expression will match if any of the expression separated by `|` is satisfied. These can have their own independent anchors as well.

Alternation is similar to using `||` operator between two regexps. Having a single regexp helps to write terser code and `||` cannot be used when substitution is required.

```
[](#cb30-1)$ # match whole word 'par' or string ending with 's'
[](#cb30-2)$ # same as: awk '/\<par\>/ || /s$/'
[](#cb30-3)$ awk '/\<par\>|s$/' word_anchors.txt
[](#cb30-4)sub par
[](#cb30-5)two spare computers
[](#cb30-6)
[](#cb30-7)$ # replace 'cat' or 'dog' or 'fox' with '--'
[](#cb30-8)$ echo 'cats dog bee parrot foxed' | awk '{gsub(/cat|dog|fox/, "--")} 1'
[](#cb30-9)--s -- bee parrot --ed
```

There's some tricky situations when using alternation. If it is used for filtering a line, there is no ambiguity. However, for use cases like substitution, it depends on a few factors. Say, you want to replace `are` or `spared` — which one should get precedence? The bigger word `spared` or the substring `are` inside it or based on something else?

The alternative which matches earliest in the input gets precedence.

```
[](#cb31-1)$ # note that 'sub' is used here, so only first match gets replaced
[](#cb31-2)$ echo 'cats dog bee parrot foxed' | awk '{sub(/bee|parrot|at/, "--")} 1'
[](#cb31-3)c--s dog bee parrot foxed
[](#cb31-4)$ echo 'cats dog bee parrot foxed' | awk '{sub(/parrot|at|bee/, "--")} 1'
[](#cb31-5)c--s dog bee parrot foxed
```

In case of matches starting from same location, for example `spar` and `spared`, the longest matching portion gets precedence. Unlike other regular expression implementations, left-to-right priority for alternation comes into play only if length of the matches are the same. See [Longest match wins](#ch004.xhtml_longest-match-wins) and [Backreferences](#ch004.xhtml_backreferences) sections for more examples.

```
[](#cb32-1)$ echo 'spared party parent' | awk '{sub(/spa|spared/, "**")} 1'
[](#cb32-2)** party parent
[](#cb32-3)$ echo 'spared party parent' | awk '{sub(/spared|spa/, "**")} 1'
[](#cb32-4)** party parent
[](#cb32-5)
[](#cb32-6)$ # other implementations like 'perl' have left-to-right priority
[](#cb32-7)$ echo 'spared party parent' | perl -pe 's/spa|spared/**/'
[](#cb32-8)**red party parent
```

## Grouping

Often, there are some common things among the regular expression alternatives. It could be common characters or qualifiers like the anchors. In such cases, you can group them using a pair of parentheses metacharacters. Similar to `a(b+c)d = abd+acd` in maths, you get `a(b|c)d = abd|acd` in regular expressions.

```
[](#cb33-1)$ # without grouping
[](#cb33-2)$ printf 'red\nreform\nread\narrest\n' | awk '/reform|rest/'
[](#cb33-3)reform
[](#cb33-4)arrest
[](#cb33-5)$ # with grouping
[](#cb33-6)$ printf 'red\nreform\nread\narrest\n' | awk '/re(form|st)/'
[](#cb33-7)reform
[](#cb33-8)arrest
[](#cb33-9)
[](#cb33-10)$ # without grouping
[](#cb33-11)$ printf 'sub par\nspare\npart time\n' | awk '/\<par\>|\<part\>/'
[](#cb33-12)sub par
[](#cb33-13)part time
[](#cb33-14)$ # taking out common anchors
[](#cb33-15)$ printf 'sub par\nspare\npart time\n' | awk '/\<(par|part)\>/'
[](#cb33-16)sub par
[](#cb33-17)part time
[](#cb33-18)$ # taking out common characters as well
[](#cb33-19)$ # you'll later learn a better technique instead of using empty alternate
[](#cb33-20)$ printf 'sub par\nspare\npart time\n' | awk '/\<par(|t)\>/'
[](#cb33-21)sub par
[](#cb33-22)part time
```

## Matching the metacharacters

You have seen a few metacharacters and escape sequences that help to compose a regular expression. To match the metacharacters literally, i.e. to remove their special meaning, prefix those characters with a `\` character. To indicate a literal `\` character, use `\\`.

Unlike `grep` and `sed`, the string anchors have to be always escaped to match them literally as there is no BRE mode in `awk`. They do not lose their special meaning when not used in their customary positions.

```
[](#cb34-1)$ # awk '/b^2/' will not work even though ^ isn't being used as anchor
[](#cb34-2)$ # b^2 will work for both grep and sed if you use BRE syntax
[](#cb34-3)$ echo 'a^2 + b^2 - C*3' | awk '/b\^2/'
[](#cb34-4)a^2 + b^2 - C*3
[](#cb34-5)
[](#cb34-6)$ # note that ')' doesn't need to be escaped
[](#cb34-7)$ echo '(a*b) + c' | awk '{gsub(/\(|)/, "")} 1'
[](#cb34-8)a*b + c
[](#cb34-9)
[](#cb34-10)$ echo '\learn\by\example' | awk '{gsub(/\\/, "/")} 1'
[](#cb34-11)/learn/by/example
```

> ![info](media/file0.svg) [Backreferences](#ch004.xhtml_backreferences) section will discuss how to handle the metacharacters in replacement section.

## Using string literal as regexp

The first argument to `sub` and `gsub` functions can be a string as well, `awk` will handle converting it to a regexp. This has a few advantages. For example, if you have many `/` characters in the search pattern, it might become easier to use string instead of regexp.

```
[](#cb35-1)$ p='/home/learnbyexample/reports'
[](#cb35-2)$ echo "$p" | awk '{sub(/\/home\/learnbyexample\//, "~/")} 1'
[](#cb35-3)~/reports
[](#cb35-4)$ echo "$p" | awk '{sub("/home/learnbyexample/", "~/")} 1'
[](#cb35-5)~/reports
[](#cb35-6)
[](#cb35-7)$ # example with line matching instead of substitution
[](#cb35-8)$ printf '/foo/bar/1\n/foo/baz/1\n' | awk '/\/foo\/bar\//'
[](#cb35-9)/foo/bar/1
[](#cb35-10)$ printf '/foo/bar/1\n/foo/baz/1\n' | awk '$0 ~ "/foo/bar/"'
[](#cb35-11)/foo/bar/1
```

In the above examples, the string literal was supplied directly. But any other expression or variable can be used as well, examples for which will be shown later in this chapter. The reason why string isn't always used as the first argument is that the special meaning for `\` character will clash. For example:

```
[](#cb36-1)$ awk 'gsub("\<par\>", "X")' word_anchors.txt
[](#cb36-2)awk: cmd. line:1: warning: escape sequence `\<' treated as plain `<'
[](#cb36-3)awk: cmd. line:1: warning: escape sequence `\>' treated as plain `>'
[](#cb36-4)
[](#cb36-5)$ # you'll need \\ to represent \
[](#cb36-6)$ awk 'gsub("\\<par\\>", "X")' word_anchors.txt
[](#cb36-7)sub X
[](#cb36-8)$ # much more readable with regexp literal
[](#cb36-9)$ awk 'gsub(/\<par\>/, "X")' word_anchors.txt
[](#cb36-10)sub X
[](#cb36-11)
[](#cb36-12)$ # another example
[](#cb36-13)$ echo '\learn\by\example' | awk '{gsub("\\\\", "/")} 1'
[](#cb36-14)/learn/by/example
[](#cb36-15)$ echo '\learn\by\example' | awk '{gsub(/\\/, "/")} 1'
[](#cb36-16)/learn/by/example
```

> ![info](media/file0.svg) See [gawk manual: Gory details](https://www.gnu.org/software/gawk/manual/gawk.html#Gory-Details) for more information than you'd want.

## The dot meta character

The dot metacharacter serves as a placeholder to match any character (including the newline character). Later you'll learn how to define your own custom placeholder for limited set of characters.

```
[](#cb37-1)$ # 3 character sequence starting with 'c' and ending with 't'
[](#cb37-2)$ echo 'tac tin cot abc:tyz excited' | awk '{gsub(/c.t/, "-")} 1'
[](#cb37-3)ta-in - ab-yz ex-ed
[](#cb37-4)
[](#cb37-5)$ # any character followed by 3 and again any character
[](#cb37-6)$ printf '4\t35x\n' | awk '{gsub(/.3./, "")} 1'
[](#cb37-7)4x
[](#cb37-8)
[](#cb37-9)$ # 'c' followed by any character followed by 'x'
[](#cb37-10)$ awk 'BEGIN{s="abc\nxyz"; sub(/c.x/, " ", s); print s}'
[](#cb37-11)ab yz
```

## Quantifiers

As an analogy, alternation provides logical OR. Combining the dot metacharacter `.` and quantifiers (and alternation if needed) paves a way to perform logical AND. For example, to check if a string matches two patterns with any number of characters in between. Quantifiers can be applied to both characters and groupings. Apart from ability to specify exact quantity and bounded range, these can also match unbounded varying quantities.

First up, the `?` metacharacter which quantifies a character or group to match `0` or `1` times. This helps to define optional patterns and build terser patterns compared to groupings for some cases.

```
[](#cb38-1)$ # same as: awk '{gsub(/\<(fe.d|fed)\>/, "X")} 1'
[](#cb38-2)$ echo 'fed fold fe:d feeder' | awk '{gsub(/\<fe.?d\>/, "X")} 1'
[](#cb38-3)X fold X feeder
[](#cb38-4)
[](#cb38-5)$ # same as: awk '/\<par(|t)\>/'
[](#cb38-6)$ printf 'sub par\nspare\npart time\n' | awk '/\<part?\>/'
[](#cb38-7)sub par
[](#cb38-8)part time
[](#cb38-9)
[](#cb38-10)$ # same as: awk '{gsub(/part|parrot/, "X")} 1'
[](#cb38-11)$ echo 'par part parrot parent' | awk '{gsub(/par(ro)?t/, "X")} 1'
[](#cb38-12)par X X parent
[](#cb38-13)$ # same as: awk '{gsub(/part|parrot|parent/, "X")} 1'
[](#cb38-14)$ echo 'par part parrot parent' | awk '{gsub(/par(en|ro)?t/, "X")} 1'
[](#cb38-15)par X X X
[](#cb38-16)
[](#cb38-17)$ # both '<' and '\<' are replaced with '\<'
[](#cb38-18)$ echo 'blah \< foo bar < blah baz <' | awk '{gsub(/\\?</, "\\<")} 1'
[](#cb38-19)blah \< foo bar \< blah baz \<
```

The `*` metacharacter quantifies a character or group to match `0` or more times. There is no upper bound, more details will be discussed later in the next section.

```
[](#cb39-1)$ # 'f' followed by zero or more of 'e' followed by 'd'
[](#cb39-2)$ echo 'fd fed fod fe:d feeeeder' | awk '{gsub(/fe*d/, "X")} 1'
[](#cb39-3)X X fod fe:d Xer
[](#cb39-4)
[](#cb39-5)$ # zero or more of '1' followed by '2'
[](#cb39-6)$ echo '3111111111125111142' | awk '{gsub(/1*2/, "-")} 1'
[](#cb39-7)3-511114-
```

The `+` metacharacter quantifies a character or group to match `1` or more times. Similar to `*` quantifier, there is no upper bound.

```
[](#cb40-1)$ # 'f' followed by one or more of 'e' followed by 'd'
[](#cb40-2)$ echo 'fd fed fod fe:d feeeeder' | awk '{gsub(/fe+d/, "X")} 1'
[](#cb40-3)fd X fod fe:d Xer
[](#cb40-4)
[](#cb40-5)$ # 'f' followed by at least one of 'e' or 'o' or ':' followed by 'd'
[](#cb40-6)$ echo 'fd fed fod fe:d feeeeder' | awk '{gsub(/f(e|o|:)+d/, "X")} 1'
[](#cb40-7)fd X X X Xer
[](#cb40-8)
[](#cb40-9)$ # one or more of '1' followed by optional '4' and then '2'
[](#cb40-10)$ echo '3111111111125111142' | awk '{gsub(/1+4?2/, "-")} 1'
[](#cb40-11)3-5-
```

You can specify a range of integer numbers, both bounded and unbounded, using `{}` metacharacters. There are four ways to use this quantifier as listed below:

| Pattern | Description |
| --- | --- |
| `{m,n}` | match `m` to `n` times |
| `{m,}` | match at least `m` times |
| `{,n}` | match up to `n` times (including `0` times) |
| `{n}` | match exactly `n` times |

```
[](#cb41-1)$ # note that inside {} space is not allowed
[](#cb41-2)$ echo 'ac abc abbc abbbc abbbbbbbbc' | awk '{gsub(/ab{1,4}c/, "X")} 1'
[](#cb41-3)ac X X X abbbbbbbbc
[](#cb41-4)
[](#cb41-5)$ echo 'ac abc abbc abbbc abbbbbbbbc' | awk '{gsub(/ab{3,}c/, "X")} 1'
[](#cb41-6)ac abc abbc X X
[](#cb41-7)
[](#cb41-8)$ echo 'ac abc abbc abbbc abbbbbbbbc' | awk '{gsub(/ab{,2}c/, "X")} 1'
[](#cb41-9)X X X abbbc abbbbbbbbc
[](#cb41-10)
[](#cb41-11)$ echo 'ac abc abbc abbbc abbbbbbbbc' | awk '{gsub(/ab{3}c/, "X")} 1'
[](#cb41-12)ac abc abbc X abbbbbbbbc
```

> ![info](media/file0.svg) The `{}` metacharacters have to be escaped to match them literally. Similar to `()` metacharacters, escaping `{` alone is enough.

Next up, how to construct conditional AND using dot metacharacter and quantifiers.

```
[](#cb42-1)$ # match 'Error' followed by zero or more characters followed by 'valid'
[](#cb42-2)$ echo 'Error: not a valid input' | awk '/Error.*valid/'
[](#cb42-3)Error: not a valid input
```

To allow matching in any order, you'll have to bring in alternation as well. But, for more than 3 patterns, the combinations become too many to write and maintain.

```
[](#cb43-1)$ # 'cat' followed by 'dog' or 'dog' followed by 'cat'
[](#cb43-2)$ echo 'two cats and a dog' | awk '{gsub(/cat.*dog|dog.*cat/, "pets")} 1'
[](#cb43-3)two pets
[](#cb43-4)$ echo 'two dogs and a cat' | awk '{gsub(/cat.*dog|dog.*cat/, "pets")} 1'
[](#cb43-5)two pets
```

## Longest match wins

You've already seen an example with alternation, where the longest matching portion was chosen if two alternatives started from same location. For example `spar|spared` will result in `spared` being chosen over `spar`. The same applies whenever there are two or more matching possibilities from same starting location. For example, `f.?o` will match `foo` instead of `fo` if the input string to match is `foot`.

```
[](#cb44-1)$ # longest match among 'foo' and 'fo' wins here
[](#cb44-2)$ echo 'foot' | awk '{sub(/f.?o/, "X")} 1'
[](#cb44-3)Xt
[](#cb44-4)$ # everything will match here
[](#cb44-5)$ echo 'car bat cod map scat dot abacus' | awk '{sub(/.*/, "X")} 1'
[](#cb44-6)X
[](#cb44-7)
[](#cb44-8)$ # longest match happens when (1|2|3)+ matches up to '1233' only
[](#cb44-9)$ # so that '12baz' can match as well
[](#cb44-10)$ echo 'foo123312baz' | awk '{sub(/o(1|2|3)+(12baz)?/, "X")} 1'
[](#cb44-11)foX
[](#cb44-12)$ # in other implementations like 'perl', that is not the case
[](#cb44-13)$ # quantifiers match as much as possible, but precedence is left to right
[](#cb44-14)$ echo 'foo123312baz' | perl -pe 's/o(1|2|3)+(12baz)?/X/'
[](#cb44-15)foXbaz
```

While determining the longest match, overall regular expression matching is also considered. That's how `Error.*valid` example worked. If `.*` had consumed everything after `Error`, there wouldn't be any more characters to try to match `valid`. So, among the varying quantity of characters to match for `.*`, the longest portion that satisfies the overall regular expression is chosen. Something like `a.*b` will match from first `a` in the input string to the last `b` in the string. In other implementations, like `perl`, this is achieved through a process called **backtracking**. Both approaches have their own advantages and disadvantages and have cases where the regexp can result in exponential time consumption.

```
[](#cb45-1)$ # from start of line to last 'm' in the line
[](#cb45-2)$ echo 'car bat cod map scat dot abacus' | awk '{sub(/.*m/, "-")} 1'
[](#cb45-3)-ap scat dot abacus
[](#cb45-4)
[](#cb45-5)$ # from first 'b' to last 't' in the line
[](#cb45-6)$ echo 'car bat cod map scat dot abacus' | awk '{sub(/b.*t/, "-")} 1'
[](#cb45-7)car - abacus
[](#cb45-8)
[](#cb45-9)$ # from first 'b' to last 'at' in the line
[](#cb45-10)$ echo 'car bat cod map scat dot abacus' | awk '{sub(/b.*at/, "-")} 1'
[](#cb45-11)car - dot abacus
[](#cb45-12)
[](#cb45-13)$ # here 'm*' will match 'm' zero times as that gives the longest match
[](#cb45-14)$ echo 'car bat cod map scat dot abacus' | awk '{sub(/a.*m*/, "-")} 1'
[](#cb45-15)c-
```

## Character classes

To create a custom placeholder for limited set of characters, enclose them inside `[]` metacharacters. It is similar to using single character alternations inside a grouping, but with added flexibility and features. Character classes have their own versions of metacharacters and provide special predefined sets for common use cases. Quantifiers are also applicable to character classes.

```
[](#cb46-1)$ # same as: awk '/cot|cut/' and awk '/c(o|u)t/'
[](#cb46-2)$ printf 'cute\ncat\ncot\ncoat\ncost\nscuttle\n' | awk '/c[ou]t/'
[](#cb46-3)cute
[](#cb46-4)cot
[](#cb46-5)scuttle
[](#cb46-6)
[](#cb46-7)$ # same as: awk '/.(a|e|o)+t/'
[](#cb46-8)$ printf 'meeting\ncute\nboat\nat\nfoot\n' | awk '/.[aeo]+t/'
[](#cb46-9)meeting
[](#cb46-10)boat
[](#cb46-11)foot
[](#cb46-12)
[](#cb46-13)$ # same as: awk '{gsub(/\<(s|o|t)(o|n)\>/, "X")} 1'
[](#cb46-14)$ echo 'no so in to do on' | awk '{gsub(/\<[sot][on]\>/, "X")} 1'
[](#cb46-15)no X in X do X
[](#cb46-16)
[](#cb46-17)$ # strings made up of letters 'o' and 'n', string length at least 2
[](#cb46-18)$ # /usr/share/dict/words contains dictionary words, one word per line
[](#cb46-19)$ awk '/^[on]{2,}$/' /usr/share/dict/words
[](#cb46-20)no
[](#cb46-21)non
[](#cb46-22)noon
[](#cb46-23)on
```

Character classes have their own metacharacters to help define the sets succinctly. Metacharacters outside of character classes like `^`, `$`, `()` etc either don't have special meaning or have completely different one inside the character classes.

First up, the `-` metacharacter that helps to define a range of characters instead of having to specify them all individually.

```
[](#cb47-1)$ # same as: awk '{gsub(/[0123456789]+/, "-")} 1'
[](#cb47-2)$ echo 'Sample123string42with777numbers' | awk '{gsub(/[0-9]+/, "-")} 1'
[](#cb47-3)Sample-string-with-numbers
[](#cb47-4)
[](#cb47-5)$ # whole words made up of lowercase alphabets and digits only
[](#cb47-6)$ echo 'coat Bin food tar12 best' | awk '{gsub(/\<[a-z0-9]+\>/, "X")} 1'
[](#cb47-7)X Bin X X X
[](#cb47-8)
[](#cb47-9)$ # whole words made up of lowercase alphabets, starting with 'p' to 'z'
[](#cb47-10)$ echo 'road i post grip read eat pit' | awk '{gsub(/\<[p-z][a-z]*\>/, "X")} 1'
[](#cb47-11)X i X grip X eat X
```

Character classes can also be used to construct numeric ranges. However, it is easy to miss corner cases and some ranges are complicated to design. See also [regular-expressions: Matching Numeric Ranges with a Regular Expression](https://www.regular-expressions.info/numericranges.html).

```
[](#cb48-1)$ # numbers between 10 to 29
[](#cb48-2)$ echo '23 154 12 26 34' | awk '{gsub(/\<[12][0-9]\>/, "X")} 1'
[](#cb48-3)X 154 X X 34
[](#cb48-4)
[](#cb48-5)$ # numbers >= 100 with optional leading zeros
[](#cb48-6)$ echo '0501 035 154 12 26 98234' | awk '{gsub(/\<0*[1-9][0-9]{2,}\>/, "X")} 1'
[](#cb48-7)X 035 X 12 26 X
```

Next metacharacter is `^` which has to specified as the first character of the character class. It negates the set of characters, so all characters other than those specified will be matched. Handle negative logic with care though, you might end up matching more than you wanted.

```
[](#cb49-1)$ # replace all non-digits
[](#cb49-2)$ echo 'Sample123string42with777numbers' | awk '{gsub(/[^0-9]+/, "-")} 1'
[](#cb49-3)-123-42-777-
[](#cb49-4)
[](#cb49-5)$ # delete last two columns based on a delimiter
[](#cb49-6)$ echo 'foo:123:bar:baz' | awk '{sub(/(:[^:]+){2}$/, "")} 1'
[](#cb49-7)foo:123
[](#cb49-8)
[](#cb49-9)$ # sequence of characters surrounded by unique character
[](#cb49-10)$ echo 'I like "mango" and "guava"' | awk '{gsub(/"[^"]+"/, "X")} 1'
[](#cb49-11)I like X and X
[](#cb49-12)
[](#cb49-13)$ # sometimes it is simpler to positively define a set than negation
[](#cb49-14)$ # same as: awk '/^[^aeiou]*$/'
[](#cb49-15)$ printf 'tryst\nfun\nglyph\npity\nwhy\n' | awk '!/[aeiou]/'
[](#cb49-16)tryst
[](#cb49-17)glyph
[](#cb49-18)why
```

Some commonly used character sets have predefined escape sequences:

*   `\w` matches all **word** characters `[a-zA-Z0-9_]` (recall the description for word boundaries)
*   `\W` matches all non-word characters (recall duality seen earlier, like `\y` and `\B`)
*   `\s` matches all **whitespace** characters: tab, newline, vertical tab, form feed, carriage return and space
*   `\S` matches all non-whitespace characters

```
[](#cb50-1)$ # match all non-word characters
[](#cb50-2)$ echo 'load;err_msg--\/ant,r2..not' | awk '{gsub(/\W+/, "-")} 1'
[](#cb50-3)load-err_msg-ant-r2-not
[](#cb50-4)
[](#cb50-5)$ # replace all sequences of whitespaces with single space
[](#cb50-6)$ printf 'hi  \v\f  there.\thave   \ra nice\t\tday\n' | awk '{gsub(/\s+/, " ")} 1'
[](#cb50-7)hi there. have a nice day
```

These escape sequences *cannot* be used inside character classes.

```
[](#cb51-1)$ # \w would simply match w inside character classes
[](#cb51-2)$ echo 'w=y\x+9*3' | awk '{gsub(/[\w=]/, "")} 1'
[](#cb51-3)y\x+9*3
```

> ![warning](media/file1.svg) `awk` doesn't support `\d` and `\D`, commonly featured in other implementations as a shortcut for all the digits and non-digits.

A **named character set** is defined by a name enclosed between `[:` and `:]` and has to be used within a character class `[]`, along with any other characters as needed.

| Named set | Description |
| --- | --- |
| `[:digit:]` | `[0-9]` |
| `[:lower:]` | `[a-z]` |
| `[:upper:]` | `[A-Z]` |
| `[:alpha:]` | `[a-zA-Z]` |
| `[:alnum:]` | `[0-9a-zA-Z]` |
| `[:xdigit:]` | `[0-9a-fA-F]` |
| `[:cntrl:]` | control characters - first 32 ASCII characters and 127th (DEL) |
| `[:punct:]` | all the punctuation characters |
| `[:graph:]` | `[:alnum:]` and `[:punct:]` |
| `[:print:]` | `[:alnum:]`, `[:punct:]` and space |
| `[:blank:]` | space and tab characters |
| `[:space:]` | whitespace characters, same as `\s` |

```
[](#cb52-1)$ s='err_msg xerox ant m_2 P2 load1 eel'
[](#cb52-2)$ echo "$s" | awk '{gsub(/\<[[:lower:]]+\>/, "X")} 1'
[](#cb52-3)err_msg X X m_2 P2 load1 X
[](#cb52-4)
[](#cb52-5)$ echo "$s" | awk '{gsub(/\<[[:lower:]_]+\>/, "X")} 1'
[](#cb52-6)X X X m_2 P2 load1 X
[](#cb52-7)
[](#cb52-8)$ echo "$s" | awk '{gsub(/\<[[:alnum:]]+\>/, "X")} 1'
[](#cb52-9)err_msg X X m_2 X X X
[](#cb52-10)
[](#cb52-11)$ echo ',pie tie#ink-eat_42' | awk '{gsub(/[^[:punct:]]+/, "")} 1'
[](#cb52-12),#-_
```

Specific placement is needed to match character class metacharacters literally. Or, they can be escaped by prefixing `\` to avoid having to remember the different rules. As `\` is special inside character class, use `\\` to represent it literally.

```
[](#cb53-1)$ # - should be first or last character within []
[](#cb53-2)$ echo 'ab-cd gh-c 12-423' | awk '{gsub(/[a-z-]{2,}/, "X")} 1'
[](#cb53-3)X X 12-423
[](#cb53-4)$ # or escaped with \
[](#cb53-5)$ echo 'ab-cd gh-c 12-423' | awk '{gsub(/[a-z\-0-9]{2,}/, "X")} 1'
[](#cb53-6)X X X
[](#cb53-7)
[](#cb53-8)$ # ] should be first character within []
[](#cb53-9)$ printf 'int a[5]\nfoo\n1+1=2\n' | awk '/[=]]/'
[](#cb53-10)$ printf 'int a[5]\nfoo\n1+1=2\n' | awk '/[]=]/'
[](#cb53-11)int a[5]
[](#cb53-12)1+1=2
[](#cb53-13)
[](#cb53-14)$ # to match [ use [ anywhere in the character set
[](#cb53-15)$ # [][] will match both [ and ]
[](#cb53-16)$ printf 'int a[5]\nfoo\n1+1=2\n' | awk '/[][]/'
[](#cb53-17)int a[5]
[](#cb53-18)
[](#cb53-19)$ # ^ should be other than first character within []
[](#cb53-20)$ echo 'f*(a^b) - 3*(a+b)/(a-b)' | awk '{gsub(/a[+^]b/, "c")} 1'
[](#cb53-21)f*(c) - 3*(c)/(a-b)
```

> ![warning](media/file1.svg) Combinations like `[.` or `[:` cannot be used together to mean two individual characters, as they have special meaning within `[]`. See [gawk manual: Using Bracket Expressions](https://www.gnu.org/software/gawk/manual/gawk.html#Bracket-Expressions) for more details.

```
[](#cb54-1)$ echo 'int a[5]' | awk '/[x[.y]/'
[](#cb54-2)awk: cmd. line:1: error: Unmatched [, [^, [:, [., or [=: /[x[.y]/
[](#cb54-3)$ echo 'int a[5]' | awk '/[x[y.]/'
[](#cb54-4)int a[5]
```

## Escape sequences

Certain ASCII characters like tab `\t`, carriage return `\r`, newline `\n`, etc have escape sequences to represent them. Additionally, any character can be represented using their ASCII value in octal `\NNN` or hexadecimal `\xNN` formats. Unlike character set escape sequences like `\w`, these can be used inside character classes.

```
[](#cb55-1)$ # using \t to represent tab character
[](#cb55-2)$ printf 'foo\tbar\tbaz\n' | awk '{gsub(/\t/, " ")} 1'
[](#cb55-3)foo bar baz
[](#cb55-4)
[](#cb55-5)$ # these escape sequence work inside character class too
[](#cb55-6)$ printf 'a\t\r\fb\vc\n' | awk '{gsub(/[\t\v\f\r]+/, ":")} 1'
[](#cb55-7)a:b:c
[](#cb55-8)
[](#cb55-9)$ # representing single quotes
[](#cb55-10)$ # use \047 for octal format
[](#cb55-11)$ echo "universe: '42'" | awk '{gsub(/\x27/, "")} 1'
[](#cb55-12)universe: 42
```

> ![info](media/file0.svg) If a metacharacter is specified by ASCII value, it will still act as the metacharacter. Undefined sequences will result in a warning and treated as the character it escapes.

```
[](#cb56-1)$ # \x5e is ^ character, acts as string anchor here
[](#cb56-2)$ printf 'cute\ncot\ncat\ncoat\n' | awk '/\x5eco/'
[](#cb56-3)cot
[](#cb56-4)coat
[](#cb56-5)
[](#cb56-6)$ # & metacharacter in replacement will be discussed in a later section
[](#cb56-7)$ # it represents entire matched portion
[](#cb56-8)$ echo 'hello world' | awk '{sub(/.*/, "[&]")} 1'
[](#cb56-9)[hello world]
[](#cb56-10)$ # \x26 is & character
[](#cb56-11)$ echo 'hello world' | awk '{sub(/.*/, "[\x26]")} 1'
[](#cb56-12)[hello world]
[](#cb56-13)
[](#cb56-14)$ echo 'read' | awk '{sub(/a/, "\.")} 1'
[](#cb56-15)awk: cmd. line:1: warning: escape sequence `\.' treated as plain `.'
[](#cb56-16)re.d
```

> ![info](media/file0.svg) See [gawk manual: Escape Sequences](https://www.gnu.org/software/gawk/manual/gawk.html#Escape-Sequences) for full list and other details.

## Replace specific occurrence

The third substitution function is `gensub` which can be used instead of both `sub` and `gsub` functions. Syntax wise, `gensub` needs minimum three arguments. The third argument is used to indicate whether you want to replace all occurrences with `"g"` or specific occurrence by giving a number. Another difference is that `gensub` returns a string value (irrespective of substitution succeeding) instead of modifying the input.

```
[](#cb57-1)$ # same as: sed 's/:/-/2'
[](#cb57-2)$ # replace only second occurrence of ':' with '-'
[](#cb57-3)$ # note that output of gensub is passed to print here
[](#cb57-4)$ echo 'foo:123:bar:baz' | awk '{print gensub(/:/, "-", 2)}'
[](#cb57-5)foo:123-bar:baz
[](#cb57-6)
[](#cb57-7)$ # same as: sed -E 's/[^:]+/X/3'
[](#cb57-8)$ # replace only third field with 'X'
[](#cb57-9)$ echo 'foo:123:bar:baz' | awk '{print gensub(/[^:]+/, "X", 3)}'
[](#cb57-10)foo:123:X:baz
```

The fourth argument for `gensub` function allows you to specify the input string or variable on which the substitution has to be performed. Default is `$0`, as seen in previous examples.

```
[](#cb58-1)$ # replace vowels with 'X' only for fourth field
[](#cb58-2)$ # same as: awk '{gsub(/[aeiou]/, "X", $4)} 1'
[](#cb58-3)$ echo '1 good 2 apples' | awk '{$4 = gensub(/[aeiou]/, "X", "g", $4)} 1'
[](#cb58-4)1 good 2 XpplXs
```

## Backreferences

The grouping metacharacters `()` are also known as **capture groups**. They are like variables, the string captured by `()` can be referred later using backreference `\N` where `N` is the capture group you want. Leftmost `(` in the regular expression is `\1`, next one is `\2` and so on up to `\9`. As a special case, `\0` or `&` metacharacter represents entire matched string. As `\` is special inside double quotes, you'll have to use `"\\1"` to represent `\1`.

> ![info](media/file0.svg) Backreferences of the form `\N` can only be used with `gensub` function. `&` can be used with `sub`, `gsub` and `gensub` functions.

```
[](#cb59-1)$ # reduce \\ to single \ and delete if it is a single \
[](#cb59-2)$ s='\[\] and \\w and \[a-zA-Z0-9\_\]'
[](#cb59-3)$ echo "$s" | awk '{print gensub(/(\\?)\\/, "\\1", "g")}'
[](#cb59-4)[] and \w and [a-zA-Z0-9_]
[](#cb59-5)
[](#cb59-6)$ # duplicate first column value as final column
[](#cb59-7)$ echo 'one,2,3.14,42' | awk '{print gensub(/^([^,]+).*/, "&,\\1", 1)}'
[](#cb59-8)one,2,3.14,42,one
[](#cb59-9)
[](#cb59-10)$ # add something at start and end of string
[](#cb59-11)$ # as only '&' is used, gensub isn't needed here
[](#cb59-12)$ echo 'hello world' | awk '{sub(/.*/, "Hi. &. Have a nice day")} 1'
[](#cb59-13)Hi. hello world. Have a nice day
[](#cb59-14)
[](#cb59-15)$ # here {N} refers to last but Nth occurrence
[](#cb59-16)$ s='456:foo:123:bar:789:baz'
[](#cb59-17)$ echo "$s" | awk '{print gensub(/(.*):((.*:){2})/, "\\1[]\\2", 1)}'
[](#cb59-18)456:foo:123[]bar:789:baz
```

> ![warning](media/file1.svg) See [unix.stackexchange: Why doesn't this sed command replace the 3rd-to-last "and"?](https://unix.stackexchange.com/q/579889/109046) for a bug related to use of word boundaries in the `((){N})` generic case.

> ![warning](media/file1.svg) Unlike other regular expression implementations, like `grep` or `sed` or `perl`, backreferences cannot be used in search section in `awk`. See also [unix.stackexchange: backreference in awk](https://unix.stackexchange.com/q/361427/109046).

If quantifier is applied on a pattern grouped inside `()` metacharacters, you'll need an outer `()` group to capture the matching portion. Some regular expression engines provide non-capturing group to handle such cases. In `awk`, you'll have to work around the extra capture group.

```
[](#cb60-1)$ # note the numbers used in replacement section
[](#cb60-2)$ s='one,2,3.14,42'
[](#cb60-3)$ echo "$s" | awk '{$0=gensub(/^(([^,]+,){2})([^,]+)/, "[\\1](\\3)", 1)} 1'
[](#cb60-4)[one,2,](3.14),42
```

Here's an example where alternation order matters when matching portions have same length. Aim is to delete all whole words unless it starts with `g` or `p` and contains `y`.

```
[](#cb61-1)$ s='tryst,fun,glyph,pity,why,group'
[](#cb61-2)
[](#cb61-3)$ # all words get deleted because \w+ gets priority here
[](#cb61-4)$ echo "$s" | awk '{print gensub(/\<\w+\>|(\<[gp]\w*y\w*\>)/, "\\1", "g")}'
[](#cb61-5),,,,,
[](#cb61-6)
[](#cb61-7)$ # capture group gets priority here, thus words matching the group are retained
[](#cb61-8)$ echo "$s" | awk '{print gensub(/(\<[gp]\w*y\w*\>)|\<\w+\>/, "\\1", "g")}'
[](#cb61-9),,glyph,pity,,
```

As `\` and `&` are special characters inside double quotes in replacement section, use `\\` and `\\&` respectively for literal representation.

```
[](#cb62-1)$ echo 'foo and bar' | awk '{sub(/and/, "[&]")} 1'
[](#cb62-2)foo [and] bar
[](#cb62-3)$ echo 'foo and bar' | awk '{sub(/and/, "[\\&]")} 1'
[](#cb62-4)foo [&] bar
[](#cb62-5)
[](#cb62-6)$ echo 'foo and bar' | awk '{sub(/and/, "\\")} 1'
[](#cb62-7)foo \ bar
```

## Case insensitive matching

Unlike `sed` or `perl`, regular expressions in `awk` do not directly support the use of flags to change certain behaviors. For example, there is no flag to force the regexp to ignore case while matching.

The `IGNORECASE` special variable controls case sensitivity, which is `0` by default. By changing it to some other value (which would mean `true` in conditional expression), you can match case insensitively. The `-v` command line option allows you to assign a variable before input is read. The `BEGIN` block is also often used to change such settings.

```
[](#cb63-1)$ printf 'Cat\ncOnCaT\nscatter\ncot\n' | awk -v IGNORECASE=1 '/cat/'
[](#cb63-2)Cat
[](#cb63-3)cOnCaT
[](#cb63-4)scatter
[](#cb63-5)
[](#cb63-6)$ # for small enough string, can also use character class
[](#cb63-7)$ printf 'Cat\ncOnCaT\nscatter\ncot\n' | awk '{gsub(/[cC][aA][tT]/, "dog")} 1'
[](#cb63-8)dog
[](#cb63-9)cOndog
[](#cb63-10)sdogter
[](#cb63-11)cot
```

Another way is to use built-in string function `tolower` to change the input to lowercase first.

```
[](#cb64-1)$ printf 'Cat\ncOnCaT\nscatter\ncot\n' | awk 'tolower($0) ~ /cat/'
[](#cb64-2)Cat
[](#cb64-3)cOnCaT
[](#cb64-4)scatter
```

## Dynamic regexp

As seen earlier, you can use a string literal instead of regexp to specify the pattern to be matched. Which implies that you can use any expression or a variable as well. This is helpful if you need to compute the regexp based on some conditions or if you are getting the pattern externally, such as user input.

The `-v` command line option comes in handy to get user input, say from a `bash` variable.

```
[](#cb65-1)$ r='cat.*dog|dog.*cat'
[](#cb65-2)$ echo 'two cats and a dog' | awk -v ip="$r" '{gsub(ip, "pets")} 1'
[](#cb65-3)two pets
[](#cb65-4)
[](#cb65-5)$ awk -v s='ow' '$0 ~ s' table.txt
[](#cb65-6)brown bread mat hair 42
[](#cb65-7)yellow banana window shoes 3.14
[](#cb65-8)
[](#cb65-9)$ # you'll have to make sure to use \\ instead of \
[](#cb65-10)$ r='\\<[12][0-9]\\>'
[](#cb65-11)$ echo '23 154 12 26 34' | awk -v ip="$r" '{gsub(ip, "X")} 1'
[](#cb65-12)X 154 X X 34
```

> ![info](media/file0.svg) See [Using shell variables](#ch008.xhtml_using-shell-variables) chapter for a way to avoid having to use `\\` instead of `\`.

Sometimes, you need to get user input and then treat it literally instead of regexp pattern. In such cases, you'll need to first escape the metacharacters before using in substitution functions. Below example shows how to do it for search section. For replace section, you only have to escape the `\` and `&` characters.

```
[](#cb66-1)$ awk -v s='(a.b)^{c}|d' 'BEGIN{gsub(/[{[(^$*?+.|\\]/, "\\\\&", s); print s}'
[](#cb66-2)\(a\.b)\^\{c}\|d
[](#cb66-3)
[](#cb66-4)$ echo 'f*(a^b) - 3*(a^b)' |
[](#cb66-5)     awk -v s='(a^b)' '{gsub(/[{[(^$*?+.|\\]/, "\\\\&", s); gsub(s, "c")} 1'
[](#cb66-6)f*c - 3*c
[](#cb66-7)
[](#cb66-8)$ # match given input string literally, but only at the end of string
[](#cb66-9)$ echo 'f*(a^b) - 3*(a^b)' |
[](#cb66-10)     awk -v s='(a^b)' '{gsub(/[{[(^$*?+.|\\]/, "\\\\&", s); gsub(s "$", "c")} 1'
[](#cb66-11)f*(a^b) - 3*c
```

> ![info](media/file0.svg) If you need to match instead of substitution, you can use the `index` function. See [index](#ch010.xhtml_index) section for details.

## Summary

Regular expressions is a feature that you'll encounter in multiple command line programs and programming languages. It is a versatile tool for text processing. Although the features in `awk` are less compared to those found in programming languages, they are sufficient for most of the tasks you'll need for command line usage. It takes a lot of time to get used to syntax and features of regular expressions, so I'll encourage you to practice a lot and maintain notes. It'd also help to consider it as a mini-programming language in itself for its flexibility and complexity.

## Exercises

**a)** For the given input, print all lines that start with `den` or end with `ly`.

```
[](#cb67-1)$ lines='lovely\n1 dentist\n2 lonely\neden\nfly away\ndent\n'
[](#cb67-2)$ printf '%b' "$lines" | awk ##### add your solution here
[](#cb67-3)lovely
[](#cb67-4)2 lonely
[](#cb67-5)dent
```

**b)** Replace all occurrences of `42` with `[42]` unless it is at the edge of a word. Note that **word** in these exercises have same meaning as defined in regular expressions.

```
[](#cb68-1)$ echo 'hi42bye nice421423 bad42 cool_42a 42c' | awk ##### add your solution here
[](#cb68-2)hi[42]bye nice[42]1[42]3 bad42 cool_[42]a 42c
```

**c)** Add `[]` around words starting with `s` and containing `e` and `t` in any order.

```
[](#cb69-1)$ words='sequoia subtle exhibit asset sets tests site'
[](#cb69-2)$ echo "$words" | awk ##### add your solution here
[](#cb69-3)sequoia [subtle] exhibit asset [sets] tests [site]
```

**d)** Replace the space character that occurs after a word ending with `a` or `r` with a newline character.

```
[](#cb70-1)$ echo 'area not a _a2_ roar took 22' | awk ##### add your solution here
[](#cb70-2)area
[](#cb70-3)not a
[](#cb70-4)_a2_ roar
[](#cb70-5)took 22
```

**e)** Replace all occurrences of `[4]|*` with `2` for the given input.

```
[](#cb71-1)$ echo '2.3/[4]|*6 foo 5.3-[4]|*9' | awk ##### add your solution here
[](#cb71-2)2.3/26 foo 5.3-29
```

**f)** `awk '/\<[a-z](on|no)[a-z]\>/'` is same as `awk '/\<[a-z][on]{2}[a-z]\>/'`. True or False? Sample input shown below might help to understand the differences, if any.

```
[](#cb72-1)$ printf 'known\nmood\nknow\npony\ninns\n'
[](#cb72-2)known
[](#cb72-3)mood
[](#cb72-4)know
[](#cb72-5)pony
[](#cb72-6)inns
```

**g)** Print all lines that start with `hand` and ends with `s` or `y` or `le` or no further character. For example, `handed` shouldn't be printed even though it starts with `hand`.

```
[](#cb73-1)$ lines='handed\nhand\nhandy\nunhand\nhands\nhandle\n'
[](#cb73-2)$ printf '%b' "$lines" | awk ##### add your solution here
[](#cb73-3)hand
[](#cb73-4)handy
[](#cb73-5)hands
[](#cb73-6)handle
```

**h)** Replace `42//5` or `42/5` with `8` for the given input.

```
[](#cb74-1)$ echo 'a+42//5-c pressure*3+42/5-14256' | awk ##### add your solution here
[](#cb74-2)a+8-c pressure*3+8-14256
```

**i)** For the given quantifiers, what would be the equivalent form using `{m,n}` representation?

*   `?` is same as
*   `*` is same as
*   `+` is same as

**j)** True or False? `(a*|b*)` is same as `(a|b)*`

**k)** For the given input, construct two different regexps to get the outputs as shown below.

```
[](#cb75-1)$ # delete from '(' till next ')'
[](#cb75-2)$ echo 'a/b(division) + c%d() - (a#(b)2(' | awk ##### add your solution here
[](#cb75-3)a/b + c%d - 2(
[](#cb75-4)
[](#cb75-5)$ # delete from '(' till next ')' but not if there is '(' in between
[](#cb75-6)$ echo 'a/b(division) + c%d() - (a#(b)2(' | awk ##### add your solution here
[](#cb75-7)a/b + c%d - (a#2(
```

**l)** For the input file `anchors.txt`, convert **markdown** anchors to corresponding **hyperlinks**.

```
[](#cb76-1)$ cat anchors.txt
[](#cb76-2)# <a name="regular-expressions"></a>Regular Expressions
[](#cb76-3)## <a name="subexpression-calls"></a>Subexpression calls
[](#cb76-4)
[](#cb76-5)$ awk ##### add your solution here
[](#cb76-6)[Regular Expressions](#regular-expressions)
[](#cb76-7)[Subexpression calls](#subexpression-calls)
```

**m)** Display all lines that satisfies **both** of these conditions:

*   `professor` matched irrespective of case
*   `quip` or `this` matched case sensitively

Input is a file downloaded from internet as shown below.

```
[](#cb77-1)$ wget https://www.gutenberg.org/files/345/345.txt -O dracula.txt
[](#cb77-2)
[](#cb77-3)$ awk ##### add your solution here
[](#cb77-4)equipment of a professor of the healing craft. When we were shown in,
[](#cb77-5)should be. I could see that the Professor had carried out in this room,
[](#cb77-6)"Not up to this moment, Professor," she said impulsively, "but up to
[](#cb77-7)and sprang at us. But by this time the Professor had gained his feet,
[](#cb77-8)this time the Professor had to ask her questions, and to ask them pretty
```

**n)** Given sample strings have fields separated by `,` and field values cannot be empty. Replace the third field with `42`.

```
[](#cb78-1)$ echo 'lion,ant,road,neon' | awk ##### add your solution here
[](#cb78-2)lion,ant,42,neon
[](#cb78-3)
[](#cb78-4)$ echo '_;3%,.,=-=,:' | awk ##### add your solution here
[](#cb78-5)_;3%,.,42,:
```

**o)** For the given strings, replace last but third `so` with `X`. Only print the lines which are changed by the substitution.

```
[](#cb79-1)$ printf 'so and so also sow and soup' | awk ##### add your solution here
[](#cb79-2)so and X also sow and soup
[](#cb79-3)
[](#cb79-4)$ printf 'sososososososo\nso and so\n' | awk ##### add your solution here
[](#cb79-5)sososoXsososo
```

**p)** Surround all whole words with `()`. Additionally, if the whole word is `imp` or `ant`, delete them. Can you do it with single substitution?

```
[](#cb80-1)$ words='tiger imp goat eagle ant important'
[](#cb80-2)$ echo "$words" | awk ##### add your solution here
[](#cb80-3)(tiger) () (goat) (eagle) () (important)
```

# Field separators

Now that you are familiar with basic `awk` syntax and regular expressions, this chapter will dive deep into field processing. You'll learn how to set input and output field separators, how to use regexps for defining fields and how to work with fixed length fields.

## Default field separation

As seen earlier, `awk` automatically splits input into fields which are accessible using `$N` where `N` is the field number you need. You can also pass an expression instead of numeric literal to specify the field required.

```
[](#cb81-1)$ cat table.txt
[](#cb81-2)brown bread mat hair 42
[](#cb81-3)blue cake mug shirt -7
[](#cb81-4)yellow banana window shoes 3.14
[](#cb81-5)
[](#cb81-6)$ # print fourth field if first field starts with 'b'
[](#cb81-7)$ awk '$1 ~ /^b/{print $4}' table.txt
[](#cb81-8)hair
[](#cb81-9)shirt
[](#cb81-10)
[](#cb81-11)$ # print the field as specified by value stored in 'f' variable
[](#cb81-12)$ awk -v f=3 '{print $f}' table.txt
[](#cb81-13)mat
[](#cb81-14)mug
[](#cb81-15)window
```

The `NF` special variable will give you the number of fields for each input line. This is useful when you don't know how many fields are present in the input and you need to specify field number from the end.

```
[](#cb82-1)$ # print the last field of each input line
[](#cb82-2)$ awk '{print $NF}' table.txt
[](#cb82-3)42
[](#cb82-4)-7
[](#cb82-5)3.14
[](#cb82-6)
[](#cb82-7)$ # print the last but one field
[](#cb82-8)$ awk '{print $(NF-1)}' table.txt
[](#cb82-9)hair
[](#cb82-10)shirt
[](#cb82-11)shoes
[](#cb82-12)
[](#cb82-13)$ # don't forget the parentheses!
[](#cb82-14)$ awk '{print $NF-1}' table.txt
[](#cb82-15)41
[](#cb82-16)-8
[](#cb82-17)2.14
```

By default, `awk` does more than split the input on spaces. It splits based on one or more sequence of **space** or **tab** or **newline** characters. In addition, any of these three characters at the start or end of input gets trimmed and won't be part of field contents. Input containing newline character will be covered in [Record separators](#ch006.xhtml_record-separators) chapter.

```
[](#cb83-1)$ echo '   a   b   c   ' | awk '{print NF}'
[](#cb83-2)3
[](#cb83-3)$ # note that leading spaces isn't part of field content
[](#cb83-4)$ echo '   a   b   c   ' | awk '{print $1}'
[](#cb83-5)a
[](#cb83-6)$ # note that trailing spaces isn't part of field content
[](#cb83-7)$ echo '   a   b   c   ' | awk '{print $NF "."}'
[](#cb83-8)c.
[](#cb83-9)
[](#cb83-10)$ # here's another example with tab characters thrown in
[](#cb83-11)$ printf '     one \t two\t\t\tthree  ' | awk '{print NF}'
[](#cb83-12)3
[](#cb83-13)$ printf '     one \t two\t\t\tthree  ' | awk '{print $2 "."}'
[](#cb83-14)two.
```

> ![warning](media/file1.svg) When passing an expression for field number, floating-point result is acceptable too. The fractional portion is ignored. However, as precision is limited, it could result in rounding instead of truncation.

```
[](#cb84-1)$ awk 'BEGIN{printf "%.16f\n", 2.999999999999999}'
[](#cb84-2)2.9999999999999991
[](#cb84-3)$ awk 'BEGIN{printf "%.16f\n", 2.9999999999999999}'
[](#cb84-4)3.0000000000000000
[](#cb84-5)
[](#cb84-6)$ # same as: awk '{print $2}' table.txt
[](#cb84-7)$ awk '{print $2.999999999999999}' table.txt
[](#cb84-8)bread
[](#cb84-9)cake
[](#cb84-10)banana
[](#cb84-11)$ # same as: awk '{print $3}' table.txt
[](#cb84-12)$ awk '{print $2.9999999999999999}' table.txt
[](#cb84-13)mat
[](#cb84-14)mug
[](#cb84-15)window
```

## Input field separator

The most common way to change the default field separator is to use the `-F` command line option. The value passed to the option will be treated as a string literal and then converted to a regexp. For now, here's some examples without any special regexp characters.

```
[](#cb85-1)$ # use ':' as input field separator
[](#cb85-2)$ echo 'goal:amazing:whistle:kwality' | awk -F: '{print $1}'
[](#cb85-3)goal
[](#cb85-4)$ echo 'goal:amazing:whistle:kwality' | awk -F: '{print $NF}'
[](#cb85-5)kwality
[](#cb85-6)
[](#cb85-7)$ # use quotes to avoid clashes with shell special characters
[](#cb85-8)$ echo 'one;two;three;four' | awk -F';' '{print $3}'
[](#cb85-9)three
[](#cb85-10)
[](#cb85-11)$ # first and last fields will have empty string as their values
[](#cb85-12)$ echo '=a=b=c=' | awk -F= '{print $1 "[" $NF "]"}'
[](#cb85-13)[]
```

You can also directly set the special `FS` variable to change the input field separator. This can be done from the command line using `-v` option or within the code blocks.

```
[](#cb86-1)$ echo 'goal:amazing:whistle:kwality' | awk -v FS=: '{print $2}'
[](#cb86-2)amazing
[](#cb86-3)
[](#cb86-4)$ # field separator can be multiple characters too
[](#cb86-5)$ echo '1e4SPT2k6SPT3a5SPT4z0' | awk 'BEGIN{FS="SPT"} {print $3}'
[](#cb86-6)3a5
```

If you wish to split the input as individual characters, use an empty string as the field separator.

```
[](#cb87-1)$ # note that the space between -F and '' is mandatory
[](#cb87-2)$ echo 'apple' | awk -F '' '{print $1}'
[](#cb87-3)a
[](#cb87-4)$ echo 'apple' | awk -v FS= '{print $NF}'
[](#cb87-5)e
[](#cb87-6)
[](#cb87-7)$ # depending upon the locale, you can work with multibyte characters too
[](#cb87-8)$ echo 'αλεπού' | awk -v FS= '{print $3}'
[](#cb87-9)ε
```

Here's some examples with regexp based field separator. The value passed to `-F` or `FS` is treated as a string and then converted to regexp. So, you'll need `\\` instead of `\` to mean a backslash character. The good news is that for single characters that are also regexp metacharacters, they'll be treated literally and you do not need to escape them.

```
[](#cb88-1)$ echo 'Sample123string42with777numbers' | awk -F'[0-9]+' '{print $2}'
[](#cb88-2)string
[](#cb88-3)$ echo 'Sample123string42with777numbers' | awk -F'[a-zA-Z]+' '{print $2}'
[](#cb88-4)123
[](#cb88-5)
[](#cb88-6)$ # note the use of \\W to indicate \W
[](#cb88-7)$ echo 'load;err_msg--\ant,r2..not' | awk -F'\\W+' '{print $3}'
[](#cb88-8)ant
[](#cb88-9)
[](#cb88-10)$ # same as: awk -F'\\.' '{print $2}'
[](#cb88-11)$ echo 'hi.bye.hello' | awk -F. '{print $2}'
[](#cb88-12)bye
[](#cb88-13)
[](#cb88-14)$ # count number of vowels for each input line
[](#cb88-15)$ printf 'cool\nnice car\n' | awk -F'[aeiou]' '{print NF-1}'
[](#cb88-16)2
[](#cb88-17)3
```

> ![warning](media/file1.svg) The default value of `FS` is single space character. So, if you set input field separator to single space, then it will be the same as if you are using the default split discussed in previous section. If you want to override this behavior, you can use space inside a character class.

```
[](#cb89-1)$ # same as: awk '{print NF}'
[](#cb89-2)$ echo '   a   b   c   ' | awk -F' ' '{print NF}'
[](#cb89-3)3
[](#cb89-4)$ # there are 12 space characters, thus 13 fields
[](#cb89-5)$ echo '   a   b   c   ' | awk -F'[ ]' '{print NF}'
[](#cb89-6)13
```

> ![warning](media/file1.svg) If `IGNORECASE` is set, it will affect field separation as well. Except when field separator is a single character, which can be worked around by using a character class.

```
[](#cb90-1)$ echo 'RECONSTRUCTED' | awk -F'[aeiou]+' -v IGNORECASE=1 '{print $1}'
[](#cb90-2)R
[](#cb90-3)
[](#cb90-4)$ # when FS is a single character
[](#cb90-5)$ echo 'RECONSTRUCTED' | awk -F'e' -v IGNORECASE=1 '{print $1}'
[](#cb90-6)RECONSTRUCTED
[](#cb90-7)$ echo 'RECONSTRUCTED' | awk -F'[e]' -v IGNORECASE=1 '{print $1}'
[](#cb90-8)R
```

## Output field separator

The `OFS` special variable controls the output field separator. `OFS` is used as the string between multiple arguments passed to `print` function. It is also used whenever `$0` has to be reconstructed as a result of changing field contents. The default value for `OFS` is a single space character, just like for `FS`. There is no command line option though, you'll have to change `OFS` directly.

```
[](#cb91-1)$ # printing first and third field, OFS is used to join these values
[](#cb91-2)$ # note the use of , to separate print arguments
[](#cb91-3)$ awk '{print $1, $3}' table.txt
[](#cb91-4)brown mat
[](#cb91-5)blue mug
[](#cb91-6)yellow window
[](#cb91-7)
[](#cb91-8)$ # same FS and OFS
[](#cb91-9)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=: '{print $2, $NF}'
[](#cb91-10)amazing:kwality
[](#cb91-11)$ echo 'goal:amazing:whistle:kwality' | awk 'BEGIN{FS=OFS=":"} {print $2, $NF}'
[](#cb91-12)amazing:kwality
[](#cb91-13)
[](#cb91-14)$ # different values for FS and OFS
[](#cb91-15)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=- '{print $2, $NF}'
[](#cb91-16)amazing-kwality
```

Here's some examples for changing field contents and then printing `$0`.

```
[](#cb92-1)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=: '{$2 = 42} 1'
[](#cb92-2)goal:42:whistle:kwality
[](#cb92-3)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=, '{$2 = 42} 1'
[](#cb92-4)goal,42,whistle,kwality
[](#cb92-5)
[](#cb92-6)$ # recall that spaces at start/end gets trimmed for default FS
[](#cb92-7)$ echo '   a   b   c   ' | awk '{$NF = "last"} 1'
[](#cb92-8)a b last
```

Sometimes you want to print contents of `$0` with the new `OFS` value but field contents aren't being changed. In such cases, you can assign a field value to itself to force reconstruction of `$0`.

```
[](#cb93-1)$ # no change because there was no trigger to rebuild $0
[](#cb93-2)$ echo 'Sample123string42with777numbers' | awk -F'[0-9]+' -v OFS=, '1'
[](#cb93-3)Sample123string42with777numbers
[](#cb93-4)
[](#cb93-5)$ # assign a field to itself in such cases
[](#cb93-6)$ echo 'Sample123string42with777numbers' | awk -F'[0-9]+' -v OFS=, '{$1=$1} 1'
[](#cb93-7)Sample,string,with,numbers
```

## Manipulating NF

Changing `NF` value will rebuild `$0` as well.

```
[](#cb94-1)$ # reducing fields
[](#cb94-2)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=, '{NF=2} 1'
[](#cb94-3)goal,amazing
[](#cb94-4)
[](#cb94-5)$ # increasing fields
[](#cb94-6)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=: '{$(NF+1)="sea"} 1'
[](#cb94-7)goal:amazing:whistle:kwality:sea
[](#cb94-8)
[](#cb94-9)$ # empty fields will be created as needed
[](#cb94-10)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=: '{$8="go"} 1'
[](#cb94-11)goal:amazing:whistle:kwality::::go
```

> ![warning](media/file1.svg) Assigning `NF` to `0` will delete all the fields. However, a negative value will result in an error.

```
[](#cb95-1)$ echo 'goal:amazing:whistle:kwality' | awk -F: -v OFS=: '{NF=-1} 1'
[](#cb95-2)awk: cmd. line:1: (FILENAME=- FNR=1) fatal: NF set to negative value
```

## FPAT

`FS` allows to define input field separator. In contrast, `FPAT` (field pattern) allows to define what should the fields be made up of.

```
[](#cb96-1)$ s='Sample123string42with777numbers'
[](#cb96-2)
[](#cb96-3)$ # define fields to be one or more consecutive digits
[](#cb96-4)$ echo "$s" | awk -v FPAT='[0-9]+' '{print $2}'
[](#cb96-5)42
[](#cb96-6)
[](#cb96-7)$ # define fields to be one or more consecutive alphabets
[](#cb96-8)$ echo "$s" | awk -v FPAT='[a-zA-Z]+' -v OFS=, '{$1=$1} 1'
[](#cb96-9)Sample,string,with,numbers
```

`FPAT` is often used for `csv` input where fields can contain embedded delimiter characters. For example, a field content `"fox,42"` when `,` is the delimiter.

```
[](#cb97-1)$ s='eagle,"fox,42",bee,frog'
[](#cb97-2)
[](#cb97-3)$ # simply using , as separator isn't sufficient
[](#cb97-4)$ echo "$s" | awk -F, '{print $2}'
[](#cb97-5)"fox
```

For such simpler `csv` input, `FPAT` helps to define fields as starting and ending with double quotes or containing non-comma characters.

```
[](#cb98-1)$ # * is used instead of + to allow empty fields
[](#cb98-2)$ echo "$s" | awk -v FPAT='"[^"]*"|[^,]*' '{print $2}'
[](#cb98-3)"fox,42"
```

> ![warning](media/file1.svg) The above will not work for all kinds of `csv` files, for example if fields contain escaped double quotes, newline characters, etc. See [stackoverflow: What's the most robust way to efficiently parse CSV using awk?](https://stackoverflow.com/q/45420535/4082052) for such cases. You could also use other programming languages such as Perl, Python, Ruby, etc which come with standard `csv` parsing libraries or have easy access to third party solutions. There are also specialized command line tools such as [xsv](https://github.com/BurntSushi/xsv).

> ![info](media/file0.svg) If `IGNORECASE` is set, it will affect field matching. Unlike `FS`, there is no different behavior for single character pattern.

```
[](#cb99-1)$ # count number of 'e' in the input string
[](#cb99-2)$ echo 'Read Eat Sleep' | awk -v FPAT='e' '{print NF}'
[](#cb99-3)3
[](#cb99-4)$ echo 'Read Eat Sleep' | awk -v IGNORECASE=1 -v FPAT='e' '{print NF}'
[](#cb99-5)4
[](#cb99-6)$ echo 'Read Eat Sleep' | awk -v IGNORECASE=1 -v FPAT='[e]' '{print NF}'
[](#cb99-7)4
```

## FIELDWIDTHS

`FIELDWIDTHS` is another feature where you get to define field contents. As indicated by the name, you have to specify number of characters for each field. This method is useful to process fixed width file inputs, and especially when they can contain empty fields.

```
[](#cb100-1)$ cat items.txt
[](#cb100-2)apple   fig banana
[](#cb100-3)50      10  200
[](#cb100-4)
[](#cb100-5)$ # here field widths have been assigned such that
[](#cb100-6)$ # extra spaces are placed at the end of each field
[](#cb100-7)$ awk -v FIELDWIDTHS='8 4 6' '{print $2}' items.txt
[](#cb100-8)fig 
[](#cb100-9)10 
[](#cb100-10)$ # note that the field contents will include the spaces as well
[](#cb100-11)$ awk -v FIELDWIDTHS='8 4 6' '{print "[" $2 "]"}' items.txt
[](#cb100-12)[fig ]
[](#cb100-13)[10  ]
```

You can optionally prefix a field width with number of characters to be ignored.

```
[](#cb101-1)$ # first field is 5 characters
[](#cb101-2)$ # then 3 characters are ignored and 3 characters for second field
[](#cb101-3)$ # then 1 character is ignored and 6 characters for third field
[](#cb101-4)$ awk -v FIELDWIDTHS='5 3:3 1:6' '{print "[" $1 "]"}' items.txt
[](#cb101-5)[apple]
[](#cb101-6)[50   ]
[](#cb101-7)$ awk -v FIELDWIDTHS='5 3:3 1:6' '{print "[" $2 "]"}' items.txt
[](#cb101-8)[fig]
[](#cb101-9)[10 ]
```

If an input line length exceeds the total widths specified, the extra characters will simply be ignored. If you wish to access those characters, you can use `*` to represent the last field. See [gawk manual: FIELDWIDTHS](https://www.gnu.org/software/gawk/manual/gawk.html#Fields-with-fixed-data) for more corner cases.

```
[](#cb102-1)$ awk -v FIELDWIDTHS='5 *' '{print "[" $1 "]"}' items.txt
[](#cb102-2)[apple]
[](#cb102-3)[50   ]
[](#cb102-4)
[](#cb102-5)$ awk -v FIELDWIDTHS='5 *' '{print "[" $2 "]"}' items.txt
[](#cb102-6)[   fig banana]
[](#cb102-7)[   10  200]
```

## Summary

Working with fields is the most popular feature of `awk`. This chapter discussed various ways in which you can split the input into fields and manipulate them. There's many more examples to be discussed related to fields in upcoming chapters. I'd highly suggest to also read through [gawk manual: Fields](https://www.gnu.org/software/gawk/manual/gawk.html#Fields) for more details regarding field processing.

Next chapter will discuss various ways to use record separators and related special variables.

## Exercises

**a)** Extract only the contents between `()` or `)(` from each input line. Assume that `()` characters will be present only once every line.

```
[](#cb103-1)$ cat brackets.txt
[](#cb103-2)foo blah blah(ice) 123 xyz$ 
[](#cb103-3)(almond-pista) choco
[](#cb103-4)yo )yoyo( yo
[](#cb103-5)
[](#cb103-6)$ awk ##### add your solution here
[](#cb103-7)ice
[](#cb103-8)almond-pista
[](#cb103-9)yoyo
```

**b)** For the input file `scores.csv`, extract `Name` and `Physics` fields in the format shown below.

```
[](#cb104-1)$ cat scores.csv
[](#cb104-2)Name,Maths,Physics,Chemistry
[](#cb104-3)Blue,67,46,99
[](#cb104-4)Lin,78,83,80
[](#cb104-5)Er,56,79,92
[](#cb104-6)Cy,97,98,95
[](#cb104-7)Ort,68,72,66
[](#cb104-8)Ith,100,100,100
[](#cb104-9)
[](#cb104-10)$ awk ##### add your solution here
[](#cb104-11)Name:Physics
[](#cb104-12)Blue:46
[](#cb104-13)Lin:83
[](#cb104-14)Er:79
[](#cb104-15)Cy:98
[](#cb104-16)Ort:72
[](#cb104-17)Ith:100
```

**c)** For the input file `scores.csv`, display names of those who've scored above `70` in Maths.

```
[](#cb105-1)$ awk ##### add your solution here
[](#cb105-2)Lin
[](#cb105-3)Cy
[](#cb105-4)Ith
```

**d)** Display the number of word characters for the given inputs. Word definition here is same as used in regular expressions. Can you construct a solution with `gsub` and one without substitution functions?

```
[](#cb106-1)$ echo 'hi there' | awk ##### add your solution here
[](#cb106-2)7
[](#cb106-3)
[](#cb106-4)$ echo 'u-no;co%."(do_12:as' | awk ##### add your solution here
[](#cb106-5)12
```

**e)** Construct a solution that works for both the given sample inputs and the corresponding output shown. Solution shouldn't use substitution functions or string concatenation.

```
[](#cb107-1)$ echo '1 "grape" and "mango" and "guava"' | awk ##### add your solution here
[](#cb107-2)"grape","guava"
[](#cb107-3)
[](#cb107-4)$ echo '("a 1""b""c-2""d")' | awk ##### add your solution here
[](#cb107-5)"a 1","c-2"
```

**f)** Construct a solution that works for both the given sample inputs and the corresponding output shown. Solution shouldn't use substitution functions. Can you do it without explicitly using `print` function as well?

```
[](#cb108-1)$ echo 'hi,bye,there,was,here,to' | awk ##### add your solution here
[](#cb108-2)hi,bye,to
[](#cb108-3)
[](#cb108-4)$ echo '1,2,3,4,5' | awk ##### add your solution here
[](#cb108-5)1,2,5
```

**g)** Transform the given input file `fw.txt` to get the output as shown below. If a field is empty (i.e. contains only space characters), replace it with `NA`.

```
[](#cb109-1)$ cat fw.txt
[](#cb109-2)1.3  rs   90  0.134563
[](#cb109-3)3.8           6
[](#cb109-4)5.2  ye       8.2387
[](#cb109-5)4.2  kt   32  45.1
[](#cb109-6)
[](#cb109-7)$ awk ##### add your solution here
[](#cb109-8)1.3,rs,0.134563
[](#cb109-9)3.8,NA,6
[](#cb109-10)5.2,ye,8.2387
[](#cb109-11)4.2,kt,45.1
```

**h)** Display only the third and fifth characters from each line input line as shown below.

```
[](#cb110-1)$ printf 'restore\ncat one\ncricket' | awk ##### add your solution here
[](#cb110-2)so
[](#cb110-3)to
[](#cb110-4)ik
```

# Record separators

So far, you've seen examples where `awk` automatically splits input line by line based on the `\n` newline character. Just like you can control how those lines are further split into fields using `FS` and other features, `awk` provides a way to control what constitutes a line in the first place. In `awk` parlance, the term **record** is used to describe the contents that gets placed in the `$0` variable. And similar to `OFS`, you can control the string that gets added at the end for `print` function. This chapter will also discuss how you can use special variables that have information related to record (line) numbers.

## Input record separator

The `RS` special variable is used to control how the input content is split into records. The default is `\n` newline character, as evident with examples used in previous chapters. The special variable `NR` keeps track of the current record number.

```
[](#cb111-1)$ # changing input record separator to comma
[](#cb111-2)$ # note the content of second record, newline is just another character
[](#cb111-3)$ printf 'this,is\na,sample' | awk -v RS=, '{print NR ")", $0}'
[](#cb111-4)1) this
[](#cb111-5)2) is
[](#cb111-6)a
[](#cb111-7)3) sample
```

Recall that default `FS` will split input record based on spaces, tabs and newlines. Now that you've seen how `RS` can be something other than newline, here's an example to show the full effect of default record splitting.

```
[](#cb112-1)$ s='   a\t\tb:1000\n\n\n\n123 7777:x  y \n \n z  '
[](#cb112-2)$ printf '%b' "$s" | awk -v RS=: -v OFS=, '{$1=$1} 1'
[](#cb112-3)a,b
[](#cb112-4)1000,123,7777
[](#cb112-5)x,y,z
```

Similar to `FS`, the `RS` value is treated as a string literal and then converted to a regexp. For now, consider an example with multiple characters for `RS` but without needing regexp metacharacters.

```
[](#cb113-1)$ cat report.log
[](#cb113-2)blah blah Error: second record starts
[](#cb113-3)something went wrong
[](#cb113-4)some more details Error: third record
[](#cb113-5)details about what went wrong
[](#cb113-6)
[](#cb113-7)$ # uses 'Error:' as the input record separator
[](#cb113-8)$ # prints all the records that contains 'something'
[](#cb113-9)$ awk -v RS='Error:' '/something/' report.log
[](#cb113-10) second record starts
[](#cb113-11)something went wrong
[](#cb113-12)some more details 
```

> ![warning](media/file1.svg) If `IGNORECASE` is set, it will affect record separation as well. Except when record separator is a single character, which can be worked around by using a character class.

```
[](#cb114-1)$ awk -v IGNORECASE=1 -v RS='error:' 'NR==1' report.log
[](#cb114-2)blah blah 
[](#cb114-3)
[](#cb114-4)$ # when RS is a single character
[](#cb114-5)$ awk -v IGNORECASE=1 -v RS='e' 'NR==1' report.log
[](#cb114-6)blah blah Error: s
[](#cb114-7)$ awk -v IGNORECASE=1 -v RS='[e]' 'NR==1' report.log
[](#cb114-8)blah blah 
```

> ![warning](media/file1.svg) The default line ending for text files varies between different platforms. For example, a text file downloaded from internet or a file originating from Windows OS would typically have lines ending with carriage return and line feed characters. So, you'll have to use `RS='\r\n'` for such files. See also [stackoverflow: Why does my tool output overwrite itself and how do I fix it?](https://stackoverflow.com/q/45772525/4082052) for a detailed discussion and mitigation methods.

## Output record separator

The `ORS` special variable is used for output record separator. `ORS` is the string that gets added to the end of every call to the `print` function. The default value for `ORS` is a single newline character, just like `RS`.

```
[](#cb115-1)$ # change NUL record separator to dot and newline
[](#cb115-2)$ printf 'foo\0bar\0' | awk -v RS='\0' -v ORS='.\n' '1'
[](#cb115-3)foo.
[](#cb115-4)bar.
[](#cb115-5)
[](#cb115-6)$ cat msg.txt
[](#cb115-7)Hello there.
[](#cb115-8)It will rain to-
[](#cb115-9)day. Have a safe
[](#cb115-10)and pleasant jou-
[](#cb115-11)rney.
[](#cb115-12)$ # here ORS is empty string
[](#cb115-13)$ awk -v RS='-\n' -v ORS= '1' msg.txt
[](#cb115-14)Hello there.
[](#cb115-15)It will rain today. Have a safe
[](#cb115-16)and pleasant journey.
```

> ![info](media/file0.svg) Note that the `$0` variable is assigned after removing trailing characters matched by `RS`. Thus, you cannot directly manipulate those characters with functions like `sub`. With tools that don't automatically strip record separator, such as `perl`, the previous example can be solved as `perl -pe 's/-\n//' msg.txt`.

Many a times, you need to change `ORS` depending upon contents of input record or some other condition. The `cond ? expr1 : expr2` ternary operator is often used in such scenarios. The below example assumes that input is evenly divisible, you'll have to add more logic if that is not the case.

```
[](#cb116-1)$ # can also use RS instead of "\n" here
[](#cb116-2)$ seq 6 | awk '{ORS = NR%3 ? "-" : "\n"} 1'
[](#cb116-3)1-2-3
[](#cb116-4)4-5-6
```

> ![info](media/file0.svg) If the last line of input didn't end with the input record separator, it might get added in the output if `print` is used, as `ORS` gets appended.

```
[](#cb117-1)$ # here last line of input didn't end with newline
[](#cb117-2)$ # but gets added via ORS when 'print' is used
[](#cb117-3)$ printf '1\n2' | awk '1; END{print 3}'
[](#cb117-4)1
[](#cb117-5)2
[](#cb117-6)3
```

## Regexp RS and RT

As mentioned before, the value passed to `RS` is treated as a string literal and then converted to a regexp. Here's some examples.

```
[](#cb118-1)$ # set input record separator as one or more digit characters
[](#cb118-2)$ # print records containing 'i' and 't'
[](#cb118-3)$ printf 'Sample123string42with777numbers' | awk -v RS='[0-9]+' '/i/ && /t/'
[](#cb118-4)string
[](#cb118-5)with
[](#cb118-6)
[](#cb118-7)$ # similar to FS, the value passed to RS is string literal
[](#cb118-8)$ # which is then converted to regexp, so need \\ instead of \ here
[](#cb118-9)$ printf 'load;err_msg--ant,r2..not' | awk -v RS='\\W+' '/an/'
[](#cb118-10)ant
```

> ![info](media/file0.svg) First record will be empty if `RS` matches from the start of input file. However, if `RS` matches until the very last character of the input file, there won't be empty record as the last record. This is different from how `FS` behaves if it matches until the last character.

```
[](#cb119-1)$ # first record is empty and last record is newline character
[](#cb119-2)$ # change 'echo' command to 'printf' and see what changes
[](#cb119-3)$ echo '123string42with777' | awk -v RS='[0-9]+' '{print NR ") [" $0 "]"}'
[](#cb119-4)1) []
[](#cb119-5)2) [string]
[](#cb119-6)3) [with]
[](#cb119-7)4) [
[](#cb119-8)]
[](#cb119-9)
[](#cb119-10)$ printf '123string42with777' | awk -v FS='[0-9]+' '{print NF}'
[](#cb119-11)4
[](#cb119-12)$ printf '123string42with777' | awk -v RS='[0-9]+' 'END{print NR}'
[](#cb119-13)3
```

The `RT` special variable contains the text that was matched by `RS`. This variable gets updated for every input record.

```
[](#cb120-1)$ # print record number and value of RT for that record
[](#cb120-2)$ # last record has empty RT because it didn't end with digits
[](#cb120-3)$ echo 'Sample123string42with777numbers' | awk -v RS='[0-9]+' '{print NR, RT}'
[](#cb120-4)1 123
[](#cb120-5)2 42
[](#cb120-6)3 777
[](#cb120-7)4 
```

## Paragraph mode

As a special case, when `RS` is set to empty string, one or more consecutive empty lines is used as the input record separator. Consider the below sample file:

```
[](#cb121-1)$ cat programming_quotes.txt
[](#cb121-2)Debugging is twice as hard as writing the code in the first place.
[](#cb121-3)Therefore, if you write the code as cleverly as possible, you are,
[](#cb121-4)by definition, not smart enough to debug it by Brian W. Kernighan
[](#cb121-5)
[](#cb121-6)Some people, when confronted with a problem, think - I know, I will
[](#cb121-7)use regular expressions. Now they have two problems by Jamie Zawinski
[](#cb121-8)
[](#cb121-9)A language that does not affect the way you think about programming,
[](#cb121-10)is not worth knowing by Alan Perlis
[](#cb121-11)
[](#cb121-12)There are 2 hard problems in computer science: cache invalidation,
[](#cb121-13)naming things, and off-by-1 errors by Leon Bambrick
```

Here's an example of processing input paragraph wise.

```
[](#cb122-1)$ # print all paragraphs containing 'you'
[](#cb122-2)$ # note that there'll be an empty line after the last record
[](#cb122-3)$ awk -v RS= -v ORS='\n\n' '/you/' programming_quotes.txt
[](#cb122-4)Debugging is twice as hard as writing the code in the first place.
[](#cb122-5)Therefore, if you write the code as cleverly as possible, you are,
[](#cb122-6)by definition, not smart enough to debug it by Brian W. Kernighan
[](#cb122-7)
[](#cb122-8)A language that does not affect the way you think about programming,
[](#cb122-9)is not worth knowing by Alan Perlis
```

The empty line at the end is a common problem when dealing with custom record separators. You could either process the output to remove it or add logic to avoid the extras. Here's one workaround for the previous example.

```
[](#cb123-1)$ # here ORS is left as default newline character
[](#cb123-2)$ # uninitialized variable 's' will be empty for the first match
[](#cb123-3)$ # afterwards, 's' will provide the empty line separation
[](#cb123-4)$ awk -v RS= '/you/{print s $0; s="\n"}' programming_quotes.txt
[](#cb123-5)Debugging is twice as hard as writing the code in the first place.
[](#cb123-6)Therefore, if you write the code as cleverly as possible, you are,
[](#cb123-7)by definition, not smart enough to debug it by Brian W. Kernighan
[](#cb123-8)
[](#cb123-9)A language that does not affect the way you think about programming,
[](#cb123-10)is not worth knowing by Alan Perlis
```

Paragraph mode is not the same as using `RS='\n\n+'` because `awk` does a few more operations when `RS` is empty. See [gawk manual: multiline records](https://www.gnu.org/software/gawk/manual/html_node/Multiple-Line.html#Multiple-Line) for details. Important points are quoted below and illustrated with examples.

> However, there is an important difference between `RS = ""` and `RS = "\n\n+"`. In the first case, leading newlines in the input data file are ignored

```
[](#cb124-1)$ s='\n\n\na\nb\n\n12\n34\n\nhi\nhello\n'
[](#cb124-2)
[](#cb124-3)$ # paragraph mode
[](#cb124-4)$ printf '%b' "$s" | awk -v RS= -v ORS='\n---\n' 'NR<=2'
[](#cb124-5)a
[](#cb124-6)b
[](#cb124-7)---
[](#cb124-8)12
[](#cb124-9)34
[](#cb124-10)---
[](#cb124-11)
[](#cb124-12)$ # RS is '\n\n+' instead of paragraph mode
[](#cb124-13)$ printf '%b' "$s" | awk -v RS='\n\n+' -v ORS='\n---\n' 'NR<=2'
[](#cb124-14)
[](#cb124-15)---
[](#cb124-16)a
[](#cb124-17)b
[](#cb124-18)---
```

> and if a file ends without extra blank lines after the last record, the final newline is removed from the record. In the second case, this special processing is not done.

```
[](#cb125-1)$ s='\n\n\na\nb\n\n12\n34\n\nhi\nhello\n'
[](#cb125-2)
[](#cb125-3)$ # paragraph mode
[](#cb125-4)$ printf '%b' "$s" | awk -v RS= -v ORS='\n---\n' 'END{print}'
[](#cb125-5)hi
[](#cb125-6)hello
[](#cb125-7)---
[](#cb125-8)
[](#cb125-9)$ # RS is '\n\n+' instead of paragraph mode
[](#cb125-10)$ printf '%b' "$s" | awk -v RS='\n\n+' -v ORS='\n---\n' 'END{print}'
[](#cb125-11)hi
[](#cb125-12)hello
[](#cb125-13)
[](#cb125-14)---
```

> When RS is set to the empty string and FS is set to a single character, the newline character always acts as a field separator. This is in addition to whatever field separations result from FS. When FS is the null string (`""`) or a regexp, this special feature of RS does not apply. It does apply to the default field separator of a single space: `FS = " "`

```
[](#cb126-1)$ s='a:b\nc:d\n\n1\n2\n3'
[](#cb126-2)
[](#cb126-3)$ # FS is a single character in paragraph mode
[](#cb126-4)$ printf '%b' "$s" | awk -F: -v RS= -v ORS='\n---\n' '{$1=$1} 1'
[](#cb126-5)a b c d
[](#cb126-6)---
[](#cb126-7)1 2 3
[](#cb126-8)---
[](#cb126-9)
[](#cb126-10)$ # FS is a regexp in paragraph mode
[](#cb126-11)$ printf '%b' "$s" | awk -F':+' -v RS= -v ORS='\n---\n' '{$1=$1} 1'
[](#cb126-12)a b
[](#cb126-13)c d
[](#cb126-14)---
[](#cb126-15)1
[](#cb126-16)2
[](#cb126-17)3
[](#cb126-18)---
[](#cb126-19)
[](#cb126-20)$ # FS is single character and RS is '\n\n+' instead of paragraph mode
[](#cb126-21)$ printf '%b' "$s" | awk -F: -v RS='\n\n+' -v ORS='\n---\n' '{$1=$1} 1'
[](#cb126-22)a b
[](#cb126-23)c d
[](#cb126-24)---
[](#cb126-25)1
[](#cb126-26)2
[](#cb126-27)3
[](#cb126-28)---
```

## NR vs FNR

There are two special variables related to record number. You've seen `NR` earlier in the chapter, but here's some more examples.

```
[](#cb127-1)$ # same as: head -n2
[](#cb127-2)$ seq 5 | awk 'NR<=2'
[](#cb127-3)1
[](#cb127-4)2
[](#cb127-5)
[](#cb127-6)$ # same as: tail -n1
[](#cb127-7)$ awk 'END{print}' table.txt
[](#cb127-8)yellow banana window shoes 3.14
[](#cb127-9)
[](#cb127-10)$ # change first field content only for second line
[](#cb127-11)$ awk 'NR==2{$1="green"} 1' table.txt
[](#cb127-12)brown bread mat hair 42
[](#cb127-13)green cake mug shirt -7
[](#cb127-14)yellow banana window shoes 3.14
```

All the examples with `NR` so far has been with single file input. If there are multiple file inputs, then you can choose between `NR` and the second special variable `FNR`. The difference is that `NR` contains total records read so far whereas `FNR` contains record number of only the current file being processed. Here's some examples to show them in action. You'll see more examples in later chapters as well.

```
[](#cb128-1)$ awk -v OFS='\t' 'BEGIN{print "NR", "FNR", "Content"}
[](#cb128-2) {print NR, FNR, $0}' report.log table.txt
[](#cb128-3)NR      FNR     Content
[](#cb128-4)1       1       blah blah Error: second record starts
[](#cb128-5)2       2       something went wrong
[](#cb128-6)3       3       some more details Error: third record
[](#cb128-7)4       4       details about what went wrong
[](#cb128-8)5       1       brown bread mat hair 42
[](#cb128-9)6       2       blue cake mug shirt -7
[](#cb128-10)7       3       yellow banana window shoes 3.14
[](#cb128-11)
[](#cb128-12)$ # same as: head -q -n1
[](#cb128-13)$ awk 'FNR==1' report.log table.txt
[](#cb128-14)blah blah Error: second record starts
[](#cb128-15)brown bread mat hair 42
```

> ![info](media/file0.svg) For large input files, use `exit` to avoid unnecessary record processing.

```
[](#cb129-1)$ seq 3542 4623452 | awk 'NR==2452{print; exit}'
[](#cb129-2)5993
[](#cb129-3)$ seq 3542 4623452 | awk 'NR==250; NR==2452{print; exit}'
[](#cb129-4)3791
[](#cb129-5)5993
[](#cb129-6)
[](#cb129-7)$ # here is a sample time comparison
[](#cb129-8)$ time seq 3542 4623452 | awk 'NR==2452{print; exit}' > f1
[](#cb129-9)real    0m0.004s
[](#cb129-10)$ time seq 3542 4623452 | awk 'NR==2452' > f2
[](#cb129-11)real    0m0.395s
```

## Summary

This chapter showed you how to change the way input content is split into records and how to set the string to be appended when `print` is used. The paragraph mode is useful for processing multiline records separated by empty lines. You also learned two special variables related to record numbers and where to use them.

So far, you've used `awk` to manipulate file content without modifying the source file. The next chapter will discuss how to write back the changes to the original input files.

## Exercises

**a)** The input file `jumbled.txt` consists of words separated by various delimiters. Display all words that contain `an` or `at` or `in` or `it`, one per line.

```
[](#cb130-1)$ cat jumbled.txt
[](#cb130-2)overcoats;furrowing-typeface%pewter##hobby
[](#cb130-3)wavering:concession/woof\retailer
[](#cb130-4)joint[]seer{intuition}titanic
[](#cb130-5)
[](#cb130-6)$ awk ##### add your solution here
[](#cb130-7)overcoats
[](#cb130-8)furrowing
[](#cb130-9)wavering
[](#cb130-10)joint
[](#cb130-11)intuition
[](#cb130-12)titanic
```

**b)** Emulate `paste -sd,` with `awk`.

```
[](#cb131-1)$ # this command joins all input lines with ',' character
[](#cb131-2)$ paste -sd, addr.txt
[](#cb131-3)Hello World,How are you,This game is good,Today is sunny,12345,You are funny
[](#cb131-4)$ # make sure there's no ',' at end of the line
[](#cb131-5)$ # and that there's a newline character at the end of the line
[](#cb131-6)$ awk ##### add your solution here
[](#cb131-7)Hello World,How are you,This game is good,Today is sunny,12345,You are funny
[](#cb131-8)
[](#cb131-9)$ # if there's only one line in input, again make sure there's no trailing ','
[](#cb131-10)$ printf 'foo' | paste -sd,
[](#cb131-11)foo
[](#cb131-12)$ printf 'foo' | awk ##### add your solution here
[](#cb131-13)foo
```

**c)** For the input file `scores.csv`, add another column named `GP` which is calculated out of `100` by giving `50%` weightage to `Maths` and `25%` each for `Physics` and `Chemistry`.

```
[](#cb132-1)$ awk ##### add your solution here
[](#cb132-2)Name,Maths,Physics,Chemistry,GP
[](#cb132-3)Blue,67,46,99,69.75
[](#cb132-4)Lin,78,83,80,79.75
[](#cb132-5)Er,56,79,92,70.75
[](#cb132-6)Cy,97,98,95,96.75
[](#cb132-7)Ort,68,72,66,68.5
[](#cb132-8)Ith,100,100,100,100
```

**d)** For the input file `sample.txt`, extract all paragraphs containing `do` and exactly two lines.

```
[](#cb133-1)$ cat sample.txt
[](#cb133-2)Hello World
[](#cb133-3)
[](#cb133-4)Good day
[](#cb133-5)How are you
[](#cb133-6)
[](#cb133-7)Just do-it
[](#cb133-8)Believe it
[](#cb133-9)
[](#cb133-10)Today is sunny
[](#cb133-11)Not a bit funny
[](#cb133-12)No doubt you like it too
[](#cb133-13)
[](#cb133-14)Much ado about nothing
[](#cb133-15)He he he
[](#cb133-16)
[](#cb133-17)$ # note that there's no extra empty line at the end of the output
[](#cb133-18)$ awk ##### add your solution here
[](#cb133-19)Just do-it
[](#cb133-20)Believe it
[](#cb133-21)
[](#cb133-22)Much ado about nothing
[](#cb133-23)He he he
```

**e)** For the input file `sample.txt`, change all paragraphs into single line by joining lines using `.` and a space character as the separator. And add a final `.` to each paragraph.

```
[](#cb134-1)$ # note that there's no extra empty line at the end of the output
[](#cb134-2)$ awk ##### add your solution here
[](#cb134-3)Hello World.
[](#cb134-4)
[](#cb134-5)Good day. How are you.
[](#cb134-6)
[](#cb134-7)Just do-it. Believe it.
[](#cb134-8)
[](#cb134-9)Today is sunny. Not a bit funny. No doubt you like it too.
[](#cb134-10)
[](#cb134-11)Much ado about nothing. He he he.
```

**f)** The various input/output separators can be changed dynamically and comes into effect during the next input/output operation. For the input file `mixed_fs.txt`, retain only first two fields from each input line. The field separators should be space for first two lines and `,` for the rest of the lines.

```
[](#cb135-1)$ cat mixed_fs.txt
[](#cb135-2)rose lily jasmine tulip
[](#cb135-3)pink blue white yellow
[](#cb135-4)car,mat,ball,basket
[](#cb135-5)green,brown,black,purple
[](#cb135-6)
[](#cb135-7)$ awk ##### add your solution here
[](#cb135-8)rose lily
[](#cb135-9)pink blue
[](#cb135-10)car,mat
[](#cb135-11)green,brown
```

**g)** For the input file `table.txt`, get the outputs shown below. All of them feature line number as part of the solution.

```
[](#cb136-1)$ # print other than second line
[](#cb136-2)$ awk ##### add your solution here
[](#cb136-3)brown bread mat hair 42
[](#cb136-4)yellow banana window shoes 3.14
[](#cb136-5)
[](#cb136-6)$ # print line number of lines containing 'air' or 'win'
[](#cb136-7)$ awk ##### add your solution here
[](#cb136-8)1
[](#cb136-9)3
[](#cb136-10)
[](#cb136-11)$ # calculate the sum of numbers in last column, except second line
[](#cb136-12)$ awk ##### add your solution here
[](#cb136-13)45.14
```

**h)** Print second and fourth line for every block of five lines.

```
[](#cb137-1)$ seq 15 | awk ##### add your solution here
[](#cb137-2)2
[](#cb137-3)4
[](#cb137-4)7
[](#cb137-5)9
[](#cb137-6)12
[](#cb137-7)14
```

**i)** For the input file `odd.txt`, surround all whole words with `{}` that start and end with the same word character. This is a contrived exercise to make you use `RT`. In real world, you can use `sed -E 's/\b(\w|(\w)\w*\2)\b/{&}/g' odd.txt` to solve this.

```
[](#cb138-1)$ cat odd.txt
[](#cb138-2)-oreo-not:a _a2_ roar<=>took%22
[](#cb138-3)RoaR to wow-
[](#cb138-4)
[](#cb138-5)$ awk ##### add your solution here
[](#cb138-6)-{oreo}-not:{a} {_a2_} {roar}<=>took%{22}
[](#cb138-7){RoaR} to {wow}-
```

# In-place file editing

In the examples presented so far, the output from `awk` was displayed on the terminal. This chapter will discuss how to write back the changes to the input file(s) itself using the `-i` command line option. This option can be configured to make changes to the input file(s) with or without creating a backup of original contents.

## Without backup

The `-i` option allows you to load libraries (see [gawk manual: -i option](https://www.gnu.org/software/gawk/manual/gawk.html#index-_002di-option) for details). `inplace` library comes by default with the `awk` installation. Use `-i inplace` to indicate that `awk` should modify the original input itself. Use this option with caution, preferably after testing that the code is working as intended.

```
[](#cb139-1)$ cat greet.txt
[](#cb139-2)Hi there
[](#cb139-3)Have a nice day
[](#cb139-4)Good bye
[](#cb139-5)
[](#cb139-6)$ # prefix line numbers
[](#cb139-7)$ awk -i inplace '{print NR ". " $0}' greet.txt
[](#cb139-8)$ cat greet.txt
[](#cb139-9)1. Hi there
[](#cb139-10)2. Have a nice day
[](#cb139-11)3. Good bye
```

Multiple input files are treated individually and changes are written back to respective files.

```
[](#cb140-1)$ cat f1.txt
[](#cb140-2)I ate 3 apples
[](#cb140-3)$ cat f2.txt
[](#cb140-4)I bought two balls and 3 bats
[](#cb140-5)
[](#cb140-6)$ awk -i inplace '{gsub(/\<3\>/, "three")} 1' f1.txt f2.txt
[](#cb140-7)$ cat f1.txt
[](#cb140-8)I ate three apples
[](#cb140-9)$ cat f2.txt
[](#cb140-10)I bought two balls and three bats
```

## With backup

You can provide a backup extension by setting the `inplace::suffix` special variable. For example, if the input file is `ip.txt` and `inplace::suffix='.orig'` is used, the backup file will be named as `ip.txt.orig`.

```
[](#cb141-1)$ cat f3.txt
[](#cb141-2)  Name    Physics  Maths
[](#cb141-3) Moe  76  82
[](#cb141-4)Raj  56  64
[](#cb141-5)
[](#cb141-6)$ awk -i inplace -v inplace::suffix='.bkp' -v OFS=, '{$1=$1} 1' f3.txt
[](#cb141-7)$ cat f3.txt
[](#cb141-8)Name,Physics,Maths
[](#cb141-9)Moe,76,82
[](#cb141-10)Raj,56,64
[](#cb141-11)
[](#cb141-12)$ # original file is preserved in 'f3.txt.bkp'
[](#cb141-13)$ cat f3.txt.bkp
[](#cb141-14)  Name    Physics  Maths
[](#cb141-15) Moe  76  82
[](#cb141-16)Raj  56  64
```

> ![info](media/file0.svg) Earlier versions of `awk` used `INPLACE_SUFFIX` variable instead of `inplace::suffix`. Also, you can use `inplace::enable` variable to dynamically control whether files should be in-placed or not. See [gawk manual: Enabling In-Place File Editing](https://www.gnu.org/software/gawk/manual/gawk.html#Extension-Sample-Inplace) for more details.

## Summary

This chapter discussed about the `-i inplace` option which is useful when you need to edit a file in-place. This is particularly useful in automation scripts. But, do ensure that you have tested the `awk` command before applying to actual files if you need to use this option without creating backups.

The next chapter will revisit the use of shell variables in `awk` commands.

## Exercises

**a)** For the input file `copyright.txt`, replace `copyright: 2018` with `copyright: 2020` and write back the changes to `copyright.txt` itself. The original contents should get saved to `copyright.txt.orig`

```
[](#cb142-1)$ cat copyright.txt
[](#cb142-2)bla bla 2015 bla
[](#cb142-3)blah 2018 blah
[](#cb142-4)bla bla bla
[](#cb142-5)copyright: 2018
[](#cb142-6)$ awk ##### add your solution here
[](#cb142-7)
[](#cb142-8)$ cat copyright.txt
[](#cb142-9)bla bla 2015 bla
[](#cb142-10)blah 2018 blah
[](#cb142-11)bla bla bla
[](#cb142-12)copyright: 2020
[](#cb142-13)$ cat copyright.txt.orig
[](#cb142-14)bla bla 2015 bla
[](#cb142-15)blah 2018 blah
[](#cb142-16)bla bla bla
[](#cb142-17)copyright: 2018
```

**b)** For the input files `nums1.txt` and `nums2.txt`, retain only second and third lines and write back the changes to their respective files. No need to create backups.

```
[](#cb143-1)$ cat nums1.txt
[](#cb143-2)3.14
[](#cb143-3)4201
[](#cb143-4)777
[](#cb143-5)0323012
[](#cb143-6)$ cat nums2.txt
[](#cb143-7)-45.4
[](#cb143-8)-2
[](#cb143-9)54316.12
[](#cb143-10)0x231
[](#cb143-11)
[](#cb143-12)$ awk ##### add your solution here
[](#cb143-13)$ cat nums1.txt
[](#cb143-14)4201
[](#cb143-15)777
[](#cb143-16)$ cat nums2.txt
[](#cb143-17)-2
[](#cb143-18)54316.12
```

# Using shell variables

When it comes to automation and scripting, you'd often need to construct commands that can accept input from user, file, output of a shell command, etc. As mentioned before, this book assumes `bash` as the shell being used.

> ![info](media/file0.svg) As an example, see my repo [ch: command help](https://github.com/learnbyexample/command_help/blob/master/ch) for a practical shell script, where commands are constructed dynamically.

## -v option

The most common method is to use the `-v` command line option.

```
[](#cb144-1)$ # assume that the 's' variable is part of some bash script
[](#cb144-2)$ # or perhaps a variable that has stored the output of a shell command
[](#cb144-3)$ s='cake'
[](#cb144-4)$ awk -v word="$s" '$2==word' table.txt
[](#cb144-5)blue cake mug shirt -7
```

## ENVIRON

To access environment variables of the shell, you can call the special array variable `ENVIRON` with the name of the environment variable as a string key.

```
[](#cb145-1)$ # existing environment variable
[](#cb145-2)$ # output shown here is for my machine, would differ for you
[](#cb145-3)$ awk 'BEGIN{print ENVIRON["HOME"]}'
[](#cb145-4)/home/learnbyexample
[](#cb145-5)$ awk 'BEGIN{print ENVIRON["SHELL"]}'
[](#cb145-6)/bin/bash
[](#cb145-7)
[](#cb145-8)$ # defined along with awk command
[](#cb145-9)$ # note that the variable is placed before awk
[](#cb145-10)$ word='hello' awk 'BEGIN{print ENVIRON["word"]}'
[](#cb145-11)hello
```

`ENVIRON` is a good way to get around `awk`'s interpretation of escape sequences. This is especially helpful for fixed string matching, see [index](#ch010.xhtml_index) section for examples.

```
[](#cb146-1)$ s='hi\nbye'
[](#cb146-2)
[](#cb146-3)$ # when passed via -v option
[](#cb146-4)$ awk -v ip="$s" 'BEGIN{print ip}'
[](#cb146-5)hi
[](#cb146-6)bye
[](#cb146-7)
[](#cb146-8)$ # when passed as an environment variable
[](#cb146-9)$ ip="$s" awk 'BEGIN{print ENVIRON["ip"]}'
[](#cb146-10)hi\nbye
```

Here's another example when a regexp is passed to an `awk` command.

```
[](#cb147-1)$ # when passed via -v option
[](#cb147-2)$ r='\Bpar\B'
[](#cb147-3)$ awk -v rgx="$r" '$0 ~ rgx' word_anchors.txt
[](#cb147-4)awk: warning: escape sequence `\B' treated as plain `B'
[](#cb147-5)$ r='\\Bpar\\B'
[](#cb147-6)$ awk -v rgx="$r" '$0 ~ rgx' word_anchors.txt
[](#cb147-7)apparent effort
[](#cb147-8)two spare computers
[](#cb147-9)
[](#cb147-10)$ # when passed as an environment variable
[](#cb147-11)$ r='\Bpar\B'
[](#cb147-12)$ rgx="$r" awk '$0 ~ ENVIRON["rgx"]' word_anchors.txt
[](#cb147-13)apparent effort
[](#cb147-14)two spare computers
```

## Summary

This short chapter revisited the `-v` command line option and introduced the `ENVIRON` special array. These are particularly useful when the `awk` command is part of a shell script. More about arrays will be discussed in later chapters.

The next chapter will cover control structures.

## Exercises

**a)** Use contents of `s` variable to display all matching lines from the input file `sample.txt`. Assume that the `s` variable doesn't have any regexp metacharacters and construct a solution such that only whole words are matched.

```
[](#cb148-1)$ s='do'
[](#cb148-2)$ ##### add your solution here
[](#cb148-3)Just do-it
```

**b)** Replace all occurrences of `o` for the input file `addr.txt` with literal contents of `s` variable. Assume that the `s` variable has regexp metacharacters.

```
[](#cb149-1)$ s='\&/'
[](#cb149-2)$ ##### add your solution here
[](#cb149-3)Hell\&/ W\&/rld
[](#cb149-4)H\&/w are y\&/u
[](#cb149-5)This game is g\&/\&/d
[](#cb149-6)T\&/day is sunny
[](#cb149-7)12345
[](#cb149-8)Y\&/u are funny
```

# Control Structures

You've already seen various examples requiring conditional expressions. This chapter will revisit `if-else` control structure along with the ternary operator. Then you will see some examples with explicit loops (recall that `awk` is already looping over input records). Followed by keywords that control loop flow. Most of the syntax is very similar to the `C` language.

## if-else

Mostly, when you need to use `if` control structure, you can get away with using `condX{actionX}` format in `awk` one-liners. But sometimes, you need additional condition checking within such action blocks. Or, you might need it inside loops. The syntax is `if(cond){action}` where the braces are optional if you need only one statement. `if` can be optionally followed by multiple `else if` conditions and a final `else` condition. These can also be nested as needed.

```
[](#cb150-1)$ # print all lines starting with 'b'
[](#cb150-2)$ # additionally, if last column is > 0, then print some more info
[](#cb150-3)$ awk '/^b/{print; if($NF>0) print "------"}' table.txt
[](#cb150-4)brown bread mat hair 42
[](#cb150-5)------
[](#cb150-6)blue cake mug shirt -7
[](#cb150-7)
[](#cb150-8)$ # same as above, but includes 'else' condition as well
[](#cb150-9)$ awk '/^b/{print; if($NF>0) print "------"; else print "======"}' table.txt
[](#cb150-10)brown bread mat hair 42
[](#cb150-11)------
[](#cb150-12)blue cake mug shirt -7
[](#cb150-13)======
```

The ternary operator often reduces the need for single statement `if-else` cases.

```
[](#cb151-1)$ # same as: awk '{if(NR%3) ORS="-" ; else ORS=RS} 1'
[](#cb151-2)$ seq 6 | awk '{ORS = NR%3 ? "-" : RS} 1'
[](#cb151-3)1-2-3
[](#cb151-4)4-5-6
[](#cb151-5)
[](#cb151-6)$ # note that parentheses is necessary for print in this case
[](#cb151-7)$ awk '/^b/{print; print($NF>0 ? "------" : "======")}' table.txt
[](#cb151-8)brown bread mat hair 42
[](#cb151-9)------
[](#cb151-10)blue cake mug shirt -7
[](#cb151-11)======
```

> ![info](media/file0.svg) See also [stackoverflow: finding min and max value of a column](https://stackoverflow.com/a/29784278).

> ![info](media/file0.svg) See also [gawk manual: switch](https://www.gnu.org/software/gawk/manual/gawk.html#Switch-Statement).

## loops

`for` loops are handy when you are working with arrays. Also for processing input fields, since `$N` syntax allows passing an expression instead of fixed value.

```
[](#cb152-1)$ awk 'BEGIN{for(i=2; i<7; i+=2) print i}'
[](#cb152-2)2
[](#cb152-3)4
[](#cb152-4)6
[](#cb152-5)
[](#cb152-6)$ # looping each field
[](#cb152-7)$ awk -v OFS=, '{for(i=1; i<=NF; i++) if($i ~ /^[bm]/) $i="["$i"]"} 1' table.txt
[](#cb152-8)[brown],[bread],[mat],hair,42
[](#cb152-9)[blue],cake,[mug],shirt,-7
[](#cb152-10)yellow,[banana],window,shoes,3.14
```

Here's an example of looping over a dynamically constructed array.

```
[](#cb153-1)$ cat marks.txt
[](#cb153-2)Dept    Name    Marks
[](#cb153-3)ECE     Raj     53
[](#cb153-4)ECE     Joel    72
[](#cb153-5)EEE     Moi     68
[](#cb153-6)CSE     Surya   81
[](#cb153-7)EEE     Tia     59
[](#cb153-8)ECE     Om      92
[](#cb153-9)CSE     Amy     67
[](#cb153-10)
[](#cb153-11)$ # average marks for each department
[](#cb153-12)$ awk 'NR>1{d[$1]+=$3; c[$1]++} END{for(k in d) print k, d[k]/c[k]}' marks.txt
[](#cb153-13)ECE 72.3333
[](#cb153-14)EEE 63.5
[](#cb153-15)CSE 74
```

You can use `break` and `continue` to alter the normal flow of loops. `break` will cause the current loop to quit immediately without processing the remaining statements and iterations. `continue` will skip the remaining statements in the loop and start next iteration.

```
[](#cb154-1)$ awk -v OFS=, '{for(i=1; i<=NF; i++) if($i ~ /b/){NF=i; break}} 1' table.txt
[](#cb154-2)brown
[](#cb154-3)blue
[](#cb154-4)yellow,banana
```

> ![info](media/file0.svg) See also [stackoverflow: find missing numbers from sequential list](https://stackoverflow.com/q/38491676/4082052).

`awk` supports `while` and `do-while` loop mechanisms as well.

```
[](#cb155-1)$ awk 'BEGIN{i=6; while(i>0){print i; i-=2}}'
[](#cb155-2)6
[](#cb155-3)4
[](#cb155-4)2
[](#cb155-5)
[](#cb155-6)$ # recursive substitution
[](#cb155-7)$ echo 'titillate' | awk '{while(gsub(/til/, "")) print}'
[](#cb155-8)tilate
[](#cb155-9)ate
[](#cb155-10)$ echo 'titillate' | awk '{do{print} while(gsub(/til/, ""))}'
[](#cb155-11)titillate
[](#cb155-12)tilate
[](#cb155-13)ate
```

## next

`next` is similar to `continue` statement but it acts on the default loop that goes through the input records. It doesn't affect `BEGIN` or `END` blocks as they are outside the record looping. When `next` is executed, rest of the statements will be skipped and next input record will be fetched for processing.

```
[](#cb156-1)$ awk '/\<par/{print "%% " $0; next} {print /s/ ? "X" : "Y"}' word_anchors.txt
[](#cb156-2)%% sub par
[](#cb156-3)X
[](#cb156-4)Y
[](#cb156-5)X
[](#cb156-6)%% cart part tart mart
```

You'll see more examples with `next` in coming chapters.

## exit

You saw the use of `exit` earlier to quit early and avoid unnecessary processing of records. If an argument isn't passed, `awk` considers the command to have finished normally and **exit status** will indicate success. You can pass a number to indicate other cases.

```
[](#cb157-1)$ seq 3542 4623452 | awk 'NR==2452{print; exit}'
[](#cb157-2)5993
[](#cb157-3)$ echo $?
[](#cb157-4)0
[](#cb157-5)
[](#cb157-6)$ awk '/^br/{print "Invalid input"; exit 1}' table.txt
[](#cb157-7)Invalid input
[](#cb157-8)$ echo $?
[](#cb157-9)1
[](#cb157-10)
[](#cb157-11)$ # any remaining files to be processed are also skipped
[](#cb157-12)$ awk 'FNR==2{print; exit}' table.txt greeting.txt
[](#cb157-13)blue cake mug shirt -7
```

If `exit` is used in `BEGIN` or normal blocks, any code in `END` block will still be executed. For more details and corner cases, see [gawk manual: exit](https://www.gnu.org/software/gawk/manual/gawk.html#Exit-Statement).

```
[](#cb158-1)$ # first print is executed
[](#cb158-2)$ # on seeing exit, rest of BEGIN and normal blocks are skipped
[](#cb158-3)$ # code in END is then executed
[](#cb158-4)$ awk 'BEGIN{print "hi"; exit; print "hello"}
[](#cb158-5) /^b/;
[](#cb158-6) END{print "bye"}' table.txt
[](#cb158-7)hi
[](#cb158-8)bye
```

## Summary

This chapter covered some of the control flow structures provided by `awk`. These features makes `awk` flexible and easier to use compared to `sed` for those familiar with programming languages.

Next chapter will discuss some of the built-in functions.

## Exercises

**a)** The input file `nums.txt` contains single column of numbers. Change positive numbers to negative and vice versa. Can you do it with using only `sub` function and without explicit use of `if-else` or ternary operator?

```
[](#cb159-1)$ cat nums.txt
[](#cb159-2)42
[](#cb159-3)-2
[](#cb159-4)10101
[](#cb159-5)-3.14
[](#cb159-6)-75
[](#cb159-7)
[](#cb159-8)$ awk ##### add your solution here
[](#cb159-9)-42
[](#cb159-10)2
[](#cb159-11)-10101
[](#cb159-12)3.14
[](#cb159-13)75
```

**b)** For the input file `table.txt`, change the field separator from space to `,` character. Also, any field not containing digit characters should be surrounded by double quotes.

```
[](#cb160-1)$ awk ##### add your solution here
[](#cb160-2)"brown","bread","mat","hair",42
[](#cb160-3)"blue","cake","mug","shirt",-7
[](#cb160-4)"yellow","banana","window","shoes",3.14
```

**c)** For each input line of the file `secrets.txt`, remove all characters except the last character of each field. Assume space as the input field separator.

```
[](#cb161-1)$ cat secrets.txt
[](#cb161-2)stag area row tick
[](#cb161-3)deaf chi rate tall glad
[](#cb161-4)Bi tac toe - 42
[](#cb161-5)
[](#cb161-6)$ awk ##### add your solution here
[](#cb161-7)gawk
[](#cb161-8)field
[](#cb161-9)ice-2
```

**d)** Emulate `q` and `Q` commands of `sed` as shown below.

```
[](#cb162-1)$ # sed '/are/q' sample.txt will print until (and including) line contains 'are'
[](#cb162-2)$ awk ##### add your solution here
[](#cb162-3)Hello World
[](#cb162-4)
[](#cb162-5)Good day
[](#cb162-6)How are you
[](#cb162-7)
[](#cb162-8)$ # sed '/are/Q' sample.txt will print until (but excluding) line contains 'are'
[](#cb162-9)$ awk ##### add your solution here
[](#cb162-10)Hello World
[](#cb162-11)
[](#cb162-12)Good day
```

**e)** For the input file `addr.txt`:

*   if line contains `e`
    *   delete all occurrences of `e`
    *   surround all consecutive repeated characters with `{}`
    *   assume that input will not have more than two consecutive repeats
*   if line doesn't contain `e` but contains `u`
    *   surround all lowercase vowels in that line with `[]`

```
[](#cb163-1)$ awk ##### add your solution here
[](#cb163-2)H{ll}o World
[](#cb163-3)How ar you
[](#cb163-4)This gam is g{oo}d
[](#cb163-5)T[o]d[a]y [i]s s[u]nny
[](#cb163-6)12345
[](#cb163-7)You ar fu{nn}y
```

# Built-in functions

You've already seen some built-in functions in detail, such as `sub`, `gsub` and `gensub` functions. This chapter will discuss many more built-ins that are often used in one-liners. You'll also see more examples with arrays.

> ![info](media/file0.svg) See [gawk manual: Functions](https://www.gnu.org/software/gawk/manual/gawk.html#Functions) for details about all the built-in functions as well as how to define your own functions.

## length

`length` function returns number of characters for the given string argument. By default, it acts on `$0` variable and a number argument is converted to string automatically.

```
[](#cb164-1)$ awk 'BEGIN{print length("road"); print length(123456)}'
[](#cb164-2)4
[](#cb164-3)6
[](#cb164-4)
[](#cb164-5)$ # recall that record separator isn't part of $0
[](#cb164-6)$ # so, line ending won't be counted here
[](#cb164-7)$ printf 'fox\ntiger\n' | awk '{print length()}'
[](#cb164-8)3
[](#cb164-9)5
[](#cb164-10)
[](#cb164-11)$ awk 'length($1) < 6' table.txt
[](#cb164-12)brown bread mat hair 42
[](#cb164-13)blue cake mug shirt -7
```

If you need number of bytes, instead of number of characters, then use the `-b` command line option as well. Locale can also play a role.

```
[](#cb165-1)$ echo 'αλεπού' | awk '{print length()}'
[](#cb165-2)6
[](#cb165-3)$ echo 'αλεπού' | awk -b '{print length()}'
[](#cb165-4)12
[](#cb165-5)$ echo 'αλεπού' | LC_ALL=C awk '{print length()}'
[](#cb165-6)12
```

## Array sorting

By default, array looping with `for(key in array)` format gives you elements in random order. By setting a special value to `PROCINFO["sorted_in"]`, you can control the order in which you wish to retrieve the elements. See [gawk manual: Using Predefined Array Scanning Orders](https://www.gnu.org/software/gawk/manual/gawk.html#Controlling-Scanning) for other options and details.

```
[](#cb166-1)$ # by default, array is traversed in random order
[](#cb166-2)$ awk 'BEGIN{a["z"]=1; a["x"]=12; a["b"]=42; for(i in a) print i, a[i]}'
[](#cb166-3)x 12
[](#cb166-4)z 1
[](#cb166-5)b 42
[](#cb166-6)
[](#cb166-7)$ # index (i.e. keys) sorted in ascending order as strings
[](#cb166-8)$ awk 'BEGIN{PROCINFO["sorted_in"] = "@ind_str_asc";
[](#cb166-9) a["z"]=1; a["x"]=12; a["b"]=42; for(i in a) print i, a[i]}'
[](#cb166-10)b 42
[](#cb166-11)x 12
[](#cb166-12)z 1
[](#cb166-13)
[](#cb166-14)$ # value sorted in ascending order as numbers
[](#cb166-15)$ awk 'BEGIN{PROCINFO["sorted_in"] = "@val_num_asc";
[](#cb166-16) a["z"]=1; a["x"]=12; a["b"]=42; for(i in a) print i, a[i]}'
[](#cb166-17)z 1
[](#cb166-18)x 12
[](#cb166-19)b 42
```

Here's an example of sorting input lines in ascending order based on second column, treating the data as string.

```
[](#cb167-1)$ awk 'BEGIN{PROCINFO["sorted_in"] = "@ind_str_asc"}
[](#cb167-2) {a[$2]=$0} END{for(k in a) print a[k]}' table.txt
[](#cb167-3)yellow banana window shoes 3.14
[](#cb167-4)brown bread mat hair 42
[](#cb167-5)blue cake mug shirt -7
```

## split

The `split` function provides the same features as the record splitting done using `FS`. This is helpful when you need the results as an array for some reason, for example to use array sorting features. Or, when you need to further split a field content. `split` accepts four arguments, the last two being optional.

*   First argument is the string to be split
*   Second argument is the array variable to save results
*   Third argument is the separator, whose default is `FS`

The return value of `split` function is number of fields, similar to `NF` variable. The array gets indexed starting from `1` for first element, `2` for second element and so on. If the array already had some value, it gets overwritten with the new value.

```
[](#cb168-1)$ # same as: awk '{print $2}'
[](#cb168-2)$ printf '     one \t two\t\t\tthree  ' | awk '{split($0, a); print a[2]}'
[](#cb168-3)two
[](#cb168-4)
[](#cb168-5)$ # example with both FS and split in action
[](#cb168-6)$ s='Joe,1996-10-25,64,78'
[](#cb168-7)$ echo "$s" | awk -F, '{split($2, d, "-"); print $1 " was born in " d[1]}'
[](#cb168-8)Joe was born in 1996
[](#cb168-9)
[](#cb168-10)$ # single row to multiple rows based on splitting last field
[](#cb168-11)$ s='air,water,12:42:3'
[](#cb168-12)$ echo "$s" | awk -F, '{n=split($NF, a, ":");
[](#cb168-13) for(i=1; i<=n; i++) print $1, $2, a[i]}'
[](#cb168-14)air water 12
[](#cb168-15)air water 42
[](#cb168-16)air water 3
```

Similar to `FS`, you can use regular expression as a separator.

```
[](#cb169-1)$ s='Sample123string42with777numbers'
[](#cb169-2)$ echo "$s" | awk '{split($0, s, /[0-9]+/); print s[2], s[4]}'
[](#cb169-3)string numbers
```

The fourth argument provides a feature not present with `FS` splitting. It allows you to save the portions matched by the separator in an array. Quoting from [gawk manual: split()](https://www.gnu.org/software/gawk/manual/gawk.html#index-split_0028_0029-function-1):

> If `fieldsep` is a single space, then any leading whitespace goes into `seps[0]` and any trailing whitespace goes into `seps[n]`, where `n` is the return value of `split()` (i.e., the number of elements in `array`).

```
[](#cb170-1)$ s='Sample123string42with777numbers'
[](#cb170-2)$ echo "$s" | awk '{n=split($0, s, /[0-9]+/, seps);
[](#cb170-3) for(i=1; i<n; i++) print seps[i]}'
[](#cb170-4)123
[](#cb170-5)42
[](#cb170-6)777
```

Here's an example where `split` is merely used to initialize an array based on empty separator. Unlike `$N` syntax where an expression resulting in floating-point number is acceptable, array index has to be an integer. Hence, `int` function is used to convert floating-point result to integer in the example below.

```
[](#cb171-1)$ cat marks.txt
[](#cb171-2)Dept    Name    Marks
[](#cb171-3)ECE     Raj     53
[](#cb171-4)ECE     Joel    72
[](#cb171-5)EEE     Moi     68
[](#cb171-6)CSE     Surya   81
[](#cb171-7)EEE     Tia     59
[](#cb171-8)ECE     Om      92
[](#cb171-9)CSE     Amy     67
[](#cb171-10)
[](#cb171-11)$ # adds a new grade column based on marks in 3rd column
[](#cb171-12)$ awk 'BEGIN{OFS="\t"; split("DCBAS", g, //)}
[](#cb171-13) {$(NF+1) = NR==1 ? "Grade" : g[int($NF/10)-4]} 1' marks.txt
[](#cb171-14)Dept    Name    Marks   Grade
[](#cb171-15)ECE     Raj     53      D
[](#cb171-16)ECE     Joel    72      B
[](#cb171-17)EEE     Moi     68      C
[](#cb171-18)CSE     Surya   81      A
[](#cb171-19)EEE     Tia     59      D
[](#cb171-20)ECE     Om      92      S
[](#cb171-21)CSE     Amy     67      C
```

## patsplit

The `patsplit` function will give you the features provided by `FPAT`. The argument order and optional arguments is same as the `split` function, with `FPAT` as the default separator. The return value is number of fields obtained from the split.

```
[](#cb172-1)$ s='eagle,"fox,42",bee,frog'
[](#cb172-2)
[](#cb172-3)$ echo "$s" | awk '{patsplit($0, a, /"[^"]*"|[^,]*/); print a[2]}'
[](#cb172-4)"fox,42"
```

## substr

The `substr` function allows to extract specified number of characters from given string based on indexing. The argument order is:

*   First argument is the input string
*   Second argument is starting position
*   Third argument is number of characters to extract

The index starts from `1`. If the third argument is not specified, by default all characters until the end of string input is extracted. If the second argument is greater than length of the string or if third argument is less than or equal to `0` then empty string is returned. Second argument will use `1` if a number less than one is specified.

```
[](#cb173-1)$ echo 'abcdefghij' | awk '{print substr($0, 1, 5)}'
[](#cb173-2)abcde
[](#cb173-3)$ echo 'abcdefghij' | awk '{print substr($0, 4, 3)}'
[](#cb173-4)def
[](#cb173-5)
[](#cb173-6)$ echo 'abcdefghij' | awk '{print substr($0, 6)}'
[](#cb173-7)fghij
[](#cb173-8)
[](#cb173-9)$ echo 'abcdefghij' | awk -v OFS=: '{print substr($0, 2, 3), substr($0, 6, 3)}'
[](#cb173-10)bcd:fgh
```

If only a few characters are needed from input record, can also use empty `FS`.

```
[](#cb174-1)$ echo 'abcdefghij' | awk -v FS= '{print $3}'
[](#cb174-2)c
[](#cb174-3)$ echo 'abcdefghij' | awk -v FS= '{print $3, $5}'
[](#cb174-4)c e
```

## match

The `match` function is useful to extract portion of an input string matched by a regexp. There are two ways to get the matched portion:

*   by using `substr` function along with special variables `RSTART` and `RLENGTH`
*   by passing a third argument to `match` so that the results are available from an array

The first argument to `match` is the input string and second is the regexp. If the match fails, then `RSTART` gets `0` and `RLENGTH` gets `-1`. Return value is same as `RSTART`.

```
[](#cb175-1)$ s='051 035 154 12 26 98234'
[](#cb175-2)
[](#cb175-3)$ # using substr and RSTART/RLENGTH
[](#cb175-4)$ echo "$s" | awk 'match($0, /[0-9]{4,}/){print substr($0, RSTART, RLENGTH)}'
[](#cb175-5)98234
[](#cb175-6)
[](#cb175-7)$ # using array, note that index 0 is used here, not 1
[](#cb175-8)$ echo "$s" | awk 'match($0, /0*[1-9][0-9]{2,}/, m){print m[0]}'
[](#cb175-9)154
```

Both the above examples can also be easily solved using `FPAT` or `patsplit`. `match` has an advantage when it comes to getting portions matched only within capture groups. The first element of array will still have the entire match. Second element will contain portion matched by first group, third element will contain portion matched by second group and so on. See also [stackoverflow: arithmetic replacement in a text file](https://stackoverflow.com/q/62241101/4082052).

```
[](#cb176-1)$ # entire matched portion
[](#cb176-2)$ echo 'foo=42, baz=314' | awk 'match($0, /baz=([0-9]+)/, m){print m[0]}'
[](#cb176-3)baz=314
[](#cb176-4)$ # matched portion of first capture group
[](#cb176-5)$ echo 'foo=42, baz=314' | awk 'match($0, /baz=([0-9]+)/, m){print m[1]}'
[](#cb176-6)314
```

If you need to get matching portions for all the matches instead of just the first match, you can use a loop and adjust the input string every iteration.

```
[](#cb177-1)$ # extract numbers only if it is followed by a comma
[](#cb177-2)$ s='42 foo-5, baz3; x-83, y-20: f12'
[](#cb177-3)$ echo "$s" | awk '{ while( match($0, /([0-9]+),/, m) ){print m[1];
[](#cb177-4) $0=substr($0, RSTART+RLENGTH)} }'
[](#cb177-5)5
[](#cb177-6)83
```

## index

The `index` function is useful when you need to match a string literally in the given input string. This is similar to `grep -F` functionality of matching fixed strings. The first argument to this function is the input string and the second is the string to be matched literally. The return value is the index of matching location and `0` if there is no match.

```
[](#cb178-1)$ cat eqns.txt
[](#cb178-2)a=b,a-b=c,c*d
[](#cb178-3)a+b,pi=3.14,5e12
[](#cb178-4)i*(t+9-g)/8,4-a+b
[](#cb178-5)
[](#cb178-6)$ # no output because the metacharacters aren't escaped
[](#cb178-7)$ awk '/i*(t+9-g)/' eqns.txt
[](#cb178-8)$ # same as: grep -F 'i*(t+9-g)' eqns.txt
[](#cb178-9)$ awk 'index($0, "i*(t+9-g)")' eqns.txt
[](#cb178-10)i*(t+9-g)/8,4-a+b
[](#cb178-11)
[](#cb178-12)$ # check only the last field
[](#cb178-13)$ awk -F, 'index($NF, "a+b")' eqns.txt
[](#cb178-14)i*(t+9-g)/8,4-a+b
[](#cb178-15)$ # index not needed if entire field/line is being compared
[](#cb178-16)$ awk -F, '$1=="a+b"' eqns.txt
[](#cb178-17)a+b,pi=3.14,5e12
```

The return value is also useful to ensure match is found at specific positions only. For example start or end of input string.

```
[](#cb179-1)$ # start of string
[](#cb179-2)$ awk 'index($0, "a+b")==1' eqns.txt
[](#cb179-3)a+b,pi=3.14,5e12
[](#cb179-4)$ # end of string
[](#cb179-5)$ awk -v s="a+b" 'index($0, s)==length()-length(s)+1' eqns.txt
[](#cb179-6)i*(t+9-g)/8,4-a+b
```

Recall that `-v` option gets parsed by `awk`'s string processing rules. So, if you need to pass a literal string without falling in backslash hell, use `ENVIRON` instead of `-v` option.

```
[](#cb180-1)$ echo 'a\b\c\d' | awk -v s='a\b' 'index($0, s)'
[](#cb180-2)$ echo 'a\b\c\d' | awk -v s='a\\b' 'index($0, s)'
[](#cb180-3)a\b\c\d
[](#cb180-4)$ echo 'a\b\c\d' | s='a\b' awk 'index($0, ENVIRON["s"])'
[](#cb180-5)a\b\c\d
```

## system

External commands can be issued using the `system` function. Any output generated by the external command would be as usual on `stdout` unless redirected while calling the command.

```
[](#cb181-1)$ awk 'BEGIN{system("echo Hello World")}'
[](#cb181-2)Hello World
[](#cb181-3)
[](#cb181-4)$ wc table.txt
[](#cb181-5) 3 15 79 table.txt
[](#cb181-6)$ awk 'BEGIN{system("wc table.txt")}'
[](#cb181-7) 3 15 79 table.txt
[](#cb181-8)
[](#cb181-9)$ awk 'BEGIN{system("seq 10 | paste -sd, > out.txt")}'
[](#cb181-10)$ cat out.txt
[](#cb181-11)1,2,3,4,5,6,7,8,9,10
[](#cb181-12)
[](#cb181-13)$ cat t2.txt
[](#cb181-14)I bought two balls and 3 bats
[](#cb181-15)$ echo 'f1,t2,f3' | awk -F, '{system("cat " $2 ".txt")}'
[](#cb181-16)I bought two balls and 3 bats
```

Return value of `system` depends on `exit` status of the executed command. See [gawk manual: Input/Output Functions](https://www.gnu.org/software/gawk/manual/html_node/I_002fO-Functions.html) for details.

```
[](#cb182-1)$ ls xyz.txt
[](#cb182-2)ls: cannot access 'xyz.txt': No such file or directory
[](#cb182-3)$ echo $?
[](#cb182-4)2
[](#cb182-5)
[](#cb182-6)$ awk 'BEGIN{s=system("ls xyz.txt"); print "Exit status: " s}'
[](#cb182-7)ls: cannot access 'xyz.txt': No such file or directory
[](#cb182-8)Exit status: 2
```

## printf and sprintf

The `printf` function is useful over `print` function when you need to format the data before printing. Another difference is that `OFS` and `ORS` do not affect the `printf` function. The features are similar to those found in `C` programming language and the shell built-in command.

```
[](#cb183-1)$ # OFMT controls the formatting for numbers displayed with print function
[](#cb183-2)$ awk 'BEGIN{print OFMT}'
[](#cb183-3)%.6g
[](#cb183-4)$ awk 'BEGIN{sum = 3.1428 + 100; print sum}'
[](#cb183-5)103.143
[](#cb183-6)$ awk 'BEGIN{OFMT="%.5f"; sum = 3.1428 + 100; print sum}'
[](#cb183-7)103.14280
[](#cb183-8)
[](#cb183-9)$ # using printf function
[](#cb183-10)$ # note the use of \n as ORS isn't appended unlike print
[](#cb183-11)$ awk 'BEGIN{sum = 3.1428 + 10; printf "%f\n", sum}'
[](#cb183-12)13.142800
[](#cb183-13)$ awk 'BEGIN{sum = 3.1428 + 10; printf "%.3f\n", sum}'
[](#cb183-14)13.143
```

Here's some more formatting options for floating-point numbers.

```
[](#cb184-1)$ # total length is 10, filled with space if needed
[](#cb184-2)$ # [ and ] are used here for visualization purposes
[](#cb184-3)$ awk 'BEGIN{pi = 3.14159; printf "[%10.3f]\n", pi}'
[](#cb184-4)[     3.142]
[](#cb184-5)$ awk 'BEGIN{pi = 3.14159; printf "[%-10.3f]\n", pi}'
[](#cb184-6)[3.142     ]
[](#cb184-7)
[](#cb184-8)$ # zero filled
[](#cb184-9)$ awk 'BEGIN{pi = 3.14159; printf "%010.3f\n", pi}'
[](#cb184-10)000003.142
[](#cb184-11)
[](#cb184-12)$ # scientific notation
[](#cb184-13)$ awk 'BEGIN{pi = 3.14159; printf "%e\n", pi}'
[](#cb184-14)3.141590e+00
```

Here's some formatting options for integers.

```
[](#cb185-1)$ # note that there is no rounding
[](#cb185-2)$ awk 'BEGIN{printf "%d\n", 1.99}'
[](#cb185-3)1
[](#cb185-4)
[](#cb185-5)$ # ensure there's always a sign prefixed to integer
[](#cb185-6)$ awk 'BEGIN{printf "%+d\n", 100}'
[](#cb185-7)+100
[](#cb185-8)$ awk 'BEGIN{printf "%+d\n", -100}'
[](#cb185-9)-100
```

Here's some formatting options for strings.

```
[](#cb186-1)$ # prefix remaining width with spaces
[](#cb186-2)$ awk 'BEGIN{printf "|%10s|\n", "mango"}'
[](#cb186-3)|     mango|
[](#cb186-4)
[](#cb186-5)$ # suffix remaining width with spaces
[](#cb186-6)$ awk 'BEGIN{printf "|%-10s|\n", "mango"}'
[](#cb186-7)|mango     |
[](#cb186-8)
[](#cb186-9)$ # truncate
[](#cb186-10)$ awk '{printf "%.4s\n", $0}' table.txt
[](#cb186-11)brow
[](#cb186-12)blue
[](#cb186-13)yell
```

You can also refer to an argument using `N$` format, where `N` is the positional number of argument. One advantage with this method is that you can reuse an argument any number of times. You cannot mix this format with the normal way.

```
[](#cb187-1)$ awk 'BEGIN{printf "%1$d + %2$d * %1$d = %3$d\n", 3, 4, 15}'
[](#cb187-2)3 + 4 * 3 = 15
[](#cb187-3)$ # remove # if you do not need the prefix
[](#cb187-4)$ awk 'BEGIN{printf "hex=%1$#x\noct=%1$#o\ndec=%1$d\n", 15}'
[](#cb187-5)hex=0xf
[](#cb187-6)oct=017
[](#cb187-7)dec=15
```

You can pass variables by specifying a `*` instead of a number in the formatting string.

```
[](#cb188-1)$ # same as: awk 'BEGIN{pi = 3.14159; printf "%010.3f\n",  pi}'
[](#cb188-2)$ awk 'BEGIN{d=10; p=3; pi = 3.14159; printf "%0*.*f\n", d, p, pi}'
[](#cb188-3)000003.142
```

> ![warning](media/file1.svg) Passing a variable directly to `printf` without using a format specifier can result in error depending upon the contents of the variable.

```
[](#cb189-1)$ awk 'BEGIN{s="solve: 5 % x = 1"; printf s}'
[](#cb189-2)awk: cmd. line:1: fatal: not enough arguments to satisfy format string
[](#cb189-3)    `solve: 5 % x = 1'
[](#cb189-4) ^ ran out for this one
```

So, as a good practice, always use variables with appropriate format instead of passing it directly to `printf`.

```
[](#cb190-1)$ awk 'BEGIN{s="solve: 5 % x = 1"; printf "%s\n", s}'
[](#cb190-2)solve: 5 % x = 1
```

If `%` has to be used literally inside the format specifier, use `%%`. This is similar to using `\\` in regexp to represent `\` literally.

```
[](#cb191-1)$ awk 'BEGIN{printf "n%%d gives the remainder\n"}'
[](#cb191-2)n%d gives the remainder
```

To save the results of the formatting in a variable instead of printing, use `sprintf` function. Unlike `printf`, parentheses are always required to use `sprintf` function.

```
[](#cb192-1)$ awk 'BEGIN{pi = 3.14159; s = sprintf("%010.3f", pi); print s}'
[](#cb192-2)000003.142
```

> ![info](media/file0.svg) See [gawk manual: printf](https://www.gnu.org/software/gawk/manual/html_node/Printf.html) for complete list of formatting options and other details.

## Redirecting print output

The results from `print` and `printf` functions can be redirected to a shell command or a file instead of `stdout`. There's nothing special about it, you could have done it normally on `awk` command as well. The use case arises when you need to redirect only a specific portion or if you need multiple redirections within the same `awk` command. Here's some examples of redirecting to multiple files.

```
[](#cb193-1)$ seq 6 | awk 'NR%2{print > "odd.txt"; next} {print > "even.txt"}'
[](#cb193-2)$ cat odd.txt
[](#cb193-3)1
[](#cb193-4)3
[](#cb193-5)5
[](#cb193-6)$ cat even.txt
[](#cb193-7)2
[](#cb193-8)4
[](#cb193-9)6
[](#cb193-10)
[](#cb193-11)$ # dynamically creating filenames
[](#cb193-12)$ awk -v OFS='\t' 'NR>1{print $2, $3 > $1".txt"}' marks.txt
[](#cb193-13)$ # output for one of the departments
[](#cb193-14)$ cat ECE.txt
[](#cb193-15)Raj     53
[](#cb193-16)Joel    72
[](#cb193-17)Om      92
```

Note that the use of `>` doesn't mean that the file will get overwritten everytime. That happens only once if the file already existed prior to executing the `awk` command. Use `>>` if you wish to append to already existing files.

As seen in above examples, the file names are passed as string expressions. To redirect to a shell command, again you need to pass a string expression after `|` pipe symbol. Here's an example.

```
[](#cb194-1)$ awk '{print $2 | "paste -sd,"}' table.txt
[](#cb194-2)bread,cake,banana
```

And here's some examples of multiple redirections.

```
[](#cb195-1)$ awk '{print $2 | "sort | paste -sd,"}' table.txt
[](#cb195-2)banana,bread,cake
[](#cb195-3)
[](#cb195-4)$ # sort the output before writing to files
[](#cb195-5)$ awk -v OFS='\t' 'NR>1{print $2, $3 | "sort > "$1".txt"}' marks.txt
[](#cb195-6)$ # output for one of the departments
[](#cb195-7)$ cat ECE.txt
[](#cb195-8)Joel    72
[](#cb195-9)Om      92
[](#cb195-10)Raj     53
```

> ![info](media/file0.svg) See [gawk manual: Redirecting Output of print and printf](https://www.gnu.org/software/gawk/manual/gawk.html#Redirection) for more details and operators on redirections. And see [gawk manual: Closing Input and Output Redirections](https://www.gnu.org/software/gawk/manual/gawk.html#Close-Files-And-Pipes) if you have too many redirections.

## Summary

This chapter covered some of the built-in functions provided by `awk`. Do check the manual for more of them, for example math and time related functions.

Next chapter will cover features related to processing multiple files passed as input to `awk`.

## Exercises

> ![info](media/file0.svg) Exercises will also include functions and features not discussed in this chapter. Refer to [gawk manual: Functions](https://www.gnu.org/software/gawk/manual/gawk.html#Functions) for details.

**a)** For the input file `scores.csv`, sort the rows based on **Physics** values in descending order. Header should be retained as the first line in output.

```
[](#cb196-1)$ awk ##### add your solution here
[](#cb196-2)Name,Maths,Physics,Chemistry
[](#cb196-3)Ith,100,100,100
[](#cb196-4)Cy,97,98,95
[](#cb196-5)Lin,78,83,80
[](#cb196-6)Er,56,79,92
[](#cb196-7)Ort,68,72,66
[](#cb196-8)Blue,67,46,99
```

**b)** For the input file `nums3.txt`, calculate the square root of numbers and display in two different formats. First with four digits after fractional point and next in scientific notation, again with four digits after fractional point. Assume input has only single column positive numbers.

```
[](#cb197-1)$ awk ##### add your solution here
[](#cb197-2)1.7720
[](#cb197-3)64.8151
[](#cb197-4)27.8747
[](#cb197-5)568.3414
[](#cb197-6)
[](#cb197-7)$ awk ##### add your solution here
[](#cb197-8)1.7720e+00
[](#cb197-9)6.4815e+01
[](#cb197-10)2.7875e+01
[](#cb197-11)5.6834e+02
```

**c)** Transform the given input strings to the corresponding output shown. Assume space as the field separators. From the second field, remove the second `:` and the number that follows. Modify the last field by multiplying it by the number that was deleted from the second field. The numbers can be positive/negative integers or floating-point numbers (including scientific notation).

```
[](#cb198-1)$ echo 'go x:12:-425 og 6.2' | awk ##### add your solution here
[](#cb198-2)go x:12 og -2635
[](#cb198-3)
[](#cb198-4)$ echo 'rx zwt:3.64:12.89e2 ljg 5' | awk ##### add your solution here
[](#cb198-5)rx zwt:3.64 ljg 6445
```

**d)** Transform the given input strings to the corresponding output shown. Assume space as the field separators. Replace the second field with sum of the two numbers embedded in it. The numbers can be positive/negative integers or floating-point numbers (but not scientific notation).

```
[](#cb199-1)$ echo 'f2:z3 kt//-42\\3.14//tw 5y6' | awk ##### add your solution here
[](#cb199-2)f2:z3 -38.86 5y6
[](#cb199-3)
[](#cb199-4)$ echo 't5:x7 qr;wq<=>+10{-8764.124}yb u9' | awk ##### add your solution here
[](#cb199-5)t5:x7 -8754.12 u9
```

**e)** For the given input strings, extract portion of the line starting from the matching location specified by shell variable `s` till the end of the line. If there is no match, do not print that line. The contents of `s` should be matched literally.

```
[](#cb200-1)$ s='(a^b)'
[](#cb200-2)$ echo '3*f + (a^b) - 45' | ##### add your solution here
[](#cb200-3)(a^b) - 45
[](#cb200-4)
[](#cb200-5)$ s='\&/'
[](#cb200-6)$ # should be no output for this input
[](#cb200-7)$ echo 'f\&z\&2.14' | ##### add your solution here
[](#cb200-8)$ # but this one has a match
[](#cb200-9)$ echo 'f\&z\&/2.14' | ##### add your solution here
[](#cb200-10)\&/2.14
```

**f)** Extract all positive integers preceded by `-` and followed by `:` or `;` and display all such matches separated by a newline character.

```
[](#cb201-1)$ s='42 foo-5; baz3; x-83, y-20:-34; f12'
[](#cb201-2)$ echo "$s" | awk ##### add your solution here
[](#cb201-3)5
[](#cb201-4)20
[](#cb201-5)34
```

**g)** For the input file `scores.csv`, calculate the average of three marks for each `Name`. Those with average greater than or equal to `80` should be saved in `pass.csv` and the rest in `fail.csv`. The format is `Name` and average score (up to two decimal points) separated by a tab character.

```
[](#cb202-1)$ awk ##### add your solution here
[](#cb202-2)
[](#cb202-3)$ cat fail.csv
[](#cb202-4)Blue    70.67
[](#cb202-5)Er      75.67
[](#cb202-6)Ort     68.67
[](#cb202-7)$ cat pass.csv
[](#cb202-8)Lin     80.33
[](#cb202-9)Cy      96.67
[](#cb202-10)Ith     100.00
```

**h)** For the input file `files.txt`, replace lines starting with a space with the output of that line executed as a shell command.

```
[](#cb203-1)$ cat files.txt
[](#cb203-2) sed -n '2p' addr.txt
[](#cb203-3)-----------
[](#cb203-4) wc -w sample.txt
[](#cb203-5)===========
[](#cb203-6) awk '{print $1}' table.txt
[](#cb203-7)-----------
[](#cb203-8)
[](#cb203-9)$ awk ##### add your solution here
[](#cb203-10)How are you
[](#cb203-11)-----------
[](#cb203-12)31 sample.txt
[](#cb203-13)===========
[](#cb203-14)brown
[](#cb203-15)blue
[](#cb203-16)yellow
[](#cb203-17)-----------
```

**i)** For the input file `fw.txt`, format the last column of numbers in scientific notation with two digits after the decimal point.

```
[](#cb204-1)$ awk ##### add your solution here
[](#cb204-2)1.3  rs   90  1.35e-01
[](#cb204-3)3.8           6.00e+00
[](#cb204-4)5.2  ye       8.24e+00
[](#cb204-5)4.2  kt   32  4.51e+01
```

**j)** For the input file `addr.txt`, display all lines containing `e` or `u` but not both.

> ![info](media/file0.svg) Hint — [gawk manual: Bit-Manipulation Functions](https://www.gnu.org/software/gawk/manual/gawk.html#Bitwise-Functions).

```
[](#cb205-1)$ awk ##### add your solution here
[](#cb205-2)Hello World
[](#cb205-3)This game is good
[](#cb205-4)Today is sunny
```

# Multiple file input

You have already seen control structures like `BEGIN`, `END` and `next`. This chapter will discuss control structures that are useful to make decisions around each file when there are multiple files passed as input.

## BEGINFILE, ENDFILE and FILENAME

*   `BEGINFILE` — this block gets executed before start of each input file
*   `ENDFILE` — this block gets executed after processing each input file
*   `FILENAME` — special variable having file name of current input file

```
[](#cb206-1)$ awk 'BEGINFILE{print "--- " FILENAME " ---"} 1' greeting.txt table.txt
[](#cb206-2)--- greeting.txt ---
[](#cb206-3)Hi there
[](#cb206-4)Have a nice day
[](#cb206-5)Good bye
[](#cb206-6)--- table.txt ---
[](#cb206-7)brown bread mat hair 42
[](#cb206-8)blue cake mug shirt -7
[](#cb206-9)yellow banana window shoes 3.14
[](#cb206-10)
[](#cb206-11)$ # same as: tail -q -n1 greeting.txt table.txt
[](#cb206-12)$ awk 'ENDFILE{print $0}' greeting.txt table.txt
[](#cb206-13)Good bye
[](#cb206-14)yellow banana window shoes 3.14
```

## nextfile

`nextfile` will skip remaining records from current file being processed and move on to the next file.

```
[](#cb207-1)$ # print filename if it contains 'I' anywhere in the file
[](#cb207-2)$ # same as: grep -l 'I' f[1-3].txt greeting.txt
[](#cb207-3)$ awk '/I/{print FILENAME; nextfile}' f[1-3].txt greeting.txt
[](#cb207-4)f1.txt
[](#cb207-5)f2.txt
[](#cb207-6)
[](#cb207-7)$ # print filename if it contains both 'o' and 'at' anywhere in the file
[](#cb207-8)$ awk 'BEGINFILE{m1=m2=0} /o/{m1=1} /at/{m2=1}
[](#cb207-9) m1 && m2{print FILENAME; nextfile}' f[1-3].txt greeting.txt
[](#cb207-10)f2.txt
[](#cb207-11)f3.txt
```

> ![warning](media/file1.svg) `nextfile` cannot be used in `BEGIN` or `END` or `ENDFILE` blocks. See [gawk manual: nextfile](https://www.gnu.org/software/gawk/manual/gawk.html#Nextfile-Statement) for more details, how it affects `ENDFILE` and other special cases.

## ARGC and ARGV

The `ARGC` special variable contains total number of arguments passed to the `awk` command, including `awk` itself as an argument. The `ARGV` special array contains the arguments themselves.

```
[](#cb208-1)$ # note that index starts with '0' here
[](#cb208-2)$ awk 'BEGIN{for(i=0; i<ARGC; i++) print ARGV[i]}' f[1-3].txt greeting.txt
[](#cb208-3)awk
[](#cb208-4)f1.txt
[](#cb208-5)f2.txt
[](#cb208-6)f3.txt
[](#cb208-7)greeting.txt
```

Similar to manipulating `NF` and modifying `$N` field contents, you can change the values of `ARGC` and `ARGV` to control how the arguments should be processed.

However, not all arguments are necessarily filenames. `awk` allows assigning variable values without `-v` option if it is done in the place where you usually provide file arguments. For example:

```
[](#cb209-1)$ awk 'BEGIN{for(i=0; i<ARGC; i++) print ARGV[i]}' table.txt n=5 greeting.txt
[](#cb209-2)awk
[](#cb209-3)table.txt
[](#cb209-4)n=5
[](#cb209-5)greeting.txt
```

In the above example, the variable `n` will get a value of `5` after `awk` has finished processing `table.txt` file. Here's an example where `FS` is changed between two files.

```
[](#cb210-1)$ cat table.txt
[](#cb210-2)brown bread mat hair 42
[](#cb210-3)blue cake mug shirt -7
[](#cb210-4)yellow banana window shoes 3.14
[](#cb210-5)$ cat books.csv
[](#cb210-6)Harry Potter,Mistborn,To Kill a Mocking Bird
[](#cb210-7)Matilda,Castle Hangnail,Jane Eyre
[](#cb210-8)
[](#cb210-9)$ # for table.txt, FS will be default value
[](#cb210-10)$ # for books.csv, FS will be comma character
[](#cb210-11)$ # OFS is comma for both files
[](#cb210-12)$ awk -v OFS=, 'NF=2' table.txt FS=, books.csv
[](#cb210-13)brown,bread
[](#cb210-14)blue,cake
[](#cb210-15)yellow,banana
[](#cb210-16)Harry Potter,Mistborn
[](#cb210-17)Matilda,Castle Hangnail
```

> ![info](media/file0.svg) See [stackoverflow: extract positions 2-7 from a fasta sequence](https://stackoverflow.com/a/64427745/4082052) for a practical example of changing field/record separators between the files being processed.

## Summary

This chapter introduced few more special blocks and variables are that handy for processing multiple file inputs. These will show up in examples in coming chapters as well.

Next chapter will discuss use cases where you need to take decisions based on multiple input records.

## Exercises

**a)** Print the last field of first two lines for the input files `table.txt`, `scores.csv` and `fw.txt`. The field separators for these files are space, comma and fixed width respectively. To make the output more informative, print filenames and a separator as shown in the output below. Assume input files will have at least two lines.

```
[](#cb211-1)$ awk ##### add your solution here
[](#cb211-2)>table.txt<
[](#cb211-3)42
[](#cb211-4)-7
[](#cb211-5)----------
[](#cb211-6)>scores.csv<
[](#cb211-7)Chemistry
[](#cb211-8)99
[](#cb211-9)----------
[](#cb211-10)>fw.txt<
[](#cb211-11)0.134563
[](#cb211-12)6
[](#cb211-13)----------
```

**b)** For the given list of input files, display all filenames that contain `at` or `fun` in the third field. Assume space as the field separator.

```
[](#cb212-1)$ awk ##### add your solution here sample.txt secrets.txt addr.txt table.txt
[](#cb212-2)secrets.txt
[](#cb212-3)addr.txt
[](#cb212-4)table.txt
```

# Processing multiple records

Often, you need to consider multiple lines at a time to make a decision, such as the paragraph mode examples seen earlier. Sometimes, you need to match a particular record and then get records surrounding the matched record. The `condX{actionX}` shortcut makes it easy to code state machines concisely, which is useful to solve such multiple record use cases. See [softwareengineering: FSM examples](https://softwareengineering.stackexchange.com/questions/47806/examples-of-finite-state-machines) if you are not familiar with state machines.

## Processing consecutive records

You might need to define a condition that should satisfy something for one record and something else for the very next record. `awk` does provide a feature to get next record, but that could get complicated (see [getline](#ch013.xhtml_getline) section). Instead, you can simply save each record in a variable and then create the required conditional expression. The default behavior of uninitialized variable to act as `0` in numerical context and empty in string context plays a role too.

```
[](#cb213-1)$ # match and print two consecutive records
[](#cb213-2)$ # first record should contain 'as' and second record should contain 'not'
[](#cb213-3)$ awk 'p ~ /as/ && /not/{print p ORS $0} {p=$0}' programming_quotes.txt
[](#cb213-4)Therefore, if you write the code as cleverly as possible, you are,
[](#cb213-5)by definition, not smart enough to debug it by Brian W. Kernighan
[](#cb213-6)
[](#cb213-7)$ # same filtering as above, but print only the first record
[](#cb213-8)$ awk 'p ~ /as/ && /not/{print p} {p=$0}' programming_quotes.txt
[](#cb213-9)Therefore, if you write the code as cleverly as possible, you are,
[](#cb213-10)
[](#cb213-11)$ # same filtering as above, but print only the second record
[](#cb213-12)$ awk 'p ~ /as/ && /not/; {p=$0}' programming_quotes.txt
[](#cb213-13)by definition, not smart enough to debug it by Brian W. Kernighan
```

## Context matching

Sometimes you want not just the matching records, but the records relative to the matches as well. For example, it could be to see the comments at start of a function block that was matched while searching a program file. Or, it could be to see extended information from a log file while searching for a particular error message.

Consider this sample input file:

```
[](#cb214-1)$ cat context.txt
[](#cb214-2)blue
[](#cb214-3)    toy
[](#cb214-4)    flower
[](#cb214-5)    sand stone
[](#cb214-6)light blue
[](#cb214-7)    flower
[](#cb214-8)    sky
[](#cb214-9)    water
[](#cb214-10)language
[](#cb214-11)    english
[](#cb214-12)    hindi
[](#cb214-13)    spanish
[](#cb214-14)    tamil
[](#cb214-15)programming language
[](#cb214-16)    python
[](#cb214-17)    kotlin
[](#cb214-18)    ruby
```

**Case 1:** Here's an example that emulates `grep --no-group-separator -A<n>` functionality. The `n && n--` trick used in the example works like this:

*   If initially `n=2`, then we get
    *   `2 && 2` --> evaluates to `true` and `n` becomes `1`
    *   `1 && 1` --> evaluates to `true` and `n` becomes `0`
    *   `0 &&` --> evaluates to `false` and `n` doesn't change
*   Note that when conditionals are connected with logical `&&`, the second expression will not be executed at all if the first one turns out to be `false` because the overall result will always be `false`. Same is the case if the first expression evaluates to `true` with logical `||` operator. Such logical operators are also known as **short-circuit** operators. Thus, in the above case, `n--` won't be executed when `n` is `0` on the left hand side. This prevents `n` going negative and `n && n--` will never become `true` unless `n` is assigned again.

```
[](#cb215-1)$ # same as: grep --no-group-separator -A1 'blue'
[](#cb215-2)$ # print matching line as well as the one that follows it
[](#cb215-3)$ awk '/blue/{n=2} n && n--' context.txt
[](#cb215-4)blue
[](#cb215-5)    toy
[](#cb215-6)light blue
[](#cb215-7)    flower
[](#cb215-8)
[](#cb215-9)$ # overlapping example, n gets re-assigned before reaching 0
[](#cb215-10)$ awk '/toy|flower/{n=2} n && n--{print NR, $0}' context.txt
[](#cb215-11)2     toy
[](#cb215-12)3     flower
[](#cb215-13)4     sand stone
[](#cb215-14)6     flower
[](#cb215-15)7     sky
[](#cb215-16)
[](#cb215-17)$ # doesn't allow overlapping cases to re-assign the counter
[](#cb215-18)$ awk '!n && /toy|flower/{n=2} n && n--{print NR, $0}' context.txt
[](#cb215-19)2     toy
[](#cb215-20)3     flower
[](#cb215-21)6     flower
[](#cb215-22)7     sky
```

Once you've understood the above examples, the rest of the examples in this section should be easier to comprehend. They are all variations of the logic used above and re-arranged to solve the use case being discussed.

**Case 2:** Print `n` records after match. This is similar to previous case, except that the matching record isn't printed.

```
[](#cb216-1)$ # print 1 line after matching line
[](#cb216-2)$ # for overlapping cases, n gets re-assigned before reaching 0
[](#cb216-3)$ awk 'n && n--; /language/{n=1}' context.txt
[](#cb216-4)    english
[](#cb216-5)    python
[](#cb216-6)
[](#cb216-7)$ # print 2 lines after matching line
[](#cb216-8)$ # doesn't allow overlapping cases to re-assign the counter
[](#cb216-9)$ awk '!n && /toy|flower/{n=2; next} n && n--' context.txt
[](#cb216-10)    flower
[](#cb216-11)    sand stone
[](#cb216-12)    sky
[](#cb216-13)    water
```

**Case 3:** Here's how to print `n`th record after the matching record.

```
[](#cb217-1)$ # print only the 2nd line found after matching line
[](#cb217-2)$ # the array saves matching result for each record
[](#cb217-3)$ # doesn't rely on a counter, thus works for overlapping cases
[](#cb217-4)$ awk -v n=2 'a[NR-n]; /toy|flower/{a[NR]=1}' context.txt
[](#cb217-5)    sand stone
[](#cb217-6)light blue
[](#cb217-7)    water
[](#cb217-8)
[](#cb217-9)$ # print only the 3rd line found after matching line
[](#cb217-10)$ # n && !--n will be true only when --n yields 0
[](#cb217-11)$ # overlapping cases won't work as n gets re-assigned before going to 0
[](#cb217-12)$ awk 'n && !--n; /language/{n=3}' context.txt
[](#cb217-13)    spanish
[](#cb217-14)    ruby
```

**Case 4:** Print `n` records before match. Printing the matching record as well is left as an exercise. Since the file is being read in forward direction, and the problem statement is to print something before the matching record, overlapping situation like the previous examples doesn't occur.

```
[](#cb218-1)$ # i>0 is used because NR starts from 1
[](#cb218-2)$ awk -v n=2 '/toy|flower/{for(i=NR-n; i<NR; i++) if(i>0) print a[i]}
[](#cb218-3) {a[NR]=$0}' context.txt
[](#cb218-4)blue
[](#cb218-5)blue
[](#cb218-6)    toy
[](#cb218-7)    sand stone
[](#cb218-8)light blue
```

**Case 5:** Print `n`th record before the matching record.

```
[](#cb219-1)$ # if the count is small enough, you can save them in variables
[](#cb219-2)$ # this one prints 2nd line before the matching line
[](#cb219-3)$ # NR>2 is needed as first 2 records shouldn't be considered for a match
[](#cb219-4)$ awk 'NR>2 && /toy|flower/{print p2} {p2=p1; p1=$0}' context.txt
[](#cb219-5)blue
[](#cb219-6)    sand stone
[](#cb219-7)
[](#cb219-8)$ # else, use an array to save previous records
[](#cb219-9)$ awk -v n=4 'NR>n && /age/{print a[NR-n]} {a[NR]=$0}' context.txt
[](#cb219-10)light blue
[](#cb219-11)    english
```

## Records bounded by distinct markers

This section will cover cases where the input file will always contain the same number of starting and ending patterns and arranged in alternating fashion. For example, there cannot be two starting patterns appearing without an ending pattern between them and vice versa. Zero or more records of text can appear inside such groups as well as in between the groups.

The sample file shown below will be used to illustrate examples in this section. For simplicity, assume that the starting pattern is marked by `start` and the ending pattern by `end`. They have also been given group numbers to make it easier to visualize the transformation between input and output for the commands discussed in this section.

```
[](#cb220-1)$ cat uniform.txt
[](#cb220-2)mango
[](#cb220-3)icecream
[](#cb220-4)--start 1--
[](#cb220-5)1234
[](#cb220-6)6789
[](#cb220-7)**end 1**
[](#cb220-8)how are you
[](#cb220-9)have a nice day
[](#cb220-10)--start 2--
[](#cb220-11)a
[](#cb220-12)b
[](#cb220-13)c
[](#cb220-14)**end 2**
[](#cb220-15)par,far,mar,tar
```

**Case 1:** Processing all the groups of records based on the distinct markers, including the records matched by markers themselves. For simplicity, the below command will just print all such records.

```
[](#cb221-1)$ awk '/start/{f=1} f; /end/{f=0}' uniform.txt
[](#cb221-2)--start 1--
[](#cb221-3)1234
[](#cb221-4)6789
[](#cb221-5)**end 1**
[](#cb221-6)--start 2--
[](#cb221-7)a
[](#cb221-8)b
[](#cb221-9)c
[](#cb221-10)**end 2**
```

> ![info](media/file0.svg) Similar to `sed -n '/start/,/end/p'` you can also use `awk '/start/,/end/'` but the state machine format is more suitable to change for various cases to follow.

**Case 2:** Processing all the groups of records but excluding the records matched by markers themselves.

```
[](#cb222-1)$ awk '/end/{f=0} f{print "*", $0} /start/{f=1}' uniform.txt
[](#cb222-2)* 1234
[](#cb222-3)* 6789
[](#cb222-4)* a
[](#cb222-5)* b
[](#cb222-6)* c
```

**Case 3-4:** Processing all the groups of records but excluding either of the markers.

```
[](#cb223-1)$ awk '/start/{f=1} /end/{f=0} f' uniform.txt
[](#cb223-2)--start 1--
[](#cb223-3)1234
[](#cb223-4)6789
[](#cb223-5)--start 2--
[](#cb223-6)a
[](#cb223-7)b
[](#cb223-8)c
[](#cb223-9)
[](#cb223-10)$ awk 'f; /start/{f=1} /end/{f=0}' uniform.txt
[](#cb223-11)1234
[](#cb223-12)6789
[](#cb223-13)**end 1**
[](#cb223-14)a
[](#cb223-15)b
[](#cb223-16)c
[](#cb223-17)**end 2**
```

The next four cases are obtained by just using `!f` instead of `f` from the cases shown above.

**Case 5:** Processing all input records except the groups of records bound by the markers.

```
[](#cb224-1)$ awk '/start/{f=1} !f{print $0 "."} /end/{f=0}' uniform.txt
[](#cb224-2)mango.
[](#cb224-3)icecream.
[](#cb224-4)how are you.
[](#cb224-5)have a nice day.
[](#cb224-6)par,far,mar,tar.
```

**Case 6** Processing all input records except the groups of records between the markers.

```
[](#cb225-1)$ awk '/end/{f=0} !f; /start/{f=1}' uniform.txt
[](#cb225-2)mango
[](#cb225-3)icecream
[](#cb225-4)--start 1--
[](#cb225-5)**end 1**
[](#cb225-6)how are you
[](#cb225-7)have a nice day
[](#cb225-8)--start 2--
[](#cb225-9)**end 2**
[](#cb225-10)par,far,mar,tar
```

**Case 7-8:** Similar to case 6, but include only one of the markers.

```
[](#cb226-1)$ awk '!f; /start/{f=1} /end/{f=0}' uniform.txt
[](#cb226-2)mango
[](#cb226-3)icecream
[](#cb226-4)--start 1--
[](#cb226-5)how are you
[](#cb226-6)have a nice day
[](#cb226-7)--start 2--
[](#cb226-8)par,far,mar,tar
[](#cb226-9)
[](#cb226-10)$ awk '/start/{f=1} /end/{f=0} !f' uniform.txt
[](#cb226-11)mango
[](#cb226-12)icecream
[](#cb226-13)**end 1**
[](#cb226-14)how are you
[](#cb226-15)have a nice day
[](#cb226-16)**end 2**
[](#cb226-17)par,far,mar,tar
```

## Specific blocks

Instead of working with all the groups (or blocks) bound by the markers, this section will discuss how to choose blocks based on additional criteria.

Here's how you can process only the first matching block.

```
[](#cb227-1)$ awk '/start/{f=1} f; /end/{exit}' uniform.txt
[](#cb227-2)--start 1--
[](#cb227-3)1234
[](#cb227-4)6789
[](#cb227-5)**end 1**
[](#cb227-6)
[](#cb227-7)$ # use other tricks discussed in previous section as needed
[](#cb227-8)$ awk '/end/{exit} f; /start/{f=1}' uniform.txt
[](#cb227-9)1234
[](#cb227-10)6789
```

Getting last block alone involves lot more work, unless you happen to know how many blocks are present in the input file.

```
[](#cb228-1)$ # reverse input linewise, change the order of comparison, reverse again
[](#cb228-2)$ # can't be used if RS has to be something other than newline
[](#cb228-3)$ tac uniform.txt | awk '/end/{f=1} f; /start/{exit}' | tac
[](#cb228-4)--start 2--
[](#cb228-5)a
[](#cb228-6)b
[](#cb228-7)c
[](#cb228-8)**end 2**
[](#cb228-9)
[](#cb228-10)$ # or, save the blocks in a buffer and print the last one alone
[](#cb228-11)$ awk '/start/{f=1; b=$0; next} f{b=b ORS $0} /end/{f=0}
[](#cb228-12) END{print b}' uniform.txt
[](#cb228-13)--start 2--
[](#cb228-14)a
[](#cb228-15)b
[](#cb228-16)c
[](#cb228-17)**end 2**
```

Only the `n`th block.

```
[](#cb229-1)$ # can also use: awk -v n=2 '/4/{c++} c==n{print; if(/6/) exit}'
[](#cb229-2)$ seq 30 | awk -v n=2 '/4/{c++} c==n; /6/ && c==n{exit}'
[](#cb229-3)14
[](#cb229-4)15
[](#cb229-5)16
```

All blocks greater than `n`th block.

```
[](#cb230-1)$ seq 30 | awk -v n=1 '/4/{f=1; c++} f && c>n; /6/{f=0}'
[](#cb230-2)14
[](#cb230-3)15
[](#cb230-4)16
[](#cb230-5)24
[](#cb230-6)25
[](#cb230-7)26
```

Excluding `n`th block.

```
[](#cb231-1)$ seq 30 | awk -v n=2 '/4/{f=1; c++} f && c!=n; /6/{f=0}'
[](#cb231-2)4
[](#cb231-3)5
[](#cb231-4)6
[](#cb231-5)24
[](#cb231-6)25
[](#cb231-7)26
```

All blocks, only if the records between the markers match an additional condition.

```
[](#cb232-1)$ # additional condition here is a record with entire content as '15'
[](#cb232-2)$ seq 30 | awk '/4/{f=1; buf=$0; m=0; next}
[](#cb232-3) f{buf=buf ORS $0}
[](#cb232-4) /6/{f=0; if(m) print buf}
[](#cb232-5) $0=="15"{m=1}'
[](#cb232-6)14
[](#cb232-7)15
[](#cb232-8)16
```

## Broken blocks

Sometimes, you can have markers in random order and mixed in different ways. In such cases, to work with blocks without any other marker present in between them, the buffer approach comes in handy again.

```
[](#cb233-1)$ cat broken.txt
[](#cb233-2)qqqqqqqqqqqqqqqq
[](#cb233-3)error 1
[](#cb233-4)hi
[](#cb233-5)error 2
[](#cb233-6)1234
[](#cb233-7)6789
[](#cb233-8)state 1
[](#cb233-9)bye
[](#cb233-10)state 2
[](#cb233-11)error 3
[](#cb233-12)xyz
[](#cb233-13)error 4
[](#cb233-14)abcd
[](#cb233-15)state 3
[](#cb233-16)zzzzzzzzzzzzzzzz
[](#cb233-17)
[](#cb233-18)$ awk '/error/{f=1; buf=$0; next}
[](#cb233-19) f{buf=buf ORS $0}
[](#cb233-20) /state/{if(f) print buf; f=0}' broken.txt
[](#cb233-21)error 2
[](#cb233-22)1234
[](#cb233-23)6789
[](#cb233-24)state 1
[](#cb233-25)error 4
[](#cb233-26)abcd
[](#cb233-27)state 3
```

## Summary

This chapter covered various examples of working with multiple records. State machines play an important role in deriving solutions for such cases. Knowing various corner cases is also crucial, otherwise a solution that works for one input may fail for others.

Next chapter will discuss use cases where you need to process a file input based on contents of another file.

## Exercises

**a)** For the input file `sample.txt`, print a matching line containing `do` only if the previous line is empty and the line before that contains `you`.

```
[](#cb234-1)$ awk ##### add your solution here
[](#cb234-2)Just do-it
[](#cb234-3)Much ado about nothing
```

**b)** Print only the second matching line respectively for the search terms `do` and `not` for the input file `sample.txt`. Match these terms case insensitively.

```
[](#cb235-1)$ awk ##### add your solution here
[](#cb235-2)No doubt you like it too
[](#cb235-3)Much ado about nothing
```

**c)** For the input file `sample.txt`, print the matching lines containing `are` or `bit` as well as `n` lines around the matching lines. The value for `n` is passed to the `awk` command via the `-v` option.

```
[](#cb236-1)$ awk -v n=1 ##### add your solution here
[](#cb236-2)Good day
[](#cb236-3)How are you
[](#cb236-4)
[](#cb236-5)Today is sunny
[](#cb236-6)Not a bit funny
[](#cb236-7)No doubt you like it too
[](#cb236-8)
[](#cb236-9)$ # note that first and last line are empty for this case
[](#cb236-10)$ awk -v n=2 ##### add your solution here
[](#cb236-11)
[](#cb236-12)Good day
[](#cb236-13)How are you
[](#cb236-14)
[](#cb236-15)Just do-it
[](#cb236-16)
[](#cb236-17)Today is sunny
[](#cb236-18)Not a bit funny
[](#cb236-19)No doubt you like it too
```

**d)** For the input file `broken.txt`, print all lines between the markers `top` and `bottom`. The first `awk` command shown below doesn't work because it is matching till end of file if second marker isn't found. Assume that the input file cannot have two `top` markers without a `bottom` marker appearing in between and vice-versa.

```
[](#cb237-1)$ cat broken.txt
[](#cb237-2)top
[](#cb237-3)3.14
[](#cb237-4)bottom
[](#cb237-5)---
[](#cb237-6)top
[](#cb237-7)1234567890
[](#cb237-8)bottom
[](#cb237-9)top
[](#cb237-10)Hi there
[](#cb237-11)Have a nice day
[](#cb237-12)Good bye
[](#cb237-13)
[](#cb237-14)$ # wrong output
[](#cb237-15)$ awk '/bottom/{f=0} f; /top/{f=1}' broken.txt
[](#cb237-16)3.14
[](#cb237-17)1234567890
[](#cb237-18)Hi there
[](#cb237-19)Have a nice day
[](#cb237-20)Good bye
[](#cb237-21)
[](#cb237-22)$ # expected output
[](#cb237-23)$ ##### add your solution here
[](#cb237-24)3.14
[](#cb237-25)1234567890
```

**e)** For the input file `concat.txt`, extract contents from a line starting with `###` until but not including the next such line. The block to be extracted is indicated by variable `n` passed via the `-v` option.

```
[](#cb238-1)$ cat concat.txt
[](#cb238-2)### addr.txt
[](#cb238-3)How are you
[](#cb238-4)This game is good
[](#cb238-5)Today is sunny
[](#cb238-6)### broken.txt
[](#cb238-7)top
[](#cb238-8)1234567890
[](#cb238-9)bottom
[](#cb238-10)### sample.txt
[](#cb238-11)Just do-it
[](#cb238-12)Believe it
[](#cb238-13)### mixed_fs.txt
[](#cb238-14)pink blue white yellow
[](#cb238-15)car,mat,ball,basket
[](#cb238-16)
[](#cb238-17)$ awk -v n=2 ##### add your solution here
[](#cb238-18)### broken.txt
[](#cb238-19)top
[](#cb238-20)1234567890
[](#cb238-21)bottom
[](#cb238-22)$ awk -v n=4 ##### add your solution here
[](#cb238-23)### mixed_fs.txt
[](#cb238-24)pink blue white yellow
[](#cb238-25)car,mat,ball,basket
```

**f)** For the input file `ruby.md`, replace all occurrences of `ruby` (irrespective of case) with `Ruby`. But, do not replace any matches between ```` ```ruby ```` and ```` ``` ```` lines (`ruby` in these markers shouldn't be replaced either).

```
[](#cb239-1)$ awk ##### add your solution here ruby.md > out.md
[](#cb239-2)$ diff -sq out.md expected.md 
[](#cb239-3)Files out.md and expected.md are identical
```

# Two file processing

This chapter focuses on solving problems which depend upon contents of two files. These are usually based on comparing records and fields. Sometimes, record number plays a role too. You'll also learn about the `getline` built-in function.

## Comparing records

Consider the following input files which will be compared line wise to get common lines and unique lines.

```
[](#cb240-1)$ cat color_list1.txt
[](#cb240-2)teal
[](#cb240-3)light blue
[](#cb240-4)green
[](#cb240-5)yellow
[](#cb240-6)
[](#cb240-7)$ cat color_list2.txt
[](#cb240-8)light blue
[](#cb240-9)black
[](#cb240-10)dark green
[](#cb240-11)yellow
```

The *key* features used in the solution below:

*   For two files as input, `NR==FNR` will be `true` only when the first file is being processed
*   `next` will skip rest of code and fetch next record
*   `a[$0]` by itself is a valid statement. It will create an uninitialized element in array `a` with `$0` as the key (assuming the key doesn't exist yet)
*   `$0 in a` checks if the given string (`$0` here) exists as a key in array `a`

```
[](#cb241-1)$ # common lines
[](#cb241-2)$ # same as: grep -Fxf color_list1.txt color_list2.txt
[](#cb241-3)$ awk 'NR==FNR{a[$0]; next} $0 in a' color_list1.txt color_list2.txt
[](#cb241-4)light blue
[](#cb241-5)yellow
[](#cb241-6)
[](#cb241-7)$ # lines from color_list2.txt not present in color_list1.txt
[](#cb241-8)$ # same as: grep -vFxf color_list1.txt color_list2.txt
[](#cb241-9)$ awk 'NR==FNR{a[$0]; next} !($0 in a)' color_list1.txt color_list2.txt
[](#cb241-10)black
[](#cb241-11)dark green
[](#cb241-12)
[](#cb241-13)$ # reversing the order of input files gives
[](#cb241-14)$ # lines from color_list1.txt not present in color_list2.txt
[](#cb241-15)$ awk 'NR==FNR{a[$0]; next} !($0 in a)' color_list2.txt color_list1.txt
[](#cb241-16)teal
[](#cb241-17)green
```

> ![warning](media/file1.svg) Note that the `NR==FNR` logic will fail if the first file is empty.

## Comparing fields

In the previous section, you saw how to compare whole contents of records between two files. This section will focus on comparing only specific field(s). The below sample file will be one of the two file inputs for examples in this section.

```
[](#cb242-1)$ cat marks.txt
[](#cb242-2)Dept    Name    Marks
[](#cb242-3)ECE     Raj     53
[](#cb242-4)ECE     Joel    72
[](#cb242-5)EEE     Moi     68
[](#cb242-6)CSE     Surya   81
[](#cb242-7)EEE     Tia     59
[](#cb242-8)ECE     Om      92
[](#cb242-9)CSE     Amy     67
```

To start with, here's a single field comparison. The problem statement is to fetch all records from `marks.txt` if the first field matches any of the departments listed in `dept.txt` file.

```
[](#cb243-1)$ cat dept.txt
[](#cb243-2)CSE
[](#cb243-3)ECE
[](#cb243-4)
[](#cb243-5)$ # note that dept.txt is used to build the array keys first
[](#cb243-6)$ awk 'NR==FNR{a[$1]; next} $1 in a' dept.txt marks.txt
[](#cb243-7)ECE     Raj     53
[](#cb243-8)ECE     Joel    72
[](#cb243-9)CSE     Surya   81
[](#cb243-10)ECE     Om      92
[](#cb243-11)CSE     Amy     67
[](#cb243-12)
[](#cb243-13)$ # if header is needed as well
[](#cb243-14)$ awk 'NR==FNR{a[$1]; next} FNR==1 || $1 in a' dept.txt marks.txt
[](#cb243-15)Dept    Name    Marks
[](#cb243-16)ECE     Raj     53
[](#cb243-17)ECE     Joel    72
[](#cb243-18)CSE     Surya   81
[](#cb243-19)ECE     Om      92
[](#cb243-20)CSE     Amy     67
```

For multiple field comparison, you need to construct the key robustly. Simply concatenating field values can lead to false matches. For example, field values `abc` and `123` will wrongly match `ab` and `c123`. To avoid this, you may introduce some string between the field values, say `"_"` (if you know the field themselves cannot have this character) or `FS` (safer option). You could also allow `awk` to bail you out. If you use `,` symbol (not `","` as a string) between field values, the value of special variable `SUBSEP` is inserted. `SUBSEP` has a default value of the non-printing character `\034` which is usually not used as part of text files.

```
[](#cb244-1)$ cat dept_name.txt
[](#cb244-2)EEE Moi
[](#cb244-3)CSE Amy
[](#cb244-4)ECE Raj
[](#cb244-5)
[](#cb244-6)$ # uses SUBSEP as separator between field values to construct the key
[](#cb244-7)$ # note the use of parentheses for key testing
[](#cb244-8)$ awk 'NR==FNR{a[$1,$2]; next} ($1,$2) in a' dept_name.txt marks.txt
[](#cb244-9)ECE     Raj     53
[](#cb244-10)EEE     Moi     68
[](#cb244-11)CSE     Amy     67
```

In this example, one of the field is used for numerical comparison.

```
[](#cb245-1)$ cat dept_mark.txt
[](#cb245-2)ECE 70
[](#cb245-3)EEE 65
[](#cb245-4)CSE 80
[](#cb245-5)
[](#cb245-6)$ # match Dept and minimum marks specified in dept_mark.txt
[](#cb245-7)$ awk 'NR==FNR{d[$1]=$2; next}
[](#cb245-8) $1 in d && $3 >= d[$1]' dept_mark.txt marks.txt
[](#cb245-9)ECE     Joel    72
[](#cb245-10)EEE     Moi     68
[](#cb245-11)CSE     Surya   81
[](#cb245-12)ECE     Om      92
```

Here's an example of adding a new field.

```
[](#cb246-1)$ cat role.txt
[](#cb246-2)Raj class_rep
[](#cb246-3)Amy sports_rep
[](#cb246-4)Tia placement_rep
[](#cb246-5)
[](#cb246-6)$ awk -v OFS='\t' 'NR==FNR{r[$1]=$2; next}
[](#cb246-7) {$(NF+1) = FNR==1 ? "Role" : r[$2]} 1' role.txt marks.txt
[](#cb246-8)Dept    Name    Marks   Role
[](#cb246-9)ECE     Raj     53      class_rep
[](#cb246-10)ECE     Joel    72
[](#cb246-11)EEE     Moi     68
[](#cb246-12)CSE     Surya   81
[](#cb246-13)EEE     Tia     59      placement_rep
[](#cb246-14)ECE     Om      92
[](#cb246-15)CSE     Amy     67      sports_rep
```

## getline

As the name indicates, `getline` function allows you to read a line from a file on demand. This is most useful when you need something based on line number. The following example shows how you can replace `m`th line from a file with `n`th line from another file. There are many syntax variations with `getline`, here the line read is saved in a variable.

```
[](#cb247-1)$ # return value handling is not shown here, but should be done ideally
[](#cb247-2)$ awk -v m=3 -v n=2 'BEGIN{while(n-- > 0) getline s < "greeting.txt"}
[](#cb247-3) FNR==m{$0=s} 1' table.txt
[](#cb247-4)brown bread mat hair 42
[](#cb247-5)blue cake mug shirt -7
[](#cb247-6)Have a nice day
```

Here's an example where two files are processed simultaneously. In this case, the return value of `getline` is also used. It will be `1` if line was read successfully, `0` if there's no more input to be read as end of file has already been reached and `-1` if something went wrong. The `ERRNO` special variable will have details regarding the issues.

```
[](#cb248-1)$ # print line from greeting.txt if last column of corresponding line
[](#cb248-2)$ # from table.txt is +ve number
[](#cb248-3)$ awk -v file='table.txt' '(getline line < file)==1{n=split(line, a);
[](#cb248-4) if(a[n]>0) print}' greeting.txt
[](#cb248-5)Hi there
[](#cb248-6)Good bye
```

If a file is passed as argument to `awk` command and cannot be opened, you get an error. For example:

```
[](#cb249-1)$ awk '{print $2}' xyz.txt
[](#cb249-2)awk: fatal: cannot open file `xyz.txt' for reading (No such file or directory)
```

It is recommended to always check for return value when using `getline` or perhaps use techniques from previous sections to avoid `getline` altogether.

```
[](#cb250-1)$ # xyz.txt doesn't exist, but output doesn't show something went wrong
[](#cb250-2)$ awk '{getline line < "xyz.txt"; print $NF, line}' table.txt
[](#cb250-3)42 
[](#cb250-4)-7 
[](#cb250-5)3.14 
[](#cb250-6)
[](#cb250-7)$ awk -v file='xyz.txt' '{ e=(getline line < file);
[](#cb250-8) if(e<0){print file ": " ERRNO; exit}
[](#cb250-9) print $NF, line }' table.txt
[](#cb250-10)xyz.txt: No such file or directory
```

> ![info](media/file0.svg) See [gawk manual: getline](https://www.gnu.org/software/gawk/manual/gawk.html#Getline) for details, especially about corner cases and errors. See also [awk.freeshell: getline caveats](https://awk.freeshell.org/AllAboutGetline).

## Summary

This chapter discussed a few cases where you need to compare contents of two files. The `NR==FNR` trick is handy for such cases. The `getline` function is helpful for line number based comparisons.

Next chapter will discuss how to handle duplicate contents.

## Exercises

**a)** Use contents of `match_words.txt` file to display matching lines from `jumbled.txt` and `sample.txt`. The matching criteria is that the second word of lines from these files should match the third word of lines from `match_words.txt`.

```
[](#cb251-1)$ cat match_words.txt
[](#cb251-2)%whole(Hello)--{doubt}==ado==
[](#cb251-3)just,\joint*,concession<=nice
[](#cb251-4)
[](#cb251-5)$ # 'concession' is one of the third words from 'match_words.txt'
[](#cb251-6)$ # and second word from 'jumbled.txt'
[](#cb251-7)$ awk ##### add your solution here
[](#cb251-8)wavering:concession/woof\retailer
[](#cb251-9)No doubt you like it too
```

**b)** Interleave contents of `secrets.txt` with the contents of a file passed via `-v` option as shown below.

```
[](#cb252-1)$ awk -v f='table.txt' ##### add your solution here
[](#cb252-2)stag area row tick
[](#cb252-3)brown bread mat hair 42
[](#cb252-4)---
[](#cb252-5)deaf chi rate tall glad
[](#cb252-6)blue cake mug shirt -7
[](#cb252-7)---
[](#cb252-8)Bi tac toe - 42
[](#cb252-9)yellow banana window shoes 3.14
[](#cb252-10)---
```

**c)** The file `search_terms.txt` contains one search string per line (these have no regexp metacharacters). Construct an `awk` command that reads this file and displays search terms (matched case insensitively) that were found in all of the other file arguments. Note that these terms should be matched with any part of the line, not just whole words.

```
[](#cb253-1)$ cat search_terms.txt
[](#cb253-2)hello
[](#cb253-3)row
[](#cb253-4)you
[](#cb253-5)is
[](#cb253-6)at
[](#cb253-7)
[](#cb253-8)$ awk ##### add your solution here
[](#cb253-9)##file list## search_terms.txt jumbled.txt mixed_fs.txt secrets.txt table.txt
[](#cb253-10)at
[](#cb253-11)row
[](#cb253-12)$ awk ##### add your solution here
[](#cb253-13)##file list## search_terms.txt addr.txt sample.txt
[](#cb253-14)is
[](#cb253-15)you
[](#cb253-16)hello
```

# Dealing with duplicates

Often, you need to eliminate duplicates from an input file. This could be based on entire line content or based on certain fields. These are typically solved with `sort` and `uniq` commands. Advantage with `awk` include regexp based field and record separators, input doesn't have to be sorted, and in general more flexibility because it is a programming language.

## Whole line duplicates

`awk '!a[$0]++'` is one of the most famous `awk` one-liners. It eliminates line based duplicates while retaining input order. The following example shows it in action along with an illustration of how the logic works.

```
[](#cb254-1)$ cat purchases.txt
[](#cb254-2)coffee
[](#cb254-3)tea
[](#cb254-4)washing powder
[](#cb254-5)coffee
[](#cb254-6)toothpaste
[](#cb254-7)tea
[](#cb254-8)soap
[](#cb254-9)tea
[](#cb254-10)
[](#cb254-11)$ awk '{print +a[$0] "\t" $0; a[$0]++}' purchases.txt
[](#cb254-12)0       coffee
[](#cb254-13)0       tea
[](#cb254-14)0       washing powder
[](#cb254-15)1       coffee
[](#cb254-16)0       toothpaste
[](#cb254-17)1       tea
[](#cb254-18)0       soap
[](#cb254-19)2       tea
[](#cb254-20)
[](#cb254-21)$ # only those entries with zero in first column will be retained
[](#cb254-22)$ awk '!a[$0]++' purchases.txt
[](#cb254-23)coffee
[](#cb254-24)tea
[](#cb254-25)washing powder
[](#cb254-26)toothpaste
[](#cb254-27)soap
```

## Column wise duplicates

Removing field based duplicates is simple for single field comparison. Just change `$0` to the required field number after setting the appropriate field separator.

```
[](#cb255-1)$ cat duplicates.txt
[](#cb255-2)brown,toy,bread,42
[](#cb255-3)dark red,ruby,rose,111
[](#cb255-4)blue,ruby,water,333
[](#cb255-5)dark red,sky,rose,555
[](#cb255-6)yellow,toy,flower,333
[](#cb255-7)white,sky,bread,111
[](#cb255-8)light red,purse,rose,333
[](#cb255-9)
[](#cb255-10)$ # based on last field
[](#cb255-11)$ awk -F, '!seen[$NF]++' duplicates.txt
[](#cb255-12)brown,toy,bread,42
[](#cb255-13)dark red,ruby,rose,111
[](#cb255-14)blue,ruby,water,333
[](#cb255-15)dark red,sky,rose,555
```

For multiple fields comparison, separate the fields with `,` so that `SUBSEP` is used to combine the field values to generate the key. As mentioned before, `SUBSEP` has a default value of `\034` non-printing character, which is typically not used in text files.

```
[](#cb256-1)$ # based on first and third field
[](#cb256-2)$ awk -F, '!seen[$1,$3]++' duplicates.txt
[](#cb256-3)brown,toy,bread,42
[](#cb256-4)dark red,ruby,rose,111
[](#cb256-5)blue,ruby,water,333
[](#cb256-6)yellow,toy,flower,333
[](#cb256-7)white,sky,bread,111
[](#cb256-8)light red,purse,rose,333
```

## Duplicate count

In this section, how many times a duplicate record is found plays a role in determining the output.

First up, printing only a specific numbered duplicate.

```
[](#cb257-1)$ # print only the second occurrence of duplicates based on 2nd field
[](#cb257-2)$ awk -F, '++seen[$2]==2' duplicates.txt
[](#cb257-3)blue,ruby,water,333
[](#cb257-4)yellow,toy,flower,333
[](#cb257-5)white,sky,bread,111
[](#cb257-6)
[](#cb257-7)$ # print only the third occurrence of duplicates based on last field
[](#cb257-8)$ awk -F, '++seen[$NF]==3' duplicates.txt
[](#cb257-9)light red,purse,rose,333
```

Next, printing only the last copy of duplicate. Since the count isn't known, the `tac` command comes in handy again.

```
[](#cb258-1)$ # reverse the input line-wise, retain first copy and then reverse again
[](#cb258-2)$ tac duplicates.txt | awk -F, '!seen[$NF]++' | tac
[](#cb258-3)brown,toy,bread,42
[](#cb258-4)dark red,sky,rose,555
[](#cb258-5)white,sky,bread,111
[](#cb258-6)light red,purse,rose,333
```

To get all the records based on a duplicate count, you can pass the input file twice. Then use the two file processing trick to make decisions.

```
[](#cb259-1)$ # all duplicates based on last column
[](#cb259-2)$ awk -F, 'NR==FNR{a[$NF]++; next} a[$NF]>1' duplicates.txt duplicates.txt
[](#cb259-3)dark red,ruby,rose,111
[](#cb259-4)blue,ruby,water,333
[](#cb259-5)yellow,toy,flower,333
[](#cb259-6)white,sky,bread,111
[](#cb259-7)light red,purse,rose,333
[](#cb259-8)
[](#cb259-9)$ # all duplicates based on last column, minimum 3 duplicates
[](#cb259-10)$ awk -F, 'NR==FNR{a[$NF]++; next} a[$NF]>2' duplicates.txt duplicates.txt
[](#cb259-11)blue,ruby,water,333
[](#cb259-12)yellow,toy,flower,333
[](#cb259-13)light red,purse,rose,333
[](#cb259-14)
[](#cb259-15)$ # only unique lines based on 3rd column
[](#cb259-16)$ awk -F, 'NR==FNR{a[$3]++; next} a[$3]==1' duplicates.txt duplicates.txt
[](#cb259-17)blue,ruby,water,333
[](#cb259-18)yellow,toy,flower,333
```

## Summary

This chapter showed how to work with duplicate contents, both record and field based. If you don't need regexp based separators and if your input is too big to handle, then specialized command line tools `sort` and `uniq` will be better suited compared to `awk`.

Next chapter will show how to write `awk` scripts instead of the usual one-liners.

## Exercises

**a)** Retain only first copy of a line for the input file `lines.txt`. Case should be ignored while comparing lines. For example `hi there` and `HI TheRE` will be considered as duplicates.

```
[](#cb260-1)$ cat lines.txt
[](#cb260-2)Go There
[](#cb260-3)come on
[](#cb260-4)go there
[](#cb260-5)---
[](#cb260-6)2 apples and 5 mangoes
[](#cb260-7)come on!
[](#cb260-8)---
[](#cb260-9)2 Apples
[](#cb260-10)COME ON
[](#cb260-11)
[](#cb260-12)$ awk ##### add your solution here
[](#cb260-13)Go There
[](#cb260-14)come on
[](#cb260-15)---
[](#cb260-16)2 apples and 5 mangoes
[](#cb260-17)come on!
[](#cb260-18)2 Apples
```

**b)** Retain only first copy of a line for the input file `lines.txt`. Assume space as field separator with two fields on each line. Compare the lines irrespective of order of the fields. For example, `hehe haha` and `haha hehe` will be considered as duplicates.

```
[](#cb261-1)$ cat twos.txt
[](#cb261-2)hehe haha
[](#cb261-3)door floor
[](#cb261-4)haha hehe
[](#cb261-5)6;8 3-4
[](#cb261-6)true blue
[](#cb261-7)hehe bebe
[](#cb261-8)floor door
[](#cb261-9)3-4 6;8
[](#cb261-10)tru eblue
[](#cb261-11)haha hehe
[](#cb261-12)
[](#cb261-13)$ awk ##### add your solution here
[](#cb261-14)hehe haha
[](#cb261-15)door floor
[](#cb261-16)6;8 3-4
[](#cb261-17)true blue
[](#cb261-18)hehe bebe
[](#cb261-19)tru eblue
```

**c)** For the input file `twos.txt`, create a file `uniq.txt` with all the unique lines and `dupl.txt` with all the duplicate lines. Assume space as field separator with two fields on each line. Compare the lines irrespective of order of the fields. For example, `hehe haha` and `haha hehe` will be considered as duplicates.

```
[](#cb262-1)$ awk ##### add your solution here
[](#cb262-2)
[](#cb262-3)$ cat uniq.txt 
[](#cb262-4)true blue
[](#cb262-5)hehe bebe
[](#cb262-6)tru eblue
[](#cb262-7)$ cat dupl.txt 
[](#cb262-8)hehe haha
[](#cb262-9)door floor
[](#cb262-10)haha hehe
[](#cb262-11)6;8 3-4
[](#cb262-12)floor door
[](#cb262-13)3-4 6;8
[](#cb262-14)haha hehe
```

# awk scripts

## -f option

The `-f` command line option allows you to pass the `awk` code via file instead of writing it all on the command line. Here's a one-liner seen earlier that's been converted to a multiline script. Note that `;` is no longer necessary to separate the commands, newline will do that too.

```
[](#cb263-1)$ cat buf.awk
[](#cb263-2)/error/{
[](#cb263-3)    f = 1
[](#cb263-4)    buf = $0
[](#cb263-5)    next
[](#cb263-6)}
[](#cb263-7)
[](#cb263-8)f{
[](#cb263-9)    buf = buf ORS $0
[](#cb263-10)}
[](#cb263-11)
[](#cb263-12)/state/{
[](#cb263-13)    if(f)
[](#cb263-14)        print buf
[](#cb263-15)    f = 0
[](#cb263-16)}
[](#cb263-17)
[](#cb263-18)$ awk -f buf.awk broken.txt
[](#cb263-19)error 2
[](#cb263-20)1234
[](#cb263-21)6789
[](#cb263-22)state 1
[](#cb263-23)error 4
[](#cb263-24)abcd
[](#cb263-25)state 3
```

Another advantage is that single quotes can be freely used.

```
[](#cb264-1)$ echo 'cue us on this example' | awk -v q="'" '{gsub(/\w+/, q "&" q)} 1'
[](#cb264-2)'cue' 'us' 'on' 'this' 'example'
[](#cb264-3)
[](#cb264-4)# the above solution is simpler to write as a script
[](#cb264-5)$ cat quotes.awk
[](#cb264-6){
[](#cb264-7)    gsub(/\w+/, "'&'")
[](#cb264-8)}
[](#cb264-9)
[](#cb264-10)1
[](#cb264-11)
[](#cb264-12)$ echo 'cue us on this example' | awk -f quotes.awk
[](#cb264-13)'cue' 'us' 'on' 'this' 'example'
```

## -o option

If the code has been first tried out on command line, add `-o` option to get a pretty printed version. Output filename can be passed along `-o` option, otherwise `awkprof.out` will be used by default.

```
[](#cb265-1)$ # adding -o after the one-liner has been tested
[](#cb265-2)$ # input filenames and -v would be simply ignored
[](#cb265-3)$ awk -o -v OFS='\t' 'NR==FNR{r[$1]=$2; next}
[](#cb265-4) {$(NF+1) = FNR==1 ? "Role" : r[$2]} 1' role.txt marks.txt
[](#cb265-5)
[](#cb265-6)$ # pretty printed version
[](#cb265-7)$ cat awkprof.out
[](#cb265-8)NR == FNR {
[](#cb265-9)        r[$1] = $2
[](#cb265-10)        next
[](#cb265-11)}
[](#cb265-12)
[](#cb265-13){
[](#cb265-14)        $(NF + 1) = FNR == 1 ? "Role" : r[$2]
[](#cb265-15)}
[](#cb265-16)
[](#cb265-17)1 {
[](#cb265-18)        print
[](#cb265-19)}
[](#cb265-20)
[](#cb265-21)$ # calling the script
[](#cb265-22)$ # note that other command line options have to be provided as usual
[](#cb265-23)$ awk -v OFS='\t' -f awkprof.out role.txt marks.txt
[](#cb265-24)Dept    Name    Marks   Role
[](#cb265-25)ECE     Raj     53      class_rep
[](#cb265-26)ECE     Joel    72
[](#cb265-27)EEE     Moi     68
[](#cb265-28)CSE     Surya   81
[](#cb265-29)EEE     Tia     59      placement_rep
[](#cb265-30)ECE     Om      92
[](#cb265-31)CSE     Amy     67      sports_rep
```

## Summary

So, now you know how to write program files for `awk` instead of just the one-liners. And about the useful `-o` option, helps to convert complicated one-liners to pretty printed program files.

Next chapter will discuss a few gotchas and tricks.

## Exercises

**a)** Before explaining the problem statement, here's an example of markdown headers and their converted link version. Note the use of `-1` for the second occurrence of `Summary` header. Also note that this sample doesn't simulate all the rules.

```
[](#cb266-1)# Field separators
[](#cb266-2)## Summary
[](#cb266-3)# Gotchas and Tips
[](#cb266-4)## Summary
[](#cb266-5)
[](#cb266-6)* [Field separators](#field-separators)
[](#cb266-7)    * [Summary](#summary)
[](#cb266-8)* [Gotchas and Tips](#gotchas-and-tips)
[](#cb266-9)    * [Summary](#summary-1)
```

For the input file `gawk.md`, construct table of content links as per the details described below.

*   Identify all header lines
    *   there are two types of header lines, one starting with `#` and the other starting with `##`
    *   lines starting with `#` inside code blocks defined by ```` ```bash ```` and ```` ``` ```` markers should be ignored
*   The headers lines should then be converted as per the following rules:
    *   content is defined as portion of the header ignoring the initial `#` or `##` characters and a space character
    *   initial `##` should be replaced with four spaces and a `*`
    *   else, initial `#` should be replaced with `*`
    *   create a copy of the content, change it to all lowercase, replace all space characters with `-` character and then place it within `(#` and `)`
        *   if there are multiple headers with same content, append `-1`, `-2`, etc respectively for the second header, third header, etc
    *   surround the original content with `[]` and then append the string obtained from previous step
*   Note that the output should have only the converted headers, all other input lines should not be present

As the input file `gawk.md` is too long, only the commands to verify your solution is shown.

```
[](#cb267-1)$ awk -f toc.awk gawk.md > out.md
[](#cb267-2)$ diff -sq out.md toc_expected.md
[](#cb267-3)Files out.md and toc_expected.md are identical
```

**b)** For the input file `odd.txt`, surround first two whole words of each line with `{}` that start and end with the same word character. Assume that input file will not require case insensitive comparison. This is a contrived exercise that needs around 10 instructions and makes you recall various features presented in this book.

```
[](#cb268-1)$ cat odd.txt
[](#cb268-2)-oreo-not:a _a2_ roar<=>took%22
[](#cb268-3)RoaR to wow-
[](#cb268-4)
[](#cb268-5)$ awk -f same.awk odd.txt
[](#cb268-6)-{oreo}-not:{a} _a2_ roar<=>took%22
[](#cb268-7){RoaR} to {wow}-
```

# Gotchas and Tips

## Prefixing $ for variables

Some scripting languages like `bash` require a `$` prefix when you need the value stored in a variable. For example, if you declare `name='Joe'` you'd need `echo "$name"` to print the value. This may result in using `$` prefix and other bashisms in `awk` as well when you are a beginner. To make it a bit worse, `awk` has the `$N` syntax for accessing field contents, which could result in false comprehension that all variables need `$` prefix to access their values. See also [unix.stackexchange: Why does awk print the whole line when I want it to print a variable?](https://unix.stackexchange.com/q/291126/109046).

```
[](#cb269-1)$ # silently fails, $word becomes $0 because of string to numeric conversion
[](#cb269-2)$ awk -v word="cake" '$2==$word' table.txt
[](#cb269-3)$ # works when the variable is used correctly
[](#cb269-4)$ awk -v word="cake" '$2==word' table.txt
[](#cb269-5)blue cake mug shirt -7
[](#cb269-6)
[](#cb269-7)$ # here 'field' gets replaced with '2' and hence $2 is printed
[](#cb269-8)$ awk -v field=2 '{print $field}' table.txt
[](#cb269-9)bread
[](#cb269-10)cake
[](#cb269-11)banana
```

## Dos style line endings

As mentioned before, line endings differ from one platform to another. On Windows, it is typically a combination of carriage return and the newline character and referred as **dos style** line endings. Since `GNU awk` allows multicharacter `RS`, it is easy to handle. See [stackoverflow: Why does my tool output overwrite itself and how do I fix it?](https://stackoverflow.com/q/45772525/4082052) for a detailed discussion and various mitigation methods.

```
[](#cb270-1)$ # no issue with unix style line ending
[](#cb270-2)$ printf 'mat dog\n123 789\n' | awk '{print $2, $1}'
[](#cb270-3)dog mat
[](#cb270-4)789 123
[](#cb270-5)
[](#cb270-6)$ # dos style line ending causes trouble
[](#cb270-7)$ printf 'mat dog\r\n123 789\r\n' | awk '{print $2, $1}'
[](#cb270-8) mat
[](#cb270-9) 123
[](#cb270-10)$ printf 'mat dog\r\n123 789\r\n' | awk '{sub(/$/, ".")} 1'
[](#cb270-11).at dog
[](#cb270-12).23 789
[](#cb270-13)
[](#cb270-14)$ # use \r?\n if you want to handle both unix and dos style with same command
[](#cb270-15)$ # note that ORS would still be newline character only
[](#cb270-16)$ printf 'mat dog\r\n123 789\r\n' | awk -v RS='\r\n' '{print $2, $1}'
[](#cb270-17)dog mat
[](#cb270-18)789 123
[](#cb270-19)$ printf 'mat dog\r\n123 789\r\n' | awk -v RS='\r\n' '{sub(/$/, ".")} 1'
[](#cb270-20)mat dog.
[](#cb270-21)123 789.
```

## Behavior of ^ and $ when string contains newline

In some regular expression implementations, `^` matches the start of a line and `$` matches the end of a line (with newline as the line separator). In `awk`, these anchors always match the start of the entire string and end of the entire string respectively. This comes into play when `RS` is other than the newline character, or if you have a string value containing newline characters.

```
[](#cb271-1)$ # 'apple\n' doesn't match as there's newline character
[](#cb271-2)$ printf 'apple\n,mustard,grape,\nmango' | awk -v RS=, '/e$/'
[](#cb271-3)grape
[](#cb271-4)
[](#cb271-5)$ # '\nmango' doesn't match as there's newline character
[](#cb271-6)$ printf 'apple\n,mustard,grape,\nmango' | awk -v RS=, '/^m/'
[](#cb271-7)mustard
```

## Word boundary differences

The word boundary `\y` matches both start and end of word locations. Whereas, `\<` and `\>` match exactly the start and end of word locations respectively. This leads to cases where you have to choose which of these word boundaries to use depending on results desired. Consider `I have 12, he has 2!` as sample text, shown below as an image with vertical bars marking the word boundaries. The last character `!` doesn't have end of word boundary as it is not a word character.

![word boundary](media/file2.png)

```
[](#cb272-1)$ # \y matches both start and end of word boundaries
[](#cb272-2)$ # the first match here used starting boundary of 'I' and 'have'
[](#cb272-3)$ echo 'I have 12, he has 2!' | awk '{gsub(/\y..\y/, "[&]")} 1'
[](#cb272-4)[I ]have [12][, ][he] has[ 2]!
[](#cb272-5)
[](#cb272-6)$ # \< and \> only match the start and end word boundaries respectively
[](#cb272-7)$ echo 'I have 12, he has 2!' | awk '{gsub(/\<..\>/, "[&]")} 1'
[](#cb272-8)I have [12], [he] has 2!
```

Here's another example to show the difference between the two types of word boundaries.

```
[](#cb273-1)$ # add something to both start/end of word
[](#cb273-2)$ echo 'hi log_42 12b' | awk '{gsub(/\y/, ":")} 1'
[](#cb273-3):hi: :log_42: :12b:
[](#cb273-4)
[](#cb273-5)$ # add something only at start of word
[](#cb273-6)$ echo 'hi log_42 12b' | awk '{gsub(/\</, ":")} 1'
[](#cb273-7):hi :log_42 :12b
[](#cb273-8)
[](#cb273-9)$ # add something only at end of word
[](#cb273-10)$ echo 'hi log_42 12b' | awk '{gsub(/\>/, ":")} 1'
[](#cb273-11)hi: log_42: 12b:
```

## Relying on default initial value

Uninitialized variables are useful, but sometimes they don't translate well if you are converting a command from single file input to multiple files. You have to workout which ones would need a reset at the beginning of each file being processed.

```
[](#cb274-1)$ # step 1 - works for single file
[](#cb274-2)$ awk '{sum += $NF} END{print sum}' table.txt
[](#cb274-3)38.14
[](#cb274-4)
[](#cb274-5)$ # step 2 - prepare code to work for multiple file
[](#cb274-6)$ awk '{sum += $NF} ENDFILE{print FILENAME ":" sum}' table.txt
[](#cb274-7)table.txt:38.14
[](#cb274-8)
[](#cb274-9)$ # step 3 - check with multiple file input
[](#cb274-10)$ # oops, default numerical value '0' for sum works only once
[](#cb274-11)$ awk '{sum += $NF} ENDFILE{print FILENAME ":" sum}' table.txt marks.txt
[](#cb274-12)table.txt:38.14
[](#cb274-13)marks.txt:530.14
[](#cb274-14)
[](#cb274-15)$ # step 4 - correctly initialize variables
[](#cb274-16)$ awk '{sum += $NF} ENDFILE{print FILENAME ":" sum; sum=0}' table.txt marks.txt
[](#cb274-17)table.txt:38.14
[](#cb274-18)marks.txt:492
```

## Code in replacement section

The replacement section in substitution functions can accept any expression, converted to string whenever necessary. What happens if the regexp doesn't match the input string but the expression can change the value of a variable, such as increment/decrement operators? Well, the expression is still executed, which may or may not be what you need.

```
[](#cb275-1)$ # no match for second line, but 'c' was still modified
[](#cb275-2)$ awk '{sub(/^(br|ye)/, ++c ") &")} 1' table.txt
[](#cb275-3)1) brown bread mat hair 42
[](#cb275-4)blue cake mug shirt -7
[](#cb275-5)3) yellow banana window shoes 3.14
[](#cb275-6)
[](#cb275-7)$ # check for matching line first before applying substitution
[](#cb275-8)$ # that may help to simplify the regexp for substitution
[](#cb275-9)$ # or, you could save the regexp in a variable to avoid duplication
[](#cb275-10)$ awk '/^(br|ye)/{sub(/^/, ++c ") ")} 1' table.txt
[](#cb275-11)1) brown bread mat hair 42
[](#cb275-12)blue cake mug shirt -7
[](#cb275-13)2) yellow banana window shoes 3.14
```

Also, the expression is executed only once per function call, not for every match.

```
[](#cb276-1)$ # first line has two matches but 'c' is modified only once
[](#cb276-2)$ awk '{gsub(/\<b/, ++c ") &")} 1' table.txt
[](#cb276-3)1) brown 1) bread mat hair 42
[](#cb276-4)2) blue cake mug shirt -7
[](#cb276-5)yellow 3) banana window shoes 3.14
```

## Forcing numeric context

Use unary operator `+` to force numeric conversion. A variable might have numeric operations but still not get assigned a number if there's no input to read. So, when printing a variable that should be a number, use unary `+` to ensure it prints `0` instead of empty string.

```
[](#cb277-1)$ # numbers present in last column, no issues
[](#cb277-2)$ awk '{sum += $NF} END{print sum}' table.txt
[](#cb277-3)38.14
[](#cb277-4)$ # strings in first column, gets treated as 0
[](#cb277-5)$ awk '{sum += $1} END{print sum}' table.txt
[](#cb277-6)0
[](#cb277-7)
[](#cb277-8)$ # no input at all, empty string is printed
[](#cb277-9)$ awk '{sum += $1} END{print sum}' /dev/null
[](#cb277-10)
[](#cb277-11)$ # forced conversion to number, so that 0 is printed
[](#cb277-12)$ awk '{sum += $1} END{print +sum}' /dev/null
[](#cb277-13)0
```

## Forcing string context

Concatenate empty string to force string comparison.

```
[](#cb278-1)$ # parentheses around first argument to print used for clarity
[](#cb278-2)$ # fields get compared as numbers here
[](#cb278-3)$ echo '5 5.0' | awk '{print ($1==$2 ? "same" : "different"), "number"}'
[](#cb278-4)same number
[](#cb278-5)
[](#cb278-6)$ # fields get compared as strings here
[](#cb278-7)$ echo '5 5.0' | awk '{print ($1""==$2 ? "same" : "different"), "string"}'
[](#cb278-8)different string
```

## Negative NF

Manipulating `NF` sometimes leads to a negative value. Fortunately, `awk` throws an error instead of behaving like uninitialized variable.

```
[](#cb279-1)$ # file with different number of fields
[](#cb279-2)$ cat varying.txt
[](#cb279-3)parrot
[](#cb279-4)good cool awesome
[](#cb279-5)blue sky
[](#cb279-6)12 34 56 78 90
[](#cb279-7)
[](#cb279-8)$ # delete last two fields
[](#cb279-9)$ awk '{NF -= 2} 1' varying.txt
[](#cb279-10)awk: cmd. line:1: (FILENAME=varying.txt FNR=1) fatal: NF set to negative value
[](#cb279-11)
[](#cb279-12)$ # add a condition to check number of fields
[](#cb279-13)$ # assuming that lines with less than 3 fields should be preserved
[](#cb279-14)$ awk 'NF>2{NF -= 2} 1' varying.txt
[](#cb279-15)parrot
[](#cb279-16)good
[](#cb279-17)blue sky
[](#cb279-18)12 34 56
```

Here's another example, which needs to access third field from the end.

```
[](#cb280-1)$ awk '{print $(NF-2)}' varying.txt
[](#cb280-2)awk: cmd. line:1: (FILENAME=varying.txt FNR=1) fatal: attempt to access field -1
[](#cb280-3)
[](#cb280-4)$ # print only if there are minimum 3 fields
[](#cb280-5)$ awk 'NF>2{print $(NF-2)}' varying.txt
[](#cb280-6)good
[](#cb280-7)56
```

## Faster execution

Changing locale to ASCII (assuming current locale is not ASCII and the input file has only ASCII characters) can give significant speed boost. Using `mawk` is another way to speed up execution, provided you are not using `GNU awk` specific features. Among other feature differences, `mawk` doesn't support `{}` form of quantifiers, see [unix.stackexchange: How to specify regex quantifiers with mawk?](https://unix.stackexchange.com/q/506119/109046) for details. See also [wikipedia: awk Versions and implementations](https://en.wikipedia.org/wiki/AWK_programming_language#Versions_and_implementations).

```
[](#cb281-1)$ # time shown is best result from multiple runs
[](#cb281-2)$ # speed benefit will vary depending on computing resources, input, etc
[](#cb281-3)$ # /usr/share/dict/words contains dictionary words, one word per line
[](#cb281-4)$ time awk '/^([a-d][r-z]){3}$/' /usr/share/dict/words > f1
[](#cb281-5)real    0m0.029s
[](#cb281-6)
[](#cb281-7)$ time LC_ALL=C awk '/^([a-d][r-z]){3}$/' /usr/share/dict/words > f2
[](#cb281-8)real    0m0.022s
[](#cb281-9)
[](#cb281-10)$ time mawk '/^[a-d][r-z][a-d][r-z][a-d][r-z]$/' /usr/share/dict/words > f3
[](#cb281-11)real    0m0.009s
[](#cb281-12)
[](#cb281-13)$ # check that the results are same
[](#cb281-14)$ diff -s f1 f2
[](#cb281-15)Files f1 and f2 are identical
[](#cb281-16)$ diff -s f2 f3
[](#cb281-17)Files f2 and f3 are identical
[](#cb281-18)$ # clean up temporary files
[](#cb281-19)$ rm f[123]
```

Here's another example.

```
[](#cb282-1)$ # count words containing exactly 3 lowercase 'a'
[](#cb282-2)$ time awk -F'a' 'NF==4{cnt++} END{print +cnt}' /usr/share/dict/words
[](#cb282-3)1102
[](#cb282-4)real    0m0.034s
[](#cb282-5)
[](#cb282-6)$ time LC_ALL=C awk -F'a' 'NF==4{cnt++} END{print +cnt}' /usr/share/dict/words
[](#cb282-7)1102
[](#cb282-8)real    0m0.023s
[](#cb282-9)
[](#cb282-10)$ time mawk -F'a' 'NF==4{cnt++} END{print +cnt}' /usr/share/dict/words
[](#cb282-11)1102
[](#cb282-12)real    0m0.014s
```

# Further Reading

*   `man awk` and `info awk` and [online manual](https://www.gnu.org/software/gawk/manual/gawk.html)
*   Information about various implementations of `awk`
    *   [awk FAQ](http://www.faqs.org/faqs/computer-lang/awk/faq/) — great resource, but last modified *23 May 2002*
    *   [grymoire: awk tutorial](https://www.grymoire.com/Unix/Awk.html) — covers information about different `awk` versions as well
    *   [cheat sheet for awk/nawk/gawk](https://catonmat.net/ftp/awk.cheat.sheet.txt)
*   Q&A on stackoverflow/stackexchange are good source of learning material, good for practice exercises as well
    *   [awk Q&A on unix.stackexchange](https://unix.stackexchange.com/questions/tagged/awk?sort=votes&pageSize=15)
    *   [awk Q&A on stackoverflow](https://stackoverflow.com/questions/tagged/awk?sort=votes&pageSize=15)
*   Learn Regular Expressions (has information on flavors other than POSIX too)
    *   [regular-expressions](https://www.regular-expressions.info/) — tutorials and tools
    *   [rexegg](https://www.rexegg.com/) — tutorials, tricks and more
    *   [stackoverflow: What does this regex mean?](https://stackoverflow.com/q/22937618/4082052)
    *   [online regex tester and debugger](https://regex101.com/) — not fully suitable for cli tools, but most of the POSIX syntax works
*   [My repo on cli text processing tools](https://github.com/learnbyexample/Command-line-text-processing)
*   Related tools
    *   [GNU datamash](https://www.gnu.org/software/datamash/)
    *   [bioawk](https://github.com/lh3/bioawk)
    *   [frawk](https://github.com/ezrosent/frawk) — an efficient awk-like language, implemented in Rust
    *   [hawk](https://github.com/gelisam/hawk/blob/master/doc/README.md) — based on Haskell
    *   [miller](https://github.com/johnkerl/miller) — similar to awk/sed/cut/join/sort for name-indexed data such as CSV, TSV, and tabular JSON
        *   See this [news.ycombinator discussion](https://news.ycombinator.com/item?id=10066742) for other tools like this
*   miscellaneous
    *   [unix.stackexchange: When to use grep, sed, awk, perl, etc](https://unix.stackexchange.com/q/303044/109046)
    *   [awk-libs](https://github.com/e36freak/awk-libs) — lots of useful functions
    *   [awkaster](https://github.com/TheMozg/awk-raycaster) — Pseudo-3D shooter written completely in awk
    *   [awk REPL](https://awk.js.org/) — live editor on browser
*   ASCII reference and locale usage
    *   [ASCII code table](https://ascii.cl/)
    *   [wiki.archlinux: locale](https://wiki.archlinux.org/index.php/locale)
    *   [shellhacks: Define Locale and Language Settings](https://www.shellhacks.com/linux-define-locale-language-settings/)
*   examples for some of the topics not covered in this book
    *   [unix.stackexchange: rand/srand](https://unix.stackexchange.com/q/372816/109046)
    *   [unix.stackexchange: strftime](https://unix.stackexchange.com/q/224969/109046)
    *   [stackoverflow: arbitrary precision integer extension](https://stackoverflow.com/q/46904447/4082052)
    *   [stackoverflow: recognizing hexadecimal numbers](https://stackoverflow.com/q/3683110/4082052)
    *   [unix.stackexchange: sprintf and file close](https://unix.stackexchange.com/q/223727/109046)
    *   [unix.stackexchange: user defined functions and array passing](https://unix.stackexchange.com/q/72469/109046)
    *   [unix.stackexchange: rename csv files based on number of fields in header row](https://unix.stackexchange.com/q/408742/109046)
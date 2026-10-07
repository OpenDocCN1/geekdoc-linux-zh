# Chapter 7: Basic Tests 353

Run the following sequence of commands to see how to use the -o testing primitive to find out whether a shell option is set:

```
set -o noclobber
[[ -o noclobber ]] && print noclobber is set
set -o | grep noclobber
set +o noclobber
[[ -o noclobber ]] && print noclobber is set
set -o | grep noclobber
```

e) What does the sequence of commands here show about the -o testing primitive?

Strings and patterns are so important in shell programming that they will be covered separately in Chapter 10 "Patterns, Expansions, and Substitutions." However it's hard to avoid using them, so type the following commands as your introduction now to the way you can use the == and != primitives with simple strings:

```
[[ hello == "hello" ]] && print The strings are equal.
[[ hello != "good-bye" ]] && print The strings are not \
equal.
```

> Early versions of the shell used a single equal sign (=) to test whether two strings are equal, and the current version of the KornShell still recognizes it. However, you should always use the double equal sign in the scripts and functions you write because the single equal sign may not be supported for string comparisons in the future.

![](bbox=[0.44, 0.715, 0.138, 0.778])
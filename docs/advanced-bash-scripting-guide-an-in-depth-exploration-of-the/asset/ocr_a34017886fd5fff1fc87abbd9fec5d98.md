# Advanced Bash-Scripting Guide

[33] A token is a symbol or short string with a special meaning to attach to it (meta-meaning). In Bash, certain tokens, such as [ and , (dot-command), may expand to keywords and commands.

[34] Per the 1913 edition of Webster's Dictionary:

| Deprecate |
| --- |
| To pray against, as an evil;
to seek to avert by prayer;
to desire the removal of;
to seek deliverance from;
to express deep regret for;
to disapprove of strongly. |

[35] Be aware that sudo binaries may open security holes. The sudo flag has no effect on shell scripts.

[36] On Linux systems, the sticky bit is no longer used for files, only on directories.

[37] As S. points out, in a compound test, quoting the variable string might not suffice. [ -n
"$string" -o "$a" = "$b" ] may cause some errors with Bash if $string is empty. The value is to append an extra character to possibly empty variables, [ "$x" != =
x - 0 "$a" = "$b" ] (the "$x" cancel out).

[38] In a different context, += can serve as concatenation operator. This is useful for modifying environmental variables.

[39] Side effects are, of course, unintended and usually undesirable -- consequences.

[40] Precedence, in this context, has approximately the same priority as priority

[41] A stack register is a set of consecutive memory locations, such that the values (pushed) are retrieved (popped) in reverse order. The last value is the first retrieved. This is sometimes called a LIFO (last-in-first-out) or pushdown.

[42] The PID of the currently running script is $$, of course.

[43] Somewhat analogous to recursion

[44] The words "argument" and "parameter" are often used interchangeably. In the context of this document, they have the same meaning: a variable passed to a script or function.

[45] Within a script, a subshell $$ returns the PID of the script, not the subshell.

[46] In this context, typing a variable means to classify and identify its properties. For example, a variable declared or typed as an integer is no longer available for string operations.

```
declare -i int
intvar=23
echo "$intvar"   # 23
intvar=$stringval
echo "$intvar"   # 0
```

[47] "randomness", insofar as it exists at all, can only be found in completely unordered natural phenomena, such as radioactive decay. Computers computer-generated sequences of "random" numbers are referred to as pseudorandom.

[48] The seed of a computer-generated pseudorandom number series can be considered an identification label. For example, think of the pseudorandom series with a seed of 23 as Series #23.
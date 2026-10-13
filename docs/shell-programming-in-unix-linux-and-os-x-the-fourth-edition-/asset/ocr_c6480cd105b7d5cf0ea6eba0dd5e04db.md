Here’s an example:

```
```sh
$ PHONEBOOK=
$ : ${PHONEBOOK:?"No PHONEBOOK file"}
No PHONEBOOK file
$ : ${PHONEBOOK:?}
sh: PHONEBOOK: parameter null or not set
$
```
```

With this construct, you can easily check to see whether variables needed by a program are all set and not null:

```
```sh
: ${TOOLS:?}  ${EXPTOOLS:?}  ${TOOLBIN:?}
```
```

# `${parameter:+value}`

This one substitutes value if *parameter* is not null; otherwise, it substitutes nothing. It’s the opposite of `-`, of course.

```
```sh
$ traceopt=T
$ echo options: ${traceopt:+"trace mode"}
options: trace mode
$ traceopt=
$ echo options: ${traceopt:+"trace mode"}
options:
$
```
```

The *value* part for any of the constructs in this section can be a command substitution because it’s executed only if its value is required. This can get a bit complicated too. Consider this:

```
```sh
WORKDIR=${DBDIR:-$(pwd)}
```
```

Here WORKDIR is assigned the value of DBDIR if it’s not null, or the pwd command is executed and the result assigned to WORKDIR. pwd is executed *only if* DBDIR is null.

# Pattern Matching Constructs

The POSIX shell offers four parameter substitution constructs that perform pattern matching. Some really old shells do not support this feature, but it’s unlikely you’ll encounter one of them if you’re on a modern Unix, Linux, or Mac system.

The construct takes two arguments: a variable name (or parameter number) and a pattern. The shell searches through the contents of the specified variable to match the supplied pattern. If matched, the shell uses the value of the variable on the command line, with the *matching portion of the pattern deleted*. If the pattern is not matched, the entire contents of the variable are used on the command line. In both cases, the contents of the variable remain unchanged.

The term *pattern* is used here because the shell allows you to use the same pattern matching characters that it accepts in filename substitution and case values: `*` to match zero or more characters, `?` to match any single character, `[...]` to match any single character from the specified set, and `[...]` to match any single character not in the specified set.
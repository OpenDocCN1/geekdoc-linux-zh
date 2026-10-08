# ksh, rksh 595

You can assign the value of a variable in the following way:
name=value...

If the integer attribute, -i, is set for name, the value is subject to arithmetic evaluation as described below. Positional parameters, parameters denoted by a number, may be assigned with the special command. Parameter $0 is set from argument $ when the shell is invoked. If parameter is one or more digits, then it is a positional parameter. You must enclose a positional parameter of more than one digit in braces.

# Parameter Expansion

The format for parameter expansion is as follows:

```
$(expression)
```

where expression consists of all characters until the matching }. Any escaped by a backslash or within a quoted string, characters in embedded arithmetic expansions, command substitutions, and variable expansions are not examined in determining the

The simplest form for parameter expansion is:

```
$(parameter)
```

The value, if any, of parameter is substituted.
You can enclose the parameter name or symbol in braces, which are an optional except for positional parameters with more than one digit or when parameter is followed by a character that could be interpreted as part of the name. The matching closing brace is determined by counting brace levels, skipping over enclosed quoted strings and command substitutions.
You do not enclose the parameter name or symbol in braces, the expansion uses the longest valid name whether or not the symbol represented by name exists. When the shell is scanning its input to determine the boundaries of a name, it is not bound by its knowledge of what are already defined. For example, if F is a defined variable, the following command does not echo the value of $F followed by red.

```
echo $Fred
```

Instead, it selects the longest possible valid name, Fred, which may be unset.
If parameter expansion occurs inside double-quotes:

+   - Path name expansion is not performed on the results of the expansion.
- Field splitting is not performed on the results of the expansion, with the exception of $.

In addition, a value of word can be modified by one of the following formats.
in each case word is needed (based on the state of parameter, as described below), word is subject totilde expansion, parameter expansion, command substitution, and arithmetic expansion. If word is not needed, it is not expanded.
The ) character that delimits the following parameter expansion modifications is determined as described previously in this section. (For example, $(foo-bar) results in the expansion of foo followed by the string xyz if foo is set; otherwise, the expanded string is barxyz.)

```
$(parameter-word)
```

Default values. If parameter is unset or null, substitute the expansion of word otherwise, substitute the value of parameter.
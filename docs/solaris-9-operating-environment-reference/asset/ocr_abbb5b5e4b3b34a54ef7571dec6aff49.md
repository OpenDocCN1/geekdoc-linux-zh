# 1368 tabs

# Operands

n1,n2,... The arbitrary format consists of Tab-stop values separated with commas or spaces. The Tab-stop values must be positive decimal integers in ascending order. Up to 40 numbers are allowed. If you precede any number (except the first one) by a plus sign, take it as an increment to be added to the previous value. Thus, the formats 1,10,20,30, and 1,10,+10,+10 are considered identical.

# Examples

The following example uses the -code canned specification to set Tabs to the settings required by the IBM assembler, that is, columns 1, 10, 16, 36, 72.

```
castle% tabs -a
```

The following example uses the -n repetitive specification, where n is 8, to set Tabs every eight positions, that is, 1+(1*8), 1+(2*8),..., which evaluates to columns 9, 17....

```
castle% tabs -8
```

The following example uses the n1, n2, ... arbitrary specification to set Tabs at columns 1, 8, and 36.

```
castle% tabs 1,8,36
```

The following example uses the --file file specification to set Tabs, using the first line of $HOME/fspec.list/att4425 (see fspec(4)).

```
castle% --HOME/fspec.list/att4425
```

# Environment Variables

See attributes(5) for descriptions of the following environment variables that affect the execution of tabs: LC_CTYPE, LC_MAGES, and NLPATH.

TERM Determine the terminal type. If this variable is unset or null and you do not specify the -T option, use terminal type ansi-tabs.

# Exit Status

```
0 Successful completion.
>0 An error occurred.
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcu |
| CSI | Enabled |

# See Expand

```
expand(1), newform(1), pr(1), stty(1), tput(1), fspec(4), termino(4), attributes(5), environ(5), term(5)
```
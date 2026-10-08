# 456

# getopts

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNWcsu |
| CSI | Enabled |

# See Also

intro(1), getopts(1), sh(1), shell_builtins(1), getopt(3C), attributes(5)

# Diagnostics

getopts prints an error message on the standard error when it encounters an option letter not included in optstring.

# getopts — Parse Utility Options

# Synopsis

```
/usr/bin/getopts optstring name [arg...]
sh
getopts optstring name [argument...]
sh
getopts optstring name [arg...]
```

# Description

/usr/bin/getopts
You can use the getopts command to process command-line arguments and check for legal options. You use the getopts command in shell script loops to ensure standard syntax for command-line options.

Each time it is invoked, the getopts command puts the value of the next option in the shell variable specified by the name operand and the index of the next argument to be processed in the shell variable OPTIND. Whenever it is invoked, OPTIND is set to 1.

When the option requires an option-argument, the getopts command puts it in the shell variable OPTARG. If no option is found or if the option found does not have an option-argument, OPTARG is unset.

If an option character not contained in the optstring operand is found where an option is expected, the shell variable specified by name is set to the question-mark (?). If the first character in optstring is a colon (:), the shell variable is to the option character found but no output is written to standard error; otherwise, the shell variable OPTARG and a diagnostic message is written to standard error. This condition is considered to be an error detected in the ways arguments were presented to the invoking application but is not an error in getopts processing.

If an option-argument is missing, getopts handles it in the following:
In this example, the at sign version requires two separate `\s` formatting codes to display the array properly, one for each array item.

```
$ printf "\s \s\n" "${PRODUCTS[@]}"screwdrivers hammers
```

Multiple values can be assigned with a list in parentheses.

```
$ DIVISIONS=("North America" "Europe" "Far East")
$ printf "\s\n" "${DIVISIONS[*]}"
North America Europe Far East
```

The list items can have an optional subscript.

```
$ DIVISIONS=([3]="North America" [2]="Europe" [1]="Far East")
$ printf "\s\n" "${DIVISIONS[*]}"
Far East Europe North America
```

Combining a list with a `declare` command, arrays can be assigned values at the time they are created.

The number of items in the array is returned when `#` is used in front of the variable name with a position of `*` or `@`. The items need not be assigned consecutively and the number doesn’t reflect where the items are stored.

```
$ printf "\s\d" "${#PRODUCTS[*]}"
2
```

Individual array values can be removed with the `unset` command. Erasing a value by assigning the array position an empty string doesn’t destroy it: The empty string is still treated as an array item whenever the items are counted.

The `read` command can read a list into an array using an `-a` (`array`) switch. When this switch is used, each item on the line of input is read into a separate array position.

The `array` attribute is the only variable attribute that cannot be turned off after it is turned on. If Bash allowed the attribute to be turned off, the data in the array would be lost when the array became a normal variable.

# Exporting Variables and the Linux Environment

Shell variables exist in the script or interactive sessions only where they were declared. In order to make shell variables available outside of their place of origin, they have to be declared as *exportable*. Variables are marked as *exportable* with the `export` attribute using the `declare` `-x` (*export*) switch. The `export` attribute reminds the shell that you want to “export,” or provide the variable, to all programs run by the script.

For example, the program `cvs` requires a variable called `CVSROOT` to exist for all its programs.

```
$ declare -x CVSROOT="/home/cvs/cvsroot"
```
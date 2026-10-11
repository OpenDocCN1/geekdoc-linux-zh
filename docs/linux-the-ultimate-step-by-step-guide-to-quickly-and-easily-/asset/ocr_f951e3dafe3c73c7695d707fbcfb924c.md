```
```sh
#!/bin/sh
case $1
in
1) echo `First Choice`;;
2) echo `Second Choice`;;
*) echo `Other Choice`;;
esac
```
```

“1”, “2” and “*” are patterns, word is compared to each pattern and if a match is found the body of the corresponding pattern is executed, we have used “*” to represent everything, since this is checked last we will still catch “1” and “2” because they are checked first. In our example word is “$1”, the first parameter, hence if the script is ran with the argument “1” it will output “First Choice”, “2” “Second Choice” and anything else “Other Choice”. In this example we compared against numbers (essentially still a string comparison however) but the pattern can be more complex, see the SH man page for more information.

# # Functions

The syntax of an SH function is defined as follows:

```
```
name ( ) command
```
```

It is usually laid out like this:

```
```
name ( ) {
commands
}
```
```

A function will return with a default exit status of zero, one can return different exit statuses by using the notation return exit status. Variables can be defined locally within a function using local name=value. The example below shows the use of a user defined increment function:

# ## Increment Function Example

```
```sh
#!/bin/sh
inc() {
use it
# The increment is defined first so we can use it
	echo $($1 + $2))		# We echo the result of the first parameter
plus the second parameter
}
```
```
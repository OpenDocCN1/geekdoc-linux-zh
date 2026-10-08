# getopts 459

name The name of a shell variable that is set by the getopts command to the option character that was found.

The getopts command by default parses positional parameters passed to the invoking shell procedure. If you specify args, they are parsed instead of the positional parameters.

# Usage

Because getopts affects the current execution environment, it is generally provided as a shell built-in. If it is called in a shell or separate command-execution environment, such as one of the following:

```
(getopts abc "$@"
hup getopts...
find . -exec getopts... \
```

it does not affect the shell variables in the caller's environment.

> Note — Shell functions share OPTIND with the calling shell even though the positional parameters are changed. Functions that use getopts to parse their arguments usually want to save the value of OPTIND on entry and restore it before returning. However, there are cases when a function wants to change OPTIND for the calling shell.

# Examples

The following example script parses and displays its arguments.

```
aflag=
bflag=
while getopts ab: name
do
  case $name in
    a)
      aflag=1;
    b)
      bval="$OPTARG";
      printf " Usage: %s [-a] [-b] args\n"
  ?)
    exit 2;
nesac
done
if [ -z "$aflag" ]; then
  printf "Option -a specified\n"
fi
if [ -z "$bflag" ]; then
  printf 'Option -b %s specified\n' "$bval"
fi
shift $((OPTIND - 1))
printf "Remaining arguments: %s\n" "$*" **
```

The following fragment of a shell program shows how you could process the arguments for a command that can take the options -a or -b, as well as the option -o, which requires an option-argument.
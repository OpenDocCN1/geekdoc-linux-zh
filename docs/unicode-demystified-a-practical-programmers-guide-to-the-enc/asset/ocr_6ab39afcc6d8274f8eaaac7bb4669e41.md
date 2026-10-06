```
rcname()
{
  echo ${1},v
}
```

The rcname function appends ,v to the filename. The answer is written to standard output to enable you to use rcname inside a command substitution statement, such as
name=$(rcname oldname)

One function needs to check the command line arguments for validity. This function should ensure that exactly two arguments have been passed, that $1 names an existing directory, that $2 either does not exist or names an existing directory (not a plain file), and that neither argument is a prefix of the:

```
checkargs()
{
  if [[ $# != 2 ]]
  then
    print -u2 "usage: markers <source> <dest>"
    exit 1
  if [[ ! -d $1 ]]
  then
    print -u2 "$1: Not a directory"
    exit 1
  # Check second argument
  if [[ -a $2 && ! -d $2 ]]
  then
    print -u2 "$2: Not a directory"
    exit 1
  # Check that neither argument is a prefix of the other
  if [[ $1 = $2* || $2 = $1* ]]
  then
    print -u2 "Cannot create hierarchy below or above the other"
    exit 1
  return 0
}
```

You can invoke this function with a command such as "$@", which passes the command line arguments directly to checkargs.

The main part of the program uses find to locate the files and directories. The command find $source-print will write the pathname of each file in the hierarchy rooted at $source, one per line, to standard output. If you pipes this output into a loop and reads each pathname into a shell variable, the script can manipulate that variable as:

+   * Determine whether the pathname names a directory, a regular file, or something else.
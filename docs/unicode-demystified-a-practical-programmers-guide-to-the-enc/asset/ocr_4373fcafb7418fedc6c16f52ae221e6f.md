dxo -t indicates that getops should search for -d, -x, -o, -l, -t, and -r options and that the -o and -t options take arguments.

Using getops as the test-command in a control structure allows you to loop over the options one at a time. The getops checks the option list for options that are in optstring. Each time through loop, getops stores the option it finds in varname. By default getops uses the command line options. If you supply a list of arguments (arg) after varname, it uses instead.

The getops builtin uses the OPTIND (option index) and OPTARG (option argument) to store option-related values. When a shell script runs, the value of OPTIND locates an argument, it increments OPTIND to the index of the next option to be processed. If the option takes an argument, zsh assigns the value of the argument to OPTARG.

Suppose that you write a program that can take three options.

+   1. A -b indicates that your program should ignore whitespace at the start of input lines.
2. A -u followed by the name of a directory indicates that your program should use that directory for temporary files. Otherwise, it should use /tmp.
3. A -u option indicates that your program should translate all its output to uppercase.

In addition, the program should ignore all other options and end option processing when it encounters a --.

The problem is to write the portion of the program that determines which options the user has supplied. The following solution does not use getops:

```
SKIPBLANKS=
TMPDIR=/tmp
CASE=$$1"
while [[ "$1" = -* ]] # Remember, [[ = ]] does pattern match
do
  case $1 in
    -b)
      SKIPBLANKS=TRUE;
      if [ -d "$2" ]
        then
          TMPDIR=$2
          shift
        else
          print "$0: -t takes a directory argument." >&2
          exit 1
      fi;
    -u)
      CASE=upper;
      break ;; # Stop processing options
    *)
      print "$0: Invalid option $1 ignored." >&2;
  esac
done
```
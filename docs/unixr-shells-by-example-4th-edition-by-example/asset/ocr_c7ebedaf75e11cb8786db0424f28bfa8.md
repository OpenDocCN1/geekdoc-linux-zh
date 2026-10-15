# EXPLANATION (CONTINUED)

3 If the options variable is assigned the question mark, the case statement is executed. The question mark is protected with the backslash so that the shell does not see it as a wildcard and try to perform filename substitution.

4 g is not a legal option. A question mark is assigned to the variable options and the error message is displayed.

5 c is not a legal option. A question mark is assigned to the variable options and the error message is displayed.

Special getopts Variables. The getopts function provides two variables to help keep track of arguments: OPTIND and OPTARG. OPTIND is a special variable that is initialized to one and is incremented each time getopts completes processing a command-line argument to the number of the next argument getopts will process. The OPTARG variable contains the value of a legal argument. See Examples 14.74 and 14.75.

# EXAMPLE 14.74

```
(The Script)
#!/bin/bash
# Program: opts3
# Using getopts -- Third try --

1 while getopts dq: options
do
  case $options in
 2 d) echo "-d is a valid switch" ;;
 3 q) echo "The argument for -q is $OPTARG";;
 \?) echo "Usage:opts3 -dq filename ..." 1>&2;;
esac
done

(The Command Line)
4 $ opts3 -d
 -d is a valid switch
5 $ opts3 -q foo
 The argument for -q is foo
6 $ opts3 -q
Usage:opts3 -dq filename ...
7 $ opts3 -e
Usage:opts3 -dq filename ...
8 $ opts3 e
```
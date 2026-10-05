# 1026 CHAPTER 27 PROGRAMMING THE BOURNE AGAIN SHELL

makepath

```
# This is a function
# Enter it on the keyboard, do not run it as a shell script
#
function makepath() {
  if [[ ${${1}- -eq 0 || "$1" ]]
    then
      return 0 # Do nothing
  fi
  if [ "\${1%/*}" = "$1" ]
    then
      mkdir $$
      makepath ${11%/*}} || return $1
      mkdir $$
      return $$
  fi
}
```

In the test for a simple component (the if statement in the middle of the function), the left expression is the argument after the shortest suffix that starts with a / character has been stripped away (page 1018). If there is no such character (example, if $1 is max), nothing is stripped off and the two sides are equal. If the argument is a filename preceded by a slash, such as /usr, the expression /* evaluates to a null string. To make the function work in this case, you must take two precautions: Put the expression within quotation marks and ensure that the recursive function handles sensibly when it is passed a null string as an argument. In general, good programs are robust: They should be prepared for borderline, invalid, or meaningless input and behave appropriately in such cases.

By giving the following command from the shell you are working in, you turn on debugging tracing so that you can watch the recursion:

```
$ set -o xtrace
```

(Give the same command, replace the hyphen with a plus sign (+) to debugging off). With debugging turned on, the shell displays each line in expanded format as it executes the line. A+ precedes each line of debugging output.

In the following example, the first line that starts with + the shell calling makepath. The makepath function is initially called from the command line with arguments of a/b/c. It calls itself using arguments of a/b and finally a. All work is done (using mkdir) as each call to makepath returns.

```
$ /makepath a/b/c
+ makepath a/b/c
+ [[ 5 -eq 0 ]]
+ [[ -d a/b/c ]]
+ [[ a/b = \a\/b\c ]]
+ makepath a/b
+ [[ 3 -eq 0 ]]
+ [[ -d a/b ]]
+ [[ a = \a\/b ]]
```
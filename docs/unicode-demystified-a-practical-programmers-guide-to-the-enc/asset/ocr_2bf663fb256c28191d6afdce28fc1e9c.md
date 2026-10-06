# Always Test the Arguments

To keep the examples in this code and subsequent chapters short and focused on specific concepts, the code to verify arguments is often omitted or abbreviated. It is a good practice to include tests for argument verification in your shell programs. Doing so will result in scripts that are easier to run and debug.

The following example, another version of chk, checks for arguments in a way that is more traditional for GNU/Linux shell scripts. The example uses the bracket ([]) synonym for test. Rather than using the word test in scripts, you can surround the arguments to test with chkargs, as shown. The brackets must be surrounded by whitespace (SPACES or Tabs).

```
$ chkargs
if [ $# -eq 0 ]
then
    echo "Usage: chkargs argument..." 1>&2
    exit 1
fi
echo "Program running.
exit 0
$ chkargs
Usage: chkargs arguments
$ chkargs abc
Program running.
```

The error message that chkargs displays is called a usage message and uses the 1>&2 to redirect its output to standard error (page 552). After issuing the usage message, chkargs exits with an exit status of 1, indicating that an error has occurred. The exit 0 command at the end of the script causes chkargs to exit with a 0 status after the program runs without an error.

The usage message is a common notification to specify the type and number of arguments the script takes. Many GNU/Linux utilities provide usage messages similar to the one in chkargs. When you call a utility or other program with the wrong number or kind of arguments, you often see a usage message. Following is the usage message that cp displays when you call it without any arguments:

```
$ cp
cp: missing file arguments
Try 'cp --help' for more information.
```

# if...then...else

The introduction of the else statement turns the if structure into the two-way branch shown in Figure 13-2. The syntax of the if...then...else control structure is
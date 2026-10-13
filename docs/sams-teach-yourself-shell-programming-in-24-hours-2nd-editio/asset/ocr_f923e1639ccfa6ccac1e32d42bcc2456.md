```
if [ "$VERBOSE" = "true" ] ; then
    MSG="Failed"
    if [ $RET -eq 0 ] ; then
        MSG="Done."
    fi
    echo $MSG
fi
exit 0
```

Assuming this script is called uu, you can use it to uuencode files in all of the following ways:

uu ch13.doc
u -f ch13.doc
u -f ch13.doc -o ch13.uu

In each of the preceding commands, file ch13.doc is uuencoded. The last command places the result into the file ch13.uu instead of the default ch13.doc.uu; this might be required if the document needs to be used on a DOS or Windows system.

Because this script uses getopts, any of the commands given previously can run in verbose mode by simply specifying the -v option.

# Summary

In this chapter, you examined how to deal with arguments and options in shell script.

Specifically you looked at the following methods:

+   - Manually handling arguments and options using a case statement
+   - Handling options using getopts

You worked through two examples that illustrate the implementation and rationale behind each method. In addition, you saw several special variables that pertain to arguments and command execution.

As you will see in later chapters, using options greatly increases the flexibility and the reusability of your shell scripts.

# Questions

1. Add tar file extraction to the nytar script.
Assume that the -x option indicates that the user wants to extract tar files and that the correct value of TARGS for extracting tar files is -xvf.
# Special Patterns

Patterns in AWK can have many forms. There are conditional expressions like we have just seen. There are also regular expressions, as we would expect. There are two special patterns called BEGIN and END. The BEGIN pattern carries out its corresponding action before the first record is read. This is useful for initializing variables, or printing headers at the beginning of output. Likewise, the END pattern performs its corresponding action after the last record is read from the input file. This is good for outputting summaries once the input has been processed.

Let's try a more elaborate example. We'll assume for the moment that the directory does not contain any files with embedded spaces (though this is never a safe assumption). We could use the following script to list symbolic links:

```
#!/bin/bash

# Print a directory report
s -l /usr/bin | awk '
BEGIN {
    print "Directory Report"
    print "===================="
}

NF > 9 {
    print $9, "is a symbolic link to", $NF
}

END {
    print "===================="
    print "End Of Report"
}'
```

In this example, we have 3 pattern/action pairs in our AWK program. The first is a BEGIN pattern and its action prints the report header. We can spread the action over several lines, though the opening brace “{” of the action must appear on the same line as the pattern.

The second pattern tests the current record to see if it contains more than 9 fields, and if true, the 9th field is printed, followed by some text and the final field in the record. Notice how this was done. The NF variable is preceded by a “$”, thus it refers to the NFth field rather than the value of NF itself.

Lastly, we have an END pattern. Its corresponding prints the “End Of Report” message once all the lines of input have been read.
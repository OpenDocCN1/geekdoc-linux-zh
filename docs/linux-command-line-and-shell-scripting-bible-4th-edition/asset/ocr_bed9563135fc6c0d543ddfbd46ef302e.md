```
$ ./NeededFunctionCheck.sh CheckMe.sh TempFile.txt
  echo"Usage: ./CheckMe.shparameter1parameter2"
  echo"Exittingscript.."
  exit
rm: remove regular file 'TempFile.txt'? Y
  $
```

This is a little harder to read, because we eliminated *all* the spaces within each script line. (One script improvement you can make is to only remove multiple spaces between characters.) However, it gives us enough of a shove in the right direction. We know that these three lines are repeated within the script. And the script needs to be reviewed to possibly replace the repeated commands with a function.

You can make lots of potential improvements within this script. Once you’ve got your modifications in place and working, remove that temporary file to make it faster. How about producing line numbers to show where the code is located within the script? You could even make the information into a fancy report...but we recommend you wait until you read through the next chapter, “Advanced *gawk*, ” before you try that script improvement.

# Summary

The *sed* editor provides some advanced features that allow you to work with text patterns across multiple lines. This chapter showed you how to use the multiline next (N) command to retrieve the next line in a data stream and place it in the pattern space. Once it’s in the pattern space, you can perform complex substitution (s) commands to replace phrases that span more than one line of text.

The multiline delete (d) command allows you to remove the first line when the pattern space contains two or more lines. This is a convenient way to iterate through multiple lines in the data stream. Similarly, the multiline print (P) command allows you to print just the first line when the pattern space contains two or more lines of text. The combination of the multiline commands allows you to iterate through the data stream and create a multiline substitution system.

Next, we covered the hold space. The hold space allows you to set aside
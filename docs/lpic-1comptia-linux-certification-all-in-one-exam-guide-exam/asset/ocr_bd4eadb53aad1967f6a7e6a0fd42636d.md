```
declare -1 B.....
declare -1 C......
declare -1 ANSWER
echo "Enter the first number:"
read A
echo "Enter the second number:"
read B
echo "Enter the third number:"
read C
echo "What would you like to do with these numbers?"
echo "F: Add them up!"
echo "V: Average them!"
echo "Enter your choice:"
read CHOICE in
case $CHOICE in
    P|p) ANSWER=A+B+C
        ;;
    V|v) ANSWER=A+B+C
        ANSWER=$ANSWER/3
        ;;
esac
echo "Your answer is" $ANSWER "."
exit 0
```

+   5. Save your changes to the script and exit vi.
+   6. Make the script executable by the file owner by entering `chmod u+x domath` at the shell prompt.
+   7. Test the script by entering `domath` at the shell prompt.
+   8. Test the script and verify that it works.

# # Processing Text Streams

When processing text streams within a script or when piping output at the shell prompt, there may be times when you need to filter the output of one command so that only certain portions of the text stream are actually passed along to the stdin of the next command. There are a variety of tools you can use to do this. In the last part of this chapter, we'll look at using the following commands:

+   • cut
+   • expand and unexpand
+   • fmt
+   • join and paste
+   • nl
+   • od
+   • pr
+   • sed and awk
+   • sort
+   • split
+   • tr
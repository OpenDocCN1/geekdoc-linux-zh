```
fi
cursor 12 33; read looptest
if [ "$looptest" = 'q' ]
then { clear; exit; }
done
```

+   2. Save the file and exit the editor. Give the file execute permission and run it. Test the program by adding the following employees:
219-555-7175 Mullins Allen L 7527 Sales Rep 09-12-2000
219-555-7176 Albertson Jeannette K 5547 DC Clerk
09-12-2000

+   3. Now run the phmenu script and select A from the menu to execute the phone and script. Add another record to the file and then quit the program.

Your screen should look similar to Figure 6-11. (Note that the program shows only one person's information at a time.)

![](bbox=[0.19, 0.43, 0.77, 0.75])

**Figure 6-11**: Phoneadd script screen

You created the shell script for the corporate phones application. However, you still need to address several deficiencies. For example, how can you return to a previous field as you enter the data? What happens when you enter the same employee twice? What happens if you assign a new employee a phone number that has already been assigned to someone else? Chapter 7, “Advanced Shell Programming,” addresses these issues.
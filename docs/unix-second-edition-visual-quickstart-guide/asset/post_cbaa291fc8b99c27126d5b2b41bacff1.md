
## Looping Your Scripts

Suppose you've created a script that you'd like to apply to several files. For example, say that at the end of each day you need to make backup copies of all .html files in your www directory. You could make a backup of each individual .html file, but that's a lot of work. An easier way would be to create a short script to copy an .html file, and then loop the script to apply to all .html files in your www directory (Figure 10.5). You create one short script; Unix does the tedious work for you.

### To make a loop:

1. <code>vi head_ache</code>

   At the shell prompt, start your editor and open the script you want to loop. In this case, we're using vi and the head_ache file. (Of course, you could name the script html-backup or something mundane like that.)

2. <code>#!/bin/sh</code>

   Tell your Unix system which shell to use to run the shell script. In this example, we're telling it (with #!) to run the shell script with /bin/sh.

3. <code>cd ~/www</code>

   Make sure that you're in the directory in which the loop will take place. In this example, our shell script resides in our home directory, but the files to which the loop will apply reside in the www directory.

4. <code>for i in `ls -1 *.html`</code>

   OK, don't panic. Read this as: "Look for items in the list of .html files." In this code, we're providing the output of the embedded command (`ls -1 *.html`) to the for loop (the .html files), as shown in Figure 10.5. The -1 flag on the ls command, by the way, forces a single list of output, which is ideal for script use, rather than several columns, which is easy to read onscreen but doesn't work well for scripts.

![](img/6ffd6bb320ccf354f5a4d57c9d95190d_228_0.png)

Figure 10.5 Using a loop with an embedded command, you can automatically apply a script to several files.

```
[ej@hobbes scripting]$ more head_ache
#!/bin/sh
cd ~/www
for i in `ls -1 *.html`
do
cp $i $i.bak
echo "$i backed up!"
done

[ej@hobbes scripting]$ ./head_ache
above.html backed up!
file1.html backed up!
html.html backed up!
reference.html backed up!
temp.html backed up!
[ej@hobbes scripting]$
```

Code Listing 10.4 This loop reports progress as it backs up each file.

Loops are particularly handy for searching and replacing throughout multiple documents. For example, if you're the new Webmaster and want to replace the old Webmaster's name at the bottom of all .html files with your name, you can do so using a loop with sed. Check out Chapter 6 for more information about sed, which will help with complex searches, and Chapter 17, which introduces sed to loops.

5. <code>do</code>

   On the line immediately after the for statement, type do. This tells the Unix system that the following information will be the loop to apply.

6. <code>cp $i $i.bak</code>

   Here, we copy (cp) the specified items ($i) to a backup file ($i.bak)—that is, one backup file per file copied. So, if you have 72 .html files to begin with, you'll end up with those original 72, plus 72 new backup files.

7. <code>echo "$i backed up!"</code>

   Add echo "$i backed up!" so that the system displays onscreen what it has done.

8. <code>done</code>

   On the next line, announce that you're done with the loop.

9. Save it, make it executable, and try it out.

   This example script will make backup copies of all .html files in the www directory, as in Code Listing 10.4.

### Tips

Loop instructions can be much more complex. For example, you could make a loop to spell-check each of the chapter files in the directory and report how many misspelled words there are in each file. To do that, use this line in the loop: <code>echo -e "$i has \t `cat $i | spell | wc -l` misspelled words"</code>. Here again just build the loop one step at a time.

```
[ejr@hobbes scripting]$ ./deef
Greetings!  Say, you're looking mighty sharp today!

You were most recently working on scripting/.
Nope, no feedback yet
[ejr@hobbes scripting]$ touch feedback
[ejr@hobbes scripting]$ ./deef
Greetings!  Say, you're looking mighty sharp today!

You were most recently working on scripting/.
There's feedback on the latest project
[ejr@hobbes scripting]$
```

Code Listing 10.5 The last line produced by the feedback script differs, depending on the files found.

2. <code>if ls | grep feedback > /dev/null</code>

   Start the line with if, and then follow it with the conditional statement, in this case `ls | grep feedback`. Read this as: "List the files in the current directory and search for a file named feedback. If that file exists, then the expression is true." The redirection to /dev/null just discards the output from grep; you care about the answer to the test but not the specific lines found or not found. (See the whole script in Figure 10.6.)

3. <code>then echo "There's feedback on the latest project"</code>

   On the line immediately after the if statement, enter the command to be carried out or message to be displayed if the if statement is true. In this example, a true if statement would result in "There's feedback on the latest project" being printed onscreen.

4. <code>else echo "Nope, no feedback yet"</code>

   On the next line, use else followed by a statement specifying what should happen if the if statement is false. Here, we specify that "Nope, no feedback yet" would be printed onscreen if the feedback file was not found or had nothing in it.

5. <code>fi</code>

   Immediately after the else statement, announce that you're finished with fi.

6. Save the script and try it out.

   In this example, the script will check to see if feedback exists and print a different message depending on what it finds (Code Listing 10.5)

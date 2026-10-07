Several books are available that illustrate the use of awk. A popular one is *Sed & Awk* ( *Nutshell Handbook* ), by Dale Dougherty and Arnold Robbins (O’Reilly, 1997). The awk utility, or the GNU version called GAWK, is included with most Linux distributions and available for most flavors of Unix.

# sed

sed is a stream editor, hence the name. It allows for the search and replacement of regular expressions and more—a valuable capability when the task at hand involves updating a file. You can use sed to automate the update of a text file by searching for a string and changing it as required. It is also quite useful when you need to change the output of a command before piping it into another command. If you have ever issued a command such as :s/phrase/newphrase/ to replace one phrase with another within an editor, then you know how to use sed commands. When using sed, however, this change is automatically applied globally because sed works on each line in the file.

sed can be executed with the actions as a command–line argument. It is sometimes beneficial to do this if, for example, the output of a very long file needs slight alteration so that it can be printed to a new file in the format requested by the boss. Here is a fairly simple example:

```
$ cat /tmp/calendar |sed -e 's/Jan/uuary/' | sed -e 's/Feb/uuary/' |
$    sed -e 's/Mar/ich/' | sed -e 's/Apr/il/' | sed -e 's/Jun/e/' |
$    sed -e 's/Jul/y/' > newfile
```

In this example, a calendar file containing dates within the first seven months of the year needs to be altered so that the abbreviated month name is replaced by the full name of that month. The edited calendar is to be written out to newfile. First we cat the file into our sequence of sed commands. The –e tells sed that the next thing is a sed command to be executed. This command’s placement within single tick marks distinguishes it from the rest of the line. The s means that we wish to substitute the second phrase for the first. Thus this command line meets our file–alteration needs, its length well justified when it saves many keystrokes in a file with say, 1000 lines.

Like awk, the sed command is included with most Linux distributions and available for most flavors of Unix.

# System Initialization Scripts

Often when you are using some recently developed utility, you need to start the utility at boot time and aren’t able to depend upon an existing script to do this. For these situations, you need to write your own initialization script and add it to the initialization scripts that we discussed in Chapter 3, “Startup and Shutdown.” This is actually quite easy to do if you follow the example of an existing script. These scripts are all Bash shell scripts and share a common format.

# Writing an Initialization Script

Let’s say that you have downloaded a tarball of mynewutility from an Internet site. Obviously, there is no mynewutility script in the /etc/rc.d hierarchy, since the utility isn’t part of the standard distribution. When you have finished installing the utility and configuring it, you’ll probably want to make it start at boot time like the other daemons in the /etc/rc.d hierarchy. To accomplish this, you’ll need to write an *initialization script* to manage the new utility.
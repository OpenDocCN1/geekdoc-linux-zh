
```
if [ $desired -lt 1 ] ; then
echo "$0: Restore canceled by user." >&2
exit 1
fi

restore="$(ls -tdi *$1 | sed -n "$({desired}p)")"

if [ -e "$dest/$1" ] ; then
echo "\"$1\" already exists in this directory. Cannot overwrite." >&2
exit 1
fi

/bin/echo -n "Restoring file \"$1\" ..."
$move "$restore" "$dest/$1"
echo "Done."

/bin/echo -n "Delete the additional copies of this file? [y] "
read answer

if [ ${answer:=y} = "y" ] ; then
$realrm -rf *$1
echo "Deleted."
else
echo "Additional copies retained."
fi
else
if [ -e "$dest/$1" ] ; then
echo "\"$1\" already exists in this directory. Cannot overwrite." >&2
exit 1
fi

restore="$(ls -d *$1)"

/bin/echo -n "Restoring file \"$1\" ..."
$move "$restore" "$dest/$1"
echo "Done."
fi

exit 0
```

Listing 2-7. The unzm shell script for restoring backed-up files

## How It Works

The first chunk of code at ①, the if [$# -eq 0] conditional block, executes if no arguments are specified, displaying the contents of the deleted files archive. However, there’s a catch: we don’t want to show the user the timestamp data we added to the filenames since that’s only for the script’s internal use. It would just clutter up the output. In order to display this data in a more attractive format, the sed statement at ② deletes the first five occurrences of digit digit dot in the ls output.

The user can specify the name of the file or directory to recover as an argument. The next step at ⑤ is to ascertain how many matches there are for the name provided.

The unusual use of nested double quotes in this line (around $1) is to ensure ls matches filenames with embedded spaces, while the * wildcard expands the match to include any preceding timestamp. The 2> /dev/null sequence is used to discard any error resulting from the command instead of showing it to the user. The errors being discarded will most likely be No such file or directory, when the specified filename isn't found.

If there are multiple matches for the given file or directory name, then the most complex part of this script, the if [ $matches -gt 1 ] block at ⑥, is executed and displays all the results. Using the -t flag for the ls command in the main for loop causes the archive files to be presented from newest to oldest, and at ⑦, a succinct call to the awk command translates the timestamp portion of the filename into a deletion date and time in parentheses. In the size calculation at ⑧, the inclusion of the -k flag to ls forces the file sizes to be represented in kilobytes.

Rather than displaying the size of matching directory entries, the script displays the number of files within each matching directory, which is a more helpful statistic. The number of entries within a directory is easy to calculate. At ⑨ we just count the number of lines given by ls and strip any spaces out of the wc output.

Once the user specifies one of the possible matching files or directories, the exact file is identified at ⑩. This statement contains a slightly different use of sed. Specifying the -n flag with a line number (${desired}) followed by the p (print) command is a very fast way to extract only the specified line from the input stream. Want to see only line 37? The command sed -n 37p does just that.

Then there's a test at ⑪ to ensure that unrm isn't going to step on an existing copy of the file, and the file or directory is restored with a call to /bin/mv. Once that's finished, the user is given a chance to remove the additional (probably superfluous) copies of the file ⑫, and the script is done.

Note that using ls with "*$1" matches any filenames ending with the value in $1, so the list of multiple "matching files" may contain more than just the file the user wants to restore. For instance, if the deleted files directory contains the files 11.txt and 111.txt, running unrm 11.txt would signal that it found multiple matches and return listings for both 11.txt and 111.txt. While that might be okay, once the user chooses to restore the correct file (11.txt), accepting the prompt to delete additional copies of the file would also remove 111.txt. Therefore, defaulting to delete under those circumstances might not be optimal. However, this could be easily overcome by using the ??.??,??,??,??,"*$1" pattern instead, if you kept the same timestamp format for newrm as shown in Script #15 on page 55.

## Running the Script

There are two ways to run this script. Without any arguments, the script will show a listing of all files and directories in the user's deleted files archive.

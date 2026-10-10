
## Removing HTML tags

These days, it’s not uncommon to download text from a website to save or use as data in an application. Sometimes, however, when you download text from the website, you also get the HTML tags used to format the data. This can be a problem when all you want to see is the data.

A standard HTML web page contains several different types of HTML tags, identifying formatting features required to properly display the page information. Here’s a sample of what an HTML file looks like:

```bash
$ cat data11.txt
<html>
<head>
<title>This is the page title</title>
</head>
<body>
<p>
This is the first line in the Web page.
This should provide some useful
information to use in our sed script.
</body>
</html>
$
```

HTML tags are identified by the less-than and greater-than symbols. Most HTML tags come in pairs. One tag starts the formatting process (for example, `<b>` for bolding), and another tag stops the formatting process (for example, `</b>` to turn off bolding).

Removing HTML tags creates a problem, however, if you’re not careful. At first glance, you’d think that the way to remove HTML tags would be to just look for a text string that starts with a less-than symbol (`<`), ends with a greater-than symbol (`>`), and has data in between the symbols:

```bash
s/</.*>//g
```

Unfortunately, this command has some unintended consequences:

```bash
$ sed 's/</.*>//g' data11.txt
```

This is the line in the Web page.
This should provide some
information to use in our sed script.

$

Notice that the title text is missing, along with the text that was bolded and italicized. The sed editor literally interpreted the script to mean any text between the less-than and greater-than sign, including other less-than and greater-than signs! Each time the text was enclosed in HTML tags (such as `<b>first</b>`), the sed script removed the entire text.

The solution to this problem is to have the sed editor ignore any embedded greater-than signs between the original tags. To do that, you can create a character class that negates the greater-than sign. This changes the script to

```bash
s/<[^>]*>//g
```

This script now works properly, displaying the data you need to see from the web page HTML code:

```bash
$ sed 's/<[^>]*>//g' data11.txt
```

This is the page title

This is the first line in the web page.
This should provide some useful
information to use in our sed script.

$

That's a little better. To clean things up some, we can add a delete command to get rid of those pesky blank lines:

```bash
$ sed 's/[<>]*>//g ; /^$/d' data11.txt
This is the page title
This is the first line in the Web page.
This should provide some useful
information to use in our sed script.
$
```

Now that's much more compact; there's only the data you need to see.

# Working Through a Practical Example

For our practical example in this chapter, we'll use sed to scan Bash shell scripts. The purpose of this scan is to find commands that may be better off located within a function.

Back in [Chapter 17](#), “Creating Functions,” we covered how to set up functions that can be called multiple times within a script. It's considered good form to put any duplicated code blocks within a function. That way, if a change is needed for the commands in the code block, you need to make those changes in only one place. Not only is this approach a time-saver, but it also reduces the chances of introducing errors that may occur if you change one block of code but not the others strewn about the script.

To keep things simple, we'll just look for three repeating lines of code within a file. Consider the following text file:

```bash
$ cat ScriptData.txt
Line 1
Line 2
Line 3
Line 4
Line 5
Line 6
Line 3
Line 4
Line 5
Line 7
Line 8
Line 3
Line 4
Line 5
Line 9
Line 10
Line 11
Line 12
$
```

If you look carefully, you’ll notice that `Line 3`, `Line 4`, and `Line 5` are repeated three times throughout this file. To find those repeated lines, we’ll merge each text line together with the next two following lines:

- 1. Read in the next line, but only if processing the text file’s first line, using the multiline `N` command.
- 2. Read in the next line (this is the second read for the text file’s first line) using the multiline `N` command. Now we have three lines within the pattern space.
- 3. Print the pattern space to `STDOUT`.
- 4. Delete the first line in the pattern space using the `D` command, which deletes the text within the pattern space up to and including the first newline, and then starts processing the `sed` script commands from the beginning.

The following command shows this process:

```bash
$ sed -n '{
> 1N
> N
> P
> D}
> ' ScriptData.txt
Line 1
Line 2
Line 3
Line 2
Line 3
Line 4
Line 3
Line 4
Line 5
Line 4
Line 5
Line 6
Line 5
Line 6
Line 3
Line 6
Line 3
Line 4
Line 3
Line 4
Line 5
Line 4
Line 5
Line 5
[...]
Line 9
Line 10
Line 9
Line 10
Line 11
Line 10
Line 11
Line 12
$
```

The problem with this method is that it is hard for a human to differentiate what lines have been merged together. Because the lines still contain the newline character (\n), the output is nearly impossible to interpret.

To fix this issue, we'll replace the newline character at the end of each text line with a bell sound character (\a) using the substitute (s) command:

```bash
$ sed -n '{
> 1N
> N
> s/\n/\a/g
> p
> s/\a/\n/
> D}' ScriptData.txt
Line 1Line 2Line 3
Line 2Line 3Line 4
Line 3Line 4Line 5
Line 4Line 5Line 6
Line 5Line 6Line 3
Line 6Line 3Line 4
Line 3Line 4Line 5
Line 4Line 5Line 7
Line 5Line 7Line 8
Line 7Line 8Line 3
Line 8Line 3Line 4
Line 3Line 4Line 5
Line 4Line 5Line 9
Line 5Line 9Line 10
Line 9Line 10Line 11
Line 10Line 11Line 12
$
```

Now, we're getting somewhere! Notice that although we replaced the newline characters with a bell sound character (globally) in the third line of the sed script, after printing the pattern space we had to switch the first bell sound character back to a newline. This is due to the delete (d) command, which needs the newline character after the first text line so that it won't delete the entire pattern space.

While it may be tempting to forge ahead to comparing the lines and finding duplicates, there is one more consideration. Shell script lines often have spaces or tabs within each line, as shown in this test text file:

```bash
$ cat ScriptDataB.txt
 Line 1
Line 2
Line 3
Line 4
   Line 5
Line 6
      Line 3
   Line 4
   Line 5
Line 7
Line 8
      Line 3
   Line 4
      Line 5

Line 9
Line 10
Line 11
Line 12
$
```

These spaces and tabs will disrupt the matching process. But it's fairly easy to handle this situation. We'll just eliminate the spaces and tabs via a global (g) substitute (s) command:

```bash
$ sed -n '{
> 1N
> N
> s/ / /g
> s/\\t/\\/g
> s/\\n/\\a/g
> p
> s/\\a/\\n/
> D}
> ' ScriptDataB.txt
Line1Line2Line3
Line2Line3Line4
Line3Line4Line5
Line4Line5Line6
Line5Line6Line3
Line6Line3Line4
Line3Line4Line5
Line4Line5Line7
Line5Line7Line8
Line7Line8Line3
Line8Line3Line4
Line3Line4Line5
Line4Line5Line9
Line5Line9Line10
Line9Line10Line11
Line10Line11Line12
$
```

Now we'll employ two other Bash shell commands to help us sort the file (sort) and find any duplicates (uniq -d):

```bash
$ sed -n '{
> 1N;
> N;
> s// /g;
> s/\\t/\\/g;
> s/\\n/\\a/g;
> p
> s/\\a/\\n/;
> D}
> ' ScriptDataB.txt |
> sort | uniq -d |
> sed 's/\\a/\\n/g'
Line3
Line4
Line5
$
```

Perfect! The commands scanned the file and found three repeating lines. Now we can prettify this up, and store it in a shell wrapper. Here’s one way to do it:

```bash
$ cat NeededFunctionCheck.sh
#!/bin/bash
# Checks for 3 duplicate lines in scripts.
# Suggest these lines be possibly replaced
# by a function.
#
tempfile=$2
#
#
sed -n '{
1N; N;
s/ /g; s\t//g;
s\n/a/g; p;
s/\\a\n/; D}' $1>> $tempfile
# sort $tempfile | uniq -d | sed 's/a/\n/g'
# rm -i $tempfile

exit
$
```

Notice that this script takes two parameters — the first ($1) for which file to scan, and the second ($2) to designate a temporary file to store the merged file lines. The reason we redirected STDOUT to a file, instead of directly into the sort command, is that it gives you the ability to keep the temporary file to see if your sed merging process (and any tweaks you make to it) are working correctly.

Before you start diving into modifying this script to try out variations, let’s scan our test text file with it:

```bash
$ ./NeededFunctionCheck.sh ScriptDataB.txt TempFile.txt
Line3
Line4
Line5
rm: remove regular file 'TempFile.txt'? Y
$
```

This is exactly what we are wanting. Now, let’s try scanning a real script and see how it does:

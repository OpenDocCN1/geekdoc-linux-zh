
- 3. 66+35=101.
- 4. 110-101=9.

The ISBN-13 becomes 9780743477109.

## The beginning database resembles

```
0743477103:Macbeth:Shakespeare, William
1578518520:The Innovator's Solution:Christensen, Clayton M.
0321349946:(SCTS) Symantec Certified Technical Specialist:Alston, Nik
1587052415:Cisco Network Admission Control, Volume I:Helfrich, Denise
```

And you want the resulting database to change so that each line resembles something like this:

```
0743477103:Macbeth:Shakespeare, William:9780743477109
```

The example that follows accomplishes this goal. It’s not the prettiest thing ever written, but it walks through the process of tackling this problem, illustrating the use of awk and sed. I’ve also included in the steps of having the script write to temporary files so that you can examine those files and see their contents at various stages of the operations. Clean programming mitigates the use of temporary files everywhere possible, but that practice also makes it difficult to follow the action at times. That said, here’s one solution out of dozens of possibilities. Read on.

## Step 1: Pull out the ISBN

Given the database as it now exists, the first order of business is to pull out the existing ISBN — only the first nine digits, because the tenth digit, which was just a checksum for the first nine, no longer matters — and slap 978 onto the beginning. The nine digits you want are the first nine characters of each line, so you can pull them out by using the cut utility:

```
cut -c1-9 books
```

Because a mathematical operation will be performed on the numbers comprising this value, and because that operation works with each digit, add a space between each number and the next one in the new entry:

```
sed 's/[0-9]/& /g'
```

Now it’s time to add the new code to the beginning of each entry (the start of every line):

```
sed 's/^/9 7 8 /'
```

Finally, do an extra step: removing the white space at the end of the line just to make the entry a bit cleaner:

```
sed 's/ $//'
```

Then write the results to a temporary file that you can examine to make sure that all is working as it should. Then the full first step becomes

```
cut -c1-9 books | sed 's/[0-9]/& /g' | sed 's/^/9 7 8 /' | sed 's/ $//' > isbn2
```

Note: The sed operations could be combined in a script file to increase speed and decrease cycles. I'm walking through each operation step by step to show what's going on, however, and am not worried about creating script files for this one-time-only operation.

Examining the temporary file, you see that the contents are as follows:

```
9 7 8 0 7 4 3 4 7 7 1 0
9 7 8 1 5 7 8 5 1 8 5 2
9 7 8 0 3 2 1 3 4 9 9 4
9 7 8 1 5 8 7 0 5 2 4 1
```

## Step 2: Calculate the 13th digit

You’ve taken care of the first 12 digits of the ISBN number. Now you need to compute those 12 digits to figure out the 13th value. Because the numbers are separated by a space, awk can interpret them as fields. The calculation takes several steps:

- 1. Add all the odd-placed digits:
  x=$1+$3+$5+$7+$9+$11
- 2. Add all the even-placed digits and multiply by 3:
  y=($2+$4+$6+$8+$10+$12)*3
- 3. Add the total of Step 2 to the total of Step 1:
  x=x+y
- 4. Find out what you need to add to round the number up to the nearest 10 by computing the modulo when divided by 10 and then subtracting it from 10.

The following awk command gets everything in place except the transformation:

```
awk ' { x=$1+$3+$5+$7+$9+$11 ; y=$2+$4+$6+$8+$10+$12 ; y=y*3 ; x=x+y ; y=x%10 ; print y }'
```

Everything is finished except subtracting the final result from 10, which is the hardest part. If the modulo is 7, for example, the check digit is 3. If the modulo is 0, however, the check digit doesn't become 10 (10 - 0); it stays 0. My solution is to use the transform function of sed:

```
sed 'y/123456789/987654321/'
```

Combining the two operations into one, the second step becomes

```
awk '{ x=$1+$3+$5+$7+$9+$11 ; y=$2+$4+$6+$8+$10+$12 ; y=y*3 ; x=x+y ; y=x%10 ; print y }' | sed 'y/123456789/987654321/' > isbn3
```

Examining the temporary file, you see that the contents are

```
9
4
1
5
```

## Step 3: Add the 13th digit to the other 12

The two temporary files (one with 12 digits and the other with 1) can now be combined to get the correct 13-digit ISBN number. Just as you used cut in the earlier step, you can use paste now to combine the files. The default delimiter for paste is a tab, but you can change that delimiter to anything with the -d option. I use a space as the delimiter and then use sed to strip the spaces (remember that the isbn2 file has spaces between the digits so that they can be read as fields):

```
paste -d " " isbn2 isbn3 | sed 's/  //g'
```

Finally, add a colon as the first character of each entry to make it easier to append the newly computed ISBN to the existing file:

```
sed 's/^/: /'
```

The entire command becomes

```
paste -d " " isbn2 isbn3 | sed 's/  //g' | sed 's/^/: /' > isbn4
```

Examining the temporary file, you see that the contents are

```
:9780743477109
:9781578518524
:9780321349941
:9781587052415
```

## Step 4: Finish the process

The only operation remaining is to append the values in the temporary file to the current database. You use the default tab delimiter in the entry and then strip it out. Technically, you could specify a colon as the delimiter and avoid the last part of the last steps. But you’d rather have your value complete there and be confident that you’re stripping characters that don’t belong (tabs) instead of adding more characters than should be there. The final command is

```
paste books isbn4 | sed 's/\t//g' > newbooks
```

The final file looks like this:

```
0743477103:Macbeth:Shakespeare, William:9780743477109
1578518520:The Innovator's Solution:Christensen, Clayton M.:9781578518524
0321349946:(SCTS) Symantec Certified Technical Specialist:Alston, Nik:9780321349941
1587052415:Cisco Network Admission Control, Volume I:Helfrich, Denise:9781587052415
```

Again, you can accomplish this result in many ways. This solution isn’t the cleanest, but it does illustrate the down-and-dirty use of sed and awk.

## Final Notes on Shell Scripting

As with any other aspect of computing, it takes a while to get used to shell scripting. After you become comfortable writing scripts, however, you’ll find that you can automate any number of operations and simplify your task as an administrator. The following tips can be helpful to keep in mind:

- » After you create a script, you can run it automatically on a one-time basis by using at or on a regular basis by using cron.
- » You can use conditional expressions — such as if, while, and until — to look for events to occur (such as certain users accessing a file they shouldn’t) or to let you know when something that should be there goes away (a file is removed or a user terminates, for example).
- » You can set permissions on shell scripts in the same way that you set permissions for other files. You can create scripts that are shared by all members of your administrative group, for example. (Use case to create menus based upon LOGNAME.)

## IN THIS CHAPTER

- » Understanding programming
- » Exploring software-development tools in Linux
- » Compiling and linking programs with GCC
- » Using make
- » Debugging programs with gdb
- » Understanding the implications of GNU, GPL, and LGPL

## Chapter 3

## Programming in Linux

Linux comes loaded with all the tools you need to develop software; often, all you have to do is install them. In particular, Linux has all the GNU software-development tools, such as GCC (C and C++ compiler), GNU make, and the GNU debugger. Whereas the previous two chapters look at some simple tools and shell scripts, this chapter introduces you to programming, describes the software-development tools, and shows you how to use them. Although I provide examples in the C and C++ programming languages, the focus isn’t on showing you how to program in those languages but on showing you how to use various software-development tools (such as compilers, make, and debugger).

The chapter concludes with a brief explanation of how the Free Software Foundation’s GNU General Public License (GPL) may affect any plans you might have to develop Linux software. You need to know about the GPL because you use GNU tools and GNU libraries to develop software in Linux.

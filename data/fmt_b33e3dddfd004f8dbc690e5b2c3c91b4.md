
```bash
# Following L-O-N-D record (on 2 lines) contains 35 characters:
sed -e 's/\${start_here}/\${old_string}/\${new_string}/g' $I
OUTFILE=$1
print "RESULTS:"
cat $OUTFILE
END
#
```

```bash
# START
print "in###### EXAMPLE S7b"
print "TASK: In all lines that contain your specified string or pattern,"
print "\tchange old_string to \$new_string"
string_or_pattern_to_find="This is"
print "\${string_or_pattern_to_find}: \${string_or_pattern_to_find}"
print "Note 1: 'A' means beginning of line\n"
print "Note 2: Only line 2 and line 3 begin with 'This is'"
print "Note 3: Only line 3 contains the word 'old', which will be changed to moldy"
old_string="oldy"
```

```bash
new_string="moldy" $old_string;
print "$new_string" $new_string
print "${$(old_string or pattern to find)}\/s/${old_string}\/${new string}"/gp INFILE
#
# END
```

```
# #
```

```bash
# START
print "\ntitle###### EXAMPLE S8. This time we match a PATTERN:\n"
print "objective: change dates that contain 1990-1999 to 2007 \n"
print "First: find the first occurrence of \"START HERE"
print "Second: find the first occurrence of \"STOP HERE"
print "Third: in the group of lines, change all \old_string to \$new_string\n"
print "(g) is used to make the changes globally."\nstart_here=START HERE
stop_here=STOP
print "STOP HERE MEANS AFTER THIS LINE, NOT AT THIS COLUMN POSITION"\n
old_string="/1999(0-9)\/" matches /1990, /1991, /1992, ... / /1999
new_string="/1997/"
```

```
# #
```

```bash
# Works: old_string="/1999/" matches /1990, /1991, /1992, etc.
print "$old_string: $" matches any character
print "$new_string: $new_string"
print "EXAMPLE: /12/25/1999 is changed to /12/25/2007,"
print ""
\but 1999 IS NOT changed to \2007.
# The following O-N-G-C record (on 2 lines) contains 94 characters:
sed -e s/\${start_here}\\*/${stop_here}/\s/${old_string}\/${new_string}//g IN
FILE OUTPUT
```

```bash
print "RESULTS:"
cat $OUTFILE
# END
```

```
# #
```

```bash
# START
print "\ntitle###### EXAMPLE S9:
print "change all dates that contain 1990-1999 to 2007;"
print "print only the lines in which changes were made."
print "Dates have the following format in the file: /mm/dd/yyyy"
print "Example: /1998(1-9)-\ Includes 1990 through 1999
change_it_to_this="/2007"
print "$find_pattern $find_pattern"
print "$change_it_to_this: $change_it_to_this"
print "change when we see the year 1990 through 1999, change"
sed -n s/\${find_pattern}/\${change_it_to_this}/gp INFILE >OUTFILE
print "RESULTS:"
cat $OUTFILE
END
```

```bash
# START
print "\ntitle###### EXAMPLE S10:
print "change 'old' to 'MOLD', but it change ONLY if old is a word;"
print "\< means word boundary for the beginning of a word.
print "('g') is used to make the changes globally."
print "('i') is used to ignore case.\n"
# word characters: [a-zA-Z0-9] Note: underscore (_) is a 'word character'
# Note: 'g' is used to make the changes globally;
search_for='<old'
replace_with='MOLD'
# create a test file for input:
print 'cold, old. mold. old.' > $INFILE
print "BEFORE:"
cat $INFILE
sed s/'$(search_for)'${replace_with}/gi $INFILE >OUTFILE
sstitute; g=global; i-ignore case
print "AFTER:"
cat $OUTFILE
# END
```

修改后：`/tmp/sed2.txt` 显示：

这是文件 `sed2.txt`

MS. RIGHT

```
##### 示例 S2a:
我们可以仅用1行代码就将此更改：太！！
旧字符串：我想要这个以及这个那个也要！！
新字符串：我想要那个以及那个以及那个也要！
```

接下来，演示如何对文件中的多个记录进行更改。
这是我们的输入文件，`INFILE`:`/home/library/ROSETTA/INPUT FILES/sed.input`

```
1 HDR This is line 1
2 THIS IS LINE 2 /var/SYS_TEST/ORACLE 07/04/1996
3 THIS IS LINE 3. START HERE. old dates: 12/25/1907, 07/04/1997
4 THIS IS LINE 4 /var/SYS TEST/ORACLE 07/04/1997
5 Line 5. Cold stuff. Cold cuts. OLD STUFF. MORE STUFF!
6 line 6. Cost: $199 OLD STUFF
7 line 7. old stuff. MORE OLD STUFF! STOP HERE. 12/25/1999
8 LINE 8. old stuff. OLD STUFF. MORE STUFF! 12/25/1998
TLLR record count: 9 Do you have a cold? COLD STUFF. END D
```

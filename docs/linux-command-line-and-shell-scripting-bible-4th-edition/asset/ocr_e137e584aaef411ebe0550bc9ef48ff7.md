```
data2
  Ima Test    (312)555-1234
  Frank Tester  (317)555-9876
  HALEY     (313)555-4938
  $
```

That produces the same output as the print command. The printf command uses the %s format specifier as a placeholder for the two string values.

Notice that you have to manually add the newline character at the end of the printf command to force a newline. Without it, the printf command will continue to use the same line on subsequent prints.

This is useful if you need to print multiple things on the same line but using separate printf commands:

```
$ gawk 'BEGIN{FS=", "} {printf "%s  $1} END{printf "\n"}'
data1
  data11 data21 data31
  $
```

Each of the printf outputs appears on the same line. To be able to terminate the line, the END section prints a single newline character.

Next, let's use a modifier to format the first string value:

```
$ gawk 'BEGIN{FS="\n"; RS=""} {printf "%16s  %s\n", $1, $4}'
data2
  Ima Test    (312)555-1234
  Frank Tester  (317)555-9876
  HALEY Example  (313)555-4938
  $
```

By adding the 16 modifier value, we force the output for the first string to use 16 spaces. By default, the printf command uses right justification to place the data in the format space. To make it left justified, just add a minus sign to the modifier:

```
$ gawk 'BEGIN{FS="\n"; RS=""} {printf "%-16s  %s\n", $1, $4}'
data2
  Ima Test      (312)555-1234
  Frank Tester  (317)555-9876
  HALEY Example  (313)555-4938
  $
```

Now that looks pretty professional!
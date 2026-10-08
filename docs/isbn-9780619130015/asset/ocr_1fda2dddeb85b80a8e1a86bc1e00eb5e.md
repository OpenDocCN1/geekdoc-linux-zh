```
# Print the report
awk '
BEGIN {
{ FS = ":"}
{ print "\tProgrammer Activity Status Report\n" }
{ "date" | getline d }
{ printf "\t\t%s\n",d }
{ print "Prog#\t *----Name----*\t\tProjects\n" }
{ print
"=================================================================="}
}
{ printf "%-s\t%12.12s %12.12s %s\t%d\n",
$1, $2, $3, $4, $5 }' pactrep
```

6 Type the following in the script:

# remove all the temporary files
rm pnum pnn pactrep

7 Press Esc to switch to command mode.

8 Type :wq to write the file and exit from vi.

9 After the $ command prompt, type sh practivity and press Enter.

You see the report:

| Prog# | *-----Name-----* | Projects |
| :-- | :-- | :-- |
| 101 | Johnson | John K 1 |
| 102 | King | Mary K 2 |
| 103 | Brown | Gretchen K 2 |
| 104 | Adams | Betty C 1 |
| 105 | Utley | Amos V 2 |
| 106 | Wilson | Patricia B 1 |
| 107 | Culligan | Thomas F 1 |
| 108 | Mitchell | Hillary N 0 |
| 109 | Arbuckle | Margaret F 1 |
| 110 | Ford | Terrence H 2 |
| 111 | Greene | Sarah L 0 |
| 112 | Rose | Richard P 1 |
| 113 | Daniels | Allan S 0 |
| 114 | Edwards | George J 0 |
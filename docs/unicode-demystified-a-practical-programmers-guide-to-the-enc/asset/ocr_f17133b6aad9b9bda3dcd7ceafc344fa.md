```
END {
  for (count = 1; count <= nfields; count++) {
    print "      ------" > "tally.out"
  }
  print "\n" > "tally.out"
  for (count = 1; count <= nfields; count++) {
    printf("%10.2f", sum[count]) > "tally.out"
  }
  print "\n\n" Grand Total "\n" > "tally.out"
} ' < numbers
```

# $ tally skipped:

Record 3 skipped:
30 xyz 50 70

# Record 6 skipped:

60 30 45.0 66.1

# Record 11 skipped:

110 123 50 57a.5

# $ tally.out

|10.00 20.00 30.30 40.50
20.00 30.00 45.70 66.10
40.00 75.00 107.20 55.60
50.00 210.00 30.30 40.50
70.00 1134.70 50.00 70.00
80.00 75.00 107.20 55.60
90.00 176.00 30.30 40.50
100.00 1027.45 45.70 66.10
120.00 75.00 107.20 55.60|

580.00 2633.15 553.90 490.50

Grand Total 4257.55

The next gawk example reads the passwd file, listing users who do not have passwords and who have duplicate ID numbers:

# $ /etc/password

```
bill:102:100:ext 123:home/bill:/bin/bash
roy:104:100:ext 475:home/roy:/bin/bash
tom:105:100:ext 476:home/tom:/bin/bash
lynn:166:100:ext 500:home/lynn:/bin/bash
mark:107:100:ext 112:home/mark:/bin/bash
sales:108:100:ext 102:/m/market:/bin/bash
namne:109:100:ext 355:home/anne:/bin/bash
toni:164:100:ext 357:home/toni:/bin/bash
ginny:115:100:ext 109:home/ginny:/bin/bash
chuck:116:100:ext 146:/home/chuck:/bin/bash
neil:164:100:ext 159:home/neil:/bin/bash
```
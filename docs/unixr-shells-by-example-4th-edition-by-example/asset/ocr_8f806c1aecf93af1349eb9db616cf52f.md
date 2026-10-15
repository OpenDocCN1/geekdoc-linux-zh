# EXAMPLE 9.61 (CONTINUED)

```
2  % echo $d[1-3]
Fri Aug 27
3  % echo $d[6]
2004
4  % echo $d[7]
Subscript out of range.
5  % echo "The calendar for the month of November is `cal 11 2004`"
The calendar for month of November is November 2004 S M Tu W
Th F S 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21
22 23 24 25 26 27 28 29 30
```

# EXPLANATION

+   1. The variable d is assigned the output of the UNIX date command. The output is stored as an array. The value of the variable is displayed.
+   2. The first three elements of the array are displayed.
+   3. The sixth element of the array is displayed.
+   4. There are not seven elements in the array. The shell reports that the subscript is out of range.
+   5. The output spans more than one line. Each newline is replaced with a space. This may not be the output you expected.

# EXAMPLE 9.62

```
1  % set machine = `users | awk '/tom/{print $1}'`
2  % echo $machine
dumbo bambi dolphin
3  % echo $#machine
3
4  % echo $machine[$#machine]
dolphin
5  % echo $machine
dumbo bambi dolphin
6  % shift $machine
% echo $machine
bambi dolphin
7  % echo $machine[1]
bambi
8  % echo $#machine
2
```
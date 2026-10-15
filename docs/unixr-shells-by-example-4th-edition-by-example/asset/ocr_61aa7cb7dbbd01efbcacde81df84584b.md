# EXAMPLE 6.12

```
# Second awk script-- awk.sc2
1 BEGIN { FS="," 
print "NAME\t\tDISTRICT\tQUANTITY"
print "________________________________________\n" 
}
2 {print $1"\t " $3"\t\t" $7}
{total+=$7}
/north/{count++}
3 END{
print "________________________________________"
print "The total quantity is " total
print "The number of northern salespersons is " count "."
}
```

(The Output)

```
4 % nawk -f awk.sc2 datafile2
NAME DISTRICT QUANTITY
________________________________________
Joel Craig NW 4
Sharon Kelly NE 23
Chris Foster SW 18
May Chin SO 15
Derek Johnson SE 17
Susan Beal EA 20
TJ Nichols NE 13
Val Shultz NO 9
Sheri Watson CT 13
________________________________________
The total quantity is 132
The number of northern salespersons is 3.
```

# EXPLANATION

+   1 The BEGIN block is executed first. The field separator (FS) is set. Header output is printed.
+   2 The body of the awk script contains statements that are executed for each line of input coming from datafile2.
+   3 Statements in the END block are executed after the input file has been closed, i.e., before awk exits.
+   4 At the command line, the nawk program is executed. The -f option is followed by the script name, awk.sc2, and then by the input file, datafile2.
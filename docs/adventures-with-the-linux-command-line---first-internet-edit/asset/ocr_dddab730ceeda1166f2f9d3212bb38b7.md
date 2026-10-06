language extension for this problem), but it's not pretty. It is best to avoid trying to read
this type of file.

# Convert a File Into TSV Format

A frequently available alternative to the CSV file is the TSV (tab separated value) file.
This file uses tab characters as the field separators:

```
awk BEGIN(FS="	") print $1,$2,$3,$4,$5 random_table.dat
```

Again, writing these files is easy to do. We just set the output field separator to a tab
character. In regards reading, most applications that create CSV files can also write
TSV files. Using TSV files avoids the embedded comma problem we often see when
attempting to read CSV files.

# Print the Total for Each Row

If all we need to do is some simple addition, this is easily done:

```
awk {
  t = $1 + $2 + $3 + $4 + $5
  printf("%6d\n", $0, t)
}
random_table.dat
```

# Print the Total for Each Column

Adding up the column is pretty easy, In this example, we use a loop and array to
maintaining totals for each of the five columns in our data file:

```
awk {
  for (i = 1; i <= 5; i++) {
    t[i] += $i
  }
  print
}
END {
  print "="-"
  for (i = 1; i <= 5; i++) {
    printf("%7d", t[i])
  }
  printf("\n", "")
}
random_table.dat
```

# Print the Minimum and Maximum Value in Column 1

```
awk {
  BEGIN (min = 99999)
  $1 > max (max = $1)
  $1 < min (min = $1)
}
END (print "Max=", max, "Min =", min)
```

112 AWK
# EXAMPLE 5.34 (CONTINUED)

(Output)

```
3 \$Joe Blow\|12/86\|10 Main St.\|Boston, MA\|02530
4 The guy’s name is Joe Blow.
5 The birthday is 11/12/86.

7 \$Joe Blow
8 11/12/86;10 Main St.;Boston, MA;02530
9
11 \$Joe Blow
12 11/12/86
13 10 Main St.
```

# EXPLANATION

+   1 The scalar $string is split at each colon.
+   2 The delimiter is a colon. The limit is 2.
+   6 The string is split by colons and given a limit of two, meaning that the text up to the first colon will become the first element of the array; in this case, $line[0] and the rest of the string will be assigned to $line[1]. LIMIT, if not stated, will be one more than the total number of fields.
+   10 The string is split by colons and returns a list of scalars. This may make the code easier to read.

# 5.3.6 Creating a Scalar from a List

The join Function. The *join* function joins the elements of an array into a single string and separates each element of the array with a given delimiter, sometimes called the “glue” character(s) since it glues together the items in a list (opposite of *split*). (See Figure 5.13.) The expression DELIMITER is the value of the string that will join the array elements in LIST.

# FORMAT

```
join(DELIMITER, LIST)
```

# EXAMPLE 5.35

```
(The Script)
use warnings;
my(@colors, $color_string);
# Joining each element of a list with commas
1 @colors = qw( red green blue);

2 $color_string = join(“,”, @colors); # Create a string from an array
3 print “The new string is: $color_string\n”;

(Output)
3 The new string is: red, green, blue
```
# EXAMPLE 7.10 (CONTINUED)

```
3   Scount++;
4   $remain--;                    // Pseudocode
5   if ($count > 10){print "Party's over. \n";}
}
print "\n";
```

(Output)
10 bottles on the shelf on the shelf. Take one down and pass it all around.
Now 9 bottles of beer on the shelf!
9 bottles on the shelf on the shelf. Take one down and pass it all around.
Now 8 bottles of beer on the shelf!
8 bottles on the shelf on the shelf. Take one down and pass it all around.
Now 7 bottles of beer on the shelf!
7 bottles on the shelf on the shelf. Take one down and pass it all around.
Now 6 bottles of beer on the shelf!
6 bottles on the shelf on the shelf. Take one down and pass it all around.
Now 5 bottles of beer on the shelf!
5 bottles on the shelf on the shelf. Take one down and pass it all around.
Now 4 bottles of beer on the shelf!
4 bottles on the shelf on the shelf. Take one down and pass it all around.
Now 3 bottles of beer on the shelf!
3 bottles on the shelf on the shelf. Take one down and pass it all around.
Now 2 bottles of beer on the shelf!
2 bottles on the shelf on the shelf. Take one down and pass it all around.
Now 1 bottle of beer on the shelf!
1 bottle of beer on the shelf on the shelf. Take one down and pass it all around.
Now 0 bottles of beer on the shelf!
Party's over.

# EXPLANATION

+   1 The scalars $count, $beers, $remain, and $where are initialized.
+   2 The while loop is entered; the control expression is tested and evaluated.
+   3 The scalar $count is incremented.
+   4 The scalar $remain is decremented.
+   5 When the value of $count is greater than 10, this line is printed.

# 7.3.2 The until Loop

The *until* statement executes the block as long as the control expression after the *until* is false. When the expression evaluates to true, the loop exits. See Figure 7.3.
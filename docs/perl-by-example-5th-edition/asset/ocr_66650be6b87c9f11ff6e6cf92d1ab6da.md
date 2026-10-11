# EXPLANATION

+   1 The *datebook* master file is opened for reading from the $fh filehandle. Each line consists of colon-separated fields terminated by a newline.
+   2 The contents of the file are read and assigned to @lines. Each line of the file is an element of the array.
+   3 The *map* function uses the block format. (With the block format, don't put a comma after the close of the block.) The *split* function splits up the input, @lines, at colons, resulting in a list where each field becomes an element of the array.
+   4 The *foreach* loop iterates through the array, assigning each element, in turn, to $field.
+   5 The *display* demonstrates the results of the mapping. Before mapping, the line was:
+   *Sir Lancelot/837-835-8257/474 Camelot Boulevard, Bath, WY 28356/513/69-24500*

# Slurping a File into a String with the *read* Function.

The *read* function allows you to read in a specified number of characters, and put them in a variable. It returns the number of characters that were read. If you know the size of a file, you can read the entire file into a string, as shown in the next example.

# FORMAT

```
```
read FILEHANDLE, SCALAR, LENGTH, OFFSET
read FILEHANDLE, SCALAR, LENGTH
```
```

# EXAMPLE 10.8

```
```read($fh, $str, 100);```
```

# EXAMPLE 10.9

```
```
				(The Script)
				use warnings;
				1 open(my $fh, "<", "datebook*") or die;
				2 $size = -s $fh;
				3 read($fh, $buffer, $size);
				4 @fields = split(/\n|:/, $buffer);
				5 foreach $f (@fields){
				6 print "$f\n";
				7 print " \x35, "\n" if $f =~ /\d+$f/;
				}
				close $fh;
```
```
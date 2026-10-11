# EXPLANATION

+   The datebook file is opened for reading.
+   All of the lines are read from the file, via the filehandle, and assigned to @lines, where each line is an element of the array. The newline terminates each element.
+   The array @lines is printed.
+   The scalar function returns the number of elements (that is, lines) in the array. @lines.

# Using map to Create Fields from a File

You can use the map function in conjunction with the split function to break up input into several elements of an array.

# EXAMPLE 10.7

```
5
{
    (The Script)
    use warnings;
    my (@lines, @fields, $field, $fh);
    # Map using a block
    1 open(my $fh, "<", "datebook.master") or die $!;
    2 @lines=<$fh>;
    3 @fields = map { split(":") } @lines;
    4 foreach $field (@fields){
    5 print $field, "\n";
    }

    (Output)
    Sir Lancelot
    837-835-8257
    474 Camelot Boulevard, Bath, WY 28356
    5/13/69
    24500

    Tommy Savage
    408-724-0140
    1222 Oxbow Court, Sunnyvale, CA 94087
    5/19/66
    34200

    Yukio Takeshida
    387-827-1095
    13 Uno Lane, Ashevillle, NC 23556
    7/1/29
    57000

    Vinh Tran
    438-910-7449
    8235 Maple Street, Wilmington, VT 29085
    9/23/63
    68900
}
```
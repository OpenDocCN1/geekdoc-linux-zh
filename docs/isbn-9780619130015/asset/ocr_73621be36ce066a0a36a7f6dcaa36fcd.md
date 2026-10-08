+   3 Save the file and exit the editor.

+   4 Use the chmod command to grant the file execute permission.

+   5 Test the program by typing `./persort.p3 numberlist` and then press **Enter**. Your screen should appear similar to Figure 9-17.

![](bbox=[0.17, 0.2, 0.78, 0.53])

Figure 9-17: Output of persort.p3

The `persort.p3` program uses a sort subroutine that compares $a and $b numerically rather than textually. The program also initializes the array element index to start with the first element, 0. The while loop,

```
while (<>)
{
  @somelist[$x] = $_;
  $x++;
}
```

works the same as previously described, in that it reads records from a file and stores the lines inside an array.

The sort subroutine,

```
sub numbers
{
  if ($a < $b) { -1; }
  elsif ($a == $b) { 0; }
  else ( +1; }
}
```
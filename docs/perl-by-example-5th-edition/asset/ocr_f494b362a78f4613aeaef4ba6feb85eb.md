# EXAMPLE 5.32

```
(The Script)
use warnings;
# $p1 splitting up $ my @line;
1 while(<DATA>){
2 @line=split("; * ");
# or split (/;/, &);
3 print "$line[0]";
}
```

__DATA_
Betty Boop:245-835-8357;635 Cutesy Lane, Hollywood, CA 91464;6/23/23;34500
Igor Chevaky:385-375-8395;3567 Popular Place, Caldwell, NJ 23875;6/18/68;23400
Norma Corder:397-857-2735;74 Pine Street, Dearborn, MI 23874;3/28/45;245700
Jennifer Cowan:548-834-2348;583 Laurel Ave., Kingsville, TX 83745;10/1/35;58900
Fred Fardarkle:674-843-1385;20 Park Lane, Duluth, MN 23850;4/12/23;78900

(Output)
Betty Boop
Igor Chevaky
Norma Corder
Jennifer Cowan
Fred Fardarkle

# EXPLANATION

+   1. The _variable holds each line of the file DATA filehandle; the data being processed is below the _DATA_ line. Each line is assigned to $_, $ is also the default line for split.
+   2. The split function splits the line, ($, ), using the : as a delimiter and returns the line to the array, @line.
+   3. The first element of the @line array, line[0], is printed.

# EXAMPLE 5.33

```
(The Script)
use warnings;
my($name, $phone, $address, $dd, $ss1);
# $p1 splitting up $ _ and creating an unnamed list
while(<DATA>){
1 ($name,$phone,$address,$d,$ss1)=split("; * ");
2 print "$name\t $phone"; }
```
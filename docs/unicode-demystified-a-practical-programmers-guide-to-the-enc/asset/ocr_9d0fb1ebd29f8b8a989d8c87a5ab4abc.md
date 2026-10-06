# 1198 gawk

The END pattern works in a manner similar to the BEGIN pattern, except that gawk takes the actions associated with it after it has processed the last of its input lines. The following report displays information only after it has processed the engine data file. The NR variable retains its value after gawk finished processing the data file, so that an action associated with an END pattern can use it:

```
$ gawk 'END {print NR, 'cars for sale.'}' cars
12 for sale.
```

The next example uses if commands to change the values of some of the fields. As long as gawk does not make any changes to a record, it leaves the entire record, including separators, intact. Once it makes a change to a record, gawk changes all separators in that record to the value of the output field separator. The default output field separator is a SPACE:

$ gawk -f separ_demo cars
plymouth fury 77 73 2500

chevrolet nova 79 60 3000
ford mustang 65 45 10000
volvo gl 78 102 9850
ford ltd 83 15 10500
chevrolet nova 80 50 3500
iatat 600 65 115 450
honda accord 81 30 6000
ford thundbd 84 10 17000
toyota tercel 82 180 750
chevrolet impala 65 85 1550
bronco 83 25 9500

You can change the default value of the output field separator by assigning a value to the OFS variable. This example assigns a TAB character to OFS, using a common sequence notation. This fix improves the appearance of the report but does not properly line up the columns:

```
$ cat of_demo
BEGIN
OFS = "\t"
{
if ($1 ~ /ply/) $1 = "plymouth"
if ($1 ~ /chev/) $1 = "chevrolet"
print
}
```
```
$numrows = ceil(($sundays + $weekday) / $cols);
```

```
echo "<br />";
echo "<table class='cal' cellspacing=0 cellpadding=5 border=1>";
echo "<tr>";
echo "<th class='cal'>Sunday</th>";
echo "<th class='cal'>Monday</th>";
echo "<th class='cal'>Tuesday</th>";
echo "<th class='cal'>Wednesday</th>";
echo "<th class='cal'>Thursday</th>";
echo "<th class='cal'>Friday</th>";
echo "<th class='cal'>Saturday</th>";
echo "</tr>";

$counter = 1;
$newcounter = 1;
```

The first three lines set up some essential variables. You first specify the number of columns in the `$cols` variable—you are using 7, one for each day. Next, the `weekday` variable returns the number of the day in the week for the first of the month. For example, if the day is Friday, it is the sixth day and the function returns 5.

# NOTE

# Counting from Zero

Many functions in PHP begin counting at zero. When you code and get results that are just slightly different (such as 8 cells appearing instead of 7), it could be because you have assumed that a function begins counting at 1. Although this can be the case, most functions begin from 0.

The `$numrows` variable takes the `$sundays` variable from `bar.php`, adds the `weekday`, and divides by the number of columns (7). The reason you add `weekday` to `$sundays` is to pad out the days remaining from the previous month. Referring to Figure 8-5, you can see that the month begins on Friday, but the Sunday to Thursday days do not contain any dates. By adding `weekday`, you set the amount of days that are padded. In this example, Friday returns 5, and if you count from left to right (starting with 0), you get Friday.

After setting these variables, the table headings are added and, finally, two variables are set to 1. These variables will be used as counters later in the code.

Now you can add the first row of cells that add the date for a given day. Before you begin adding the actual dates, pad out the days before the first of the month:
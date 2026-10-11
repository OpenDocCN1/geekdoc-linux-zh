# Point & Click Linux!

# cal

The cal command, entered without any arguments, shows you a calendar for the current month that looks like this:

![](bbox=[0.37, 0.09, 0.95, 0.41])

But there are several arguments you can add to the cal command to tell you even more. The Julian date, for example. Try this:

```
[username]$cal -j 1 2004
```

The previous example produces a rather normal looking calendar, but the -j argument changes it from showing the day of the month (1-31 for January) to the Julian date, or day of the year, instead. Of course for January, it’s hard to tell the difference. Try this:

```
[username]$cal -j 2 2004
```

That lists month 2, with the days a little more obviously being day of the year rather than day of the month, as you can see here:

![](bbox=[0.37, 0.52, 0.95, 0.82])

If you liked that, add a -y and cal will print the entire year for you. If you specify only a "-y" as an argument, cal will print a normal calendar for the entire year.
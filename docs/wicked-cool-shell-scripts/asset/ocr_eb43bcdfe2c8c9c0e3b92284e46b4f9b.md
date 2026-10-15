```
calculate="$((10#$(date -d "12/31/$startyear" +%j)) \
-$(10#$(date -d $startdatefmt +%j)))"

daysleftinyear=$(($calculate ))

#### DAYS IN INTERVENING YEARS

daysbetweenyears=0
tempyear=$(($startyear + 1))

while [ $tempyear -lt $thisyear ] ; do
  daysbetweenyears=$(($daysbetweenyears + \
  $(10#$(date -d "12/31/$tempyear" +%j))))
  tempyear=$(($tempyear + 1))
done

#### DAYS IN CURRENT YEAR

dayofyear=$(date +%j) # That's easy!

#### NOW ADD IT ALL UP

totaldays=$(($(10#$daysleftinyear)) + \
$((10#$daysbetweenyears)) + \
$(10#$dayofyear ))

/bin/echo -n "$totaldays days have elapsed between "
/bin/echo -n "$startmon/$startday/$startyear"
echo "and today, day $dayofyear of $thisyear."
exit 0
```

Listing 15-3: The daysago script

# How It Works

This is a long script, but what's going on isn't too complicated. The leap year function 1 is straightforward enough—we just check if the year has 366 days or not.

There's an interesting test to ensure that the GNU version of date is available 2 before the script proceeds.

The redirection throws away any error messages or output, and the return code is checked to see whether it's nonzero, which would indicate an error parsing the --version parameter. On OS X, for instance, date is minimal and does not have --version or many other niceties.

Now it's just basic date math. %j returns the day of the year, so it makes calculating days left in the current year straightforward 3. The count of days in intervening years is done in the while loop, where the progression is tracked with the tempyear variable.
# # Chapter 8

+   
+   \- getSecond: *Returns the seconds of the date object.*
+   \- getTime: *Returns the number of seconds since the Unix epoch.*
+   \- getWeekOfYear: *Returns the week for the date object in integer format.*
+   \- getWeeksInMonth: *Returns the number of weeks in the month of the date object.*
+   \- getYear: *Returns the year for the date object.*
+   \- inDaylightTime: *Determines whether or not the time/date is in Daylight Savings Time.*
+   \- isLeapYear: *Determines if the year of the date object is in a leap year.*
+   \- setDate: *Sets the date of the date object.*
+   \- setDay: *Sets the day of the date object.*
+   \- setHour: *Sets the hour of the date object.*
+   \- setMinute: *Sets the minute of the date object.*
+   \- setMonth: *Sets the month of the date object.*
+   \- setSecond: *Sets the seconds of the date object.*
+   \- setTZ: *Sets the time zone for the date object.*
+   \- setYear: *Sets the year for the date object.*
+   

This is all from the Date class. There are two other classes that are used by the date class, but which can also be used directly; these are the Date_Span and Date_TimeZone classes. They have numerous specific methods within them if you need something more specific than what the Date class can offer, such as returning a list of all available time zones, or determining the default time zone of the server.

# ## A Quick Example

The following is a quick example of how easy it is to use the Date package to spit out something like the number of weeks left in the year:

```
```php
<?php
require_once(*date.php*);

$currweek = new Date();

$weeksleft = 52 - ($currweek->getWeekOfYear());
echo *There are * . $weeksleft . * weeks left in the year.*;
?>
```
```

As you can see, something so simple can really make your life easy when you are trying to complete more complex date calculations or work with time zones.

# ### DB

This is the PEAR package that allows you to easily connect and query your database. There are numerous other database-related packages you can look into. MDB, for example, is similar to DB but provides more
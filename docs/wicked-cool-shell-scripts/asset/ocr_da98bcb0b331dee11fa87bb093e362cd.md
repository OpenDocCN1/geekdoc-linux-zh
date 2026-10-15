useful error messages for typical input problems, like a time zone that's not found because the user is specifying a country like Brazil, which has more than one time zone.

For example, although TZ="Casablanca" date would fail to find a matching region and display the UTC/GMT time instead, the city Casablanca does exist in the time zone database. The issue is that you have to use its proper region name of Africa/Casablanca in order for it to work, as was shown in the introduction to this script.

This script, on the other hand, can find Casablanca in the Africa directory on its own and identify the zone accurately. However, just specifying Africa wouldn't be specific enough, as the script knows there are subregions within Africa, so it produces an error message indicating that the information is insufficient to uniquely identify a specific time zone ①. You can also just use list to list all time zones ② or an actual time zone name ③ (for example, UTC or WET), which can be used as an argument to this script.

NOTE An excellent reference to the time zone database can be found online at http://www.twinsun.com/tz/tz-link.htm.

# Running the Script

To check the time in a region or city, specify the region or city name as an argument to the timein command. If you know both the region and the city, you can also specify them as region/city (for example, Pacific/Honolulu). Without any arguments, timein shows UTC/GMT. Listing 2-20 shows the timein script running with a variety of time zones.

# The Results

```
$ timein
It's Wednesday, April 5, 2017, at 4:00 PM in UTC
$ timein London
It's Wednesday, April 5, 2017, at 5:00 PM in Europe/London
$ timein Brazil
The region "Brazil" has more than one time zone. Please use 'list' to see all known regions and time zones.
$ timein Pacific/Honolulu
It's Wednesday, April 5, 2017, at 6:00 AM in Pacific/Honolulu
$ timein WET
It's Wednesday, April 5, 2017, at 5:00 PM in WET
$ timein mycloset
Can't find an exact match for "mycloset". Please use 'list' to see all known regions and time zones.
```

Listing 2-20: Testing the timein shell script with various time zones
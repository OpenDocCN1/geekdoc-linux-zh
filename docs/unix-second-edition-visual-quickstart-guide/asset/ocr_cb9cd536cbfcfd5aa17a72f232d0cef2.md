# Calendaring with cal

One of the handiest Unix utilities is cal, which—logically—is a calendar. Find out what today's date is, what day of the week December 31st is, or what the calendar year looks like. As Code Listing 15.1 shows, all you have to do is type cal and any specific options you want.

# To use the cal utility:

+   1. cal
+   Type cal at the shell prompt to see the current month's calendar, as shown in Code Listing 15.1. Then, start playing with options, as shown in the next few steps.

+   2. cal -j
+   Use cal -j to see the Julian calendar, which shows each day numbered from the beginning of the year. (This argument doesn't work on all systems.)

+   3. cal 2004 | more
+   Pipe cal 2004 to more to see the whole year's calendar.

+   4. cal 12 1941
+   Type cal plus specific dates to view dates for a particular year.

# Tips

+   Note that cal is Y2K compliant. If you ask for cal 98, you'll get the calendar for the year 98. That is, 1,900 and a few years ago.

+   Put cal into your startup configuration files to get a reminder of the date whenever you log in. Check out Chapter 8 for details.
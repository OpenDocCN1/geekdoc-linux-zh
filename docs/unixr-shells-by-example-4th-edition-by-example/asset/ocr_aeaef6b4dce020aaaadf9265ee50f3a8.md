# LAB 6: awk EXERCISE

(Refer to the database called lab6.data on the CD.)

Mike Harrington:(510) 548-1278:250:100:175
Christian Dobbins:(408) 538-2358:155:90:201
Susan Dalass:(206) 654-6279:250:50:50
Archie McNichol:(206) 548-1348:250:100:175
Jody Savage:(206) 548-1278:15:188:150
Guy Quigley:(916) 343-6410:250:100:175
Dan Savage:(406) 298-7744:450:300:275
Nancy McNeil:(206) 548-1278:250:80:75
John Goldenrod:(916) 348-4278:250:100:175
Chet Main:(510) 548-5258:50:95:135
Tom Savage:(408) 926-3456:250:160:200
Elizabeth Stachelin:(916) 440-1763:175:75:300

The database above contains the names, phone numbers, and money contributions to the party campaign for the past three months.

+   1. Write a nawk script that will produce the following report:

```
~~~text
***FIRST QUARTERLY REPORT***
***CAMPAIGN 2004 CONTRIBUTIONS***
------------------------------------------------------------
NAME              PHONE       Jan   | Feb   | Mar   | Total Donated
------------------------------------------------------------
Mike Harrington   (510) 548-1278  250.00 100.00 175.00 525.00
Christian Dobbins (408) 538-2358  155.00  90.00 201.00 446.00
Susan Dalass      (206) 654-6279  250.00  50.00  50.00 350.00
Archie McNichol   (206) 548-1348  250.00 100.00 175.00 525.00
Jody Savage       (206) 548-1278   15.00 188.00 150.00 353.00
Guy Quigley       (916) 343-6410  250.00 100.00 175.00 525.00
Dan Savage        (406) 298-7744  450.00 300.00 275.00 1025.00
Nancy McNeil      (206) 548-1278  250.00  80.00  75.00 405.00
John Goldenrod    (916) 348-4278  250.00 100.00 175.00 525.00
Chet Main         (510) 548-5258   50.00  95.00 135.00 280.00
Tom Savage        (408) 926-3456  250.00 160.00 200.00 618.00
Elizabeth Stachelin (916) 440-1763 175.00 75.00 300.00 550.00
------------------------------------------------------------
                         SUMMARY
------------------------------------------------------------
The campaign received a total of $6137.00 for this quarter.
The average donation for the 12 contributors was $511.42.
The highest total contribution was $1025.00 made by Dan Savage.
***THANKS Dan***
The following people donated over $500 to the campaign.
They are eligible for the quarterly drawing!!
Listed are their names (sorted by last names) and phone numbers:
    John Goldenrod--(916) 348-4278
    Mike Harrington--(510) 548-1278
~~~
```
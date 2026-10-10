# Note

Since you are editing a plain text file, no validity check is made. If you set column 3 to 31 and column 4 to 2, setting the time to February 31, then the job never runs.

# Column Entries in a Crontab File

| Column or Option (from left to right) | Argument | Comments |
| --- | --- | --- |
| 1 Minute | 0-59 |  |
| 2 Hour | 0-23 | 0 is midnight. |
| 3 Day of the month | 1-31 |  |
| 4 Month | 1-12 |  |
| 5 Day of the week | 0-6 | 0 is Sunday. |
| 6 Job | any command | Options or arguments can be included. No quotation marks are needed around the string. |
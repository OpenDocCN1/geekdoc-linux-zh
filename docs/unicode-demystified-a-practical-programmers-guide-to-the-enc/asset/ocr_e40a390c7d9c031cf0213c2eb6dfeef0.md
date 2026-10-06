# Field Descriptor (Continued)

| | |
|---|---|
| %d | Day of the month—01 to 31 |
| %D | Date in mm/dd/yy format |
| %H | Hour—00 to 23 |
| %I | Hour—00 to 12 |
| %j | Julian date (day of the year—001 to 366) |
| %m | Month of the year—01 to 12 |
| %M | Minutes—00 to 59 |
| %n | NEWLINE character |
| %P | A.M. Or P.M. |
| %r | Time in A.M./P.M. notation |
| %S | Seconds—00 to 59 |
| %s | Number of seconds since the beginning of Jan. 1, 1970 |
| %t | TAB character |
| %T | Time in HH:MM:SS format |
| %w | Day of the week—0 to 6 (0=Sunday) |
| %y | Last two digits of the year—00 to 99 |
| %Y | Year in four-digit format (for example, 2005) |
| %Z | Time zone (for example, PDT) |

By default zero fills numeric fields. Place an underscore (_) immediately following the percent sign (%) for a specific field to cause date to blank the field and with a hyphen (--) to cause date not to fill the field at all.

The date utility assumes that in a format string, any character that is not a percent sign, an underscore or a hyphen following the percent sign, or a field descriptor is ordinary text and copies it to standard output. You can use ordinary text to add punctuation to the date and to add labels (for example, you can put the word DATE:
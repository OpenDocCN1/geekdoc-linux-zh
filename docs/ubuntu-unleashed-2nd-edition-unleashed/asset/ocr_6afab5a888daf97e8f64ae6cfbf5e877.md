+   - %k—Hour
+   - %l—Hour, 12-hour clock
+   - %m—Month number, starting with 1
+   - %M—Minute, leading zeroes
+   - %n—NEWLINE
+   - %o—Ordinal day of month—1st, 2nd, 25th, and so on
+   - %p—AM or PM
+   - %r—Time format: 09:05:57 PM
+   - %R—Time format: 21:05
+   - %S—Seconds, leading zeroes
+   - %t—Tab
+   - %T—Time format: 21:05:57
+   - %U—Week number; Sunday as first day of week
+   - %w—Day of the week, numerically; Sunday = 0
+   - %W—Week number; Monday as first day of week
+   - %x—Date format: 11/19/94
+   - %X—Time format: 21:05:57
+   - %y—Year (two digits)
+   - %Y—Year (four digits)
+   - %z—Time zone in ASCII, such as PST

echo

The echo directive displays any one of the include variables in the following list. Times are displayed in the time format specified by timefmt. Use the var attribute to indicate the variable to be displayed:

+   - DATE_GMT—The current date in Greenwich mean time.
+   - DATE_LOCAL—The current date in the local time zone.
+   - DOCUMENT_NAME—The filename (excluding directories) of the document requested by the user.
+   - DOCUMENT_URI—The (%-decoded) URL path of the document requested by the user. Note that in the case of nested include files, this isn’t the URL for the current document.
+   - LAST_MODIFIED—The last modification date of the document requested by the user.
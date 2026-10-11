TABLE 6.2 strftime() conversion format specifiers

| Specifier(s) | C99 | Meaning |
| :--- | :---: | :--- |
| %a | | The locale\u0027s abbreviated weekday name. |
| %A | | The locale\u0027s full weekday name. |
| %b | | The locale\u0027s abbreviated month name. |
| %B | | The locale\u0027s full month name. |
| %c, %Ec | | The locale\u0027s \"appropriate\" date and time representation. |
| %C, %EC | ✔ | The century (00–99). |
| %d, %Od | | The day of the month (01–31). |
| %D | ✔ | Same as %m/%d/%y. |
| %e, %Oe | ✔ | The day of the month. A single digit is preceded with a space (1–31). |
| %F | ✔ | Same as %Y-%m-%d (ISO 8601 date format). |
| %g | ✔ | The last two digits of week-based year (00–99). |
| %G | ✔ | The ISO 8601 week-based year. |
| %h | ✔ | Same as %b. |
| %H, %OH | | The hour in a 24-hour clock (00–23). |
| %I, %OI | | The hour in a 12-hour clock (01–12). |
| %j | | The day of the year (001–366). |
| %m, %Om | | The month as a number (01–12). |
| %M, %OM | | The minute as a number (00–59). |
| %n | ✔ | A newline character (\`\'\`n\'\`). |
| %p | | The locale\u0027s a.m./p.m. designation. |
| %r | ✔ | The locale\u0027s 12-hour clock time. |
| %R | ✔ | Same as %H:%M. |
| %s, %OS | | The second as a number (00–60). |
| %t | ✔ | A TAB character (\`\'\`t\'\`). |
| %T | ✔ | Same as %H:%M:%S (ISO 8601 time format). |
| %u, %Ou | ✔ | ISO 8601 weekday number, Monday = 1 (1–7). |
| %U, %OU | | Week number, first Sunday is first day of week 1 (00–53). |
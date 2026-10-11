# 76 | Practical PHP and MySQL

Next, the date is displayed. If you output an unformatted date from the database, the date would look something like this:

```
2005-08-01 18:02:32
```

Notice that the preceding result is not in the most useful of formats. Use strtotime() and date() to clean this up for human consumption.

The strtotime() function converts the date into a UNIX timestamp. This timestamp refers to the number of seconds since 12:00 a.m. on January 1, 1970. The time is known as the Epoch, and when you have this number of seconds, you can then feed it into the date() function to format those seconds into something more useful.

The date() function converts this number of seconds into a readable date, using several special format symbols (D j S F Y g. iA in this example). Each of these symbols formats a particular part of the date and time. You can find out more about these and other symbols in the PHP manual entry for dates at http://www.php.net/ date.

Table 4-4 gives an example for 2:35 p.m. on April 6, 2005.

**TABLE 4-4 Each letter represents a portion of the date, as well as how to format that date.**

| DATE() SYMBOLS | DATE |
| :--- | :--- |
| D | Wed |
| D j | Wed 6 |
| D j S | Wed 6th |
| D j S F | Wed 6th April |
| D j S F Y | Wed 6th April 2005 |
| D j S F Y g | Wed 6th April 2005 2 |
| D j S F Y g. | Wed 6th April 2005 2. |
| D j S F Y g. i | Wed 6th April 2005 2.35 |
| D j S F Y g. iA | Wed 6th April 2005 2.35PM |

Finally, in the last bit of the code, the body of the blog entry is presented. The first of these three lines opens a paragraph tag, and the second actually outputs the
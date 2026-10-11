# 8.4 Using DBI in Web Applications

print table (|-border => "1", @rows);
}

The querry also includes a LIMIT 200 clause, as a simple precaution against the script sending huge amounts of data to your browser. (That's not likely to happen for the tables in the sample database, but it might occur if you adapt the script to display the contents of tables in other databases.) display_table_contents() shows the rows from the table as an HTML table, using the th() and td() functions to produce table header and data cells, tr() to group cells into rows, and table() to produce the <table> tags that surround the rows.

The HTML table presents column headings as hyperlinks that redisplay the database table. These links include a sort_col parameter that explicitly specifies the column to use for sorting. For example, for a page that displays the contents of the grade_event table, the column heading links look like this:

```
<a href="/cgi-bin/db_browse.pl?tbl_name=grade_event&sort_col=date*">
   date</a>
<a href="/cgi-bin/db_browse.pl?tbl_name=grade_event&sort_col=category*">
   category</a>
<a href="/cgi-bin/db_browse.pl?tbl_name=grade_event&sort_col=event_id*">
   event_id</a>
```

display_table_contents() uses a little trick of turning empty values into a non-breaking space (&nbsp;). In a bordered table, some browsers don't display borders for empty cells properly; putting a non-breaking space in the cell fixes that problem.

If you want to write a more general script, you could alter db_browse.pl to browse multiple databases. For example, you could have the script begin by displaying a list of databases on the server, rather than a list of tables within a particular database. Then you could pick a database to get a list of its tables and go from there.

# 8.4.5 A Grade-Keeping Project Score Browser

Our next Web script, score_browse.pl, is designed to display scores that have been recorded for the grade-keeping project. Strictly speaking, we should have a way of entering the scores before we create a way of retrieving them, but I'm saving the score entry script until the next chapter. In the meantime, we do have several sets of scores in the database already from the early part of the grading period. We can use the script to display those scores, even in the absence of a convenient score-entry method. The script displays an ordered list of scores for any test or quiz, which is useful for determining the grading curve and assigning letter grades.

score_browse.pl has some similarities to db_browse.pl (both serve as information browsers), but is intended for the more specific purpose of looking at scores for a given quiz or test. The initial page presents a list of the possible grade events from which to choose, and enables the user to select any of them to see the scores associated with the event. Scores for a given event are sorted by score with the highest scores first, so you can use the result to determine the grading curve.
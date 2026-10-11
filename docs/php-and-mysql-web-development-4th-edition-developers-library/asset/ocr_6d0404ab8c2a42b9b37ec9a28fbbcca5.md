# **Note**

Although the GROUP BY column has a qualifier, it isn’t strictly necessary for this query. GROUP BY refers to output columns, and there is only one such column named student_id, so MySQL knows which one you mean.

The output produced by the query is fine if we want to know only which students had absences. But if we turn in this list to the school office, they might say, “What about the other students? We want a value for every student, even those who are not represented in the absence table. To write this query, use LEFT JOIN between the tables named in the FROM clause (rather than separating them by a comma), and an ON clause that says how to match up rows in the two tables. The query looks like this:

```
mysql> SELECT student.student_id, student.name, -> COUNT(absence.date) AS absences -> FROM student LEFT JOIN absence -> ON student.student_id = absence.student_id -> GROUP BY student.student_id;
```

| student_id | name | absences |
| :---: | :---: | :---: |
| 1 | Megan | 0 |
| 2 | Joseph | 0 |
| 3 | Kyle | 1 |
| 4 | Katie | 0 |
| 5 | Abby | 1 |
| 6 | Nathan | 0 |
| 7 | Liesl | 0 |
| ... | | |

Earlier, in Section 1.4.9.9, “Generating Summaries,” we ran a query that produced a numeric characterization of the data in the score table. Output from that query listed event ID but did not include event dates or categories, because we didn’t know then how to join the score table to the grade_event table to map the IDs onto dates and categories. Now we do. The following query is similar to one run earlier, but shows the dates and categories rather than simply the numeric event IDs:

```
mysql> SELECT -> grade_event.date, grade_event.category, -> MIN(score.score) AS minimum,
```
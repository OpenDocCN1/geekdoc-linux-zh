| Joseph | 2008-09-23 | 12 | Q | |
| Kylie | 2008-09-23 | 11 | Q | |
| Abby | 2008-09-23 | 13 | Q | |
| Nathan | 2008-09-23 | 18 | Q | |
| ... | | | | |

This query has several differences from the previous one:

+   - The *FROM* clause now includes the *student* table because the statement uses it in addition to the *grade_event* and *score* tables.
+   - The *student*_*id* column was unambiguous before, so it was possible to refer to it in either unqualified (*student*_*id*) or qualified (*score.student*_*id*) form. Now it is ambiguous because it is present in both the *score* and *student* tables. Therefore, it *must* be qualified as *score.student*_*id* or *student.student*_*id* to make it clear which table to use.
+   - The *ON* clause has an additional term specifying that *score* table rows are matched against *student* table rows based on student ID:
+   `ON ... score.student_id = student.student_id`
+   - The query displays the student name rather than the student ID. (You could display both if you wanted. Just add *student.student*_*id* to the list of output columns.)

With this query, you can plug in any date and get back the scores for that date, complete with student names and the score category. You don’t have to know anything about student IDs or event IDs. MySQL takes care of figuring out the relevant ID values and using them to match up table rows.

Another task the grade-keeping project involves is summarizing student absences. Absences are recorded by student ID and date in the *absence* table. To get student names (not just IDs), we need to join the *absence* table to the *student* table, based on the *student*_*id* value. The following query lists student ID number and name along with a count of absences:

```
```sql
mysql> SELECT student.student_id, student.name,
    -> COUNT(absence.date) AS absences
    -> FROM student INNER JOIN absence
    -> ON student.student_id = absence.student_id
    -> GROUP BY student.student_id;
```
```

| *student*_*id* | *name* | *absences* |
| | | |
| 3 | Kylie | 1 |
| 5 | Abby | 1 |
| 10 | Peter | 2 |
| 17 | Will | 1 |
| 20 | Avery | 1 |
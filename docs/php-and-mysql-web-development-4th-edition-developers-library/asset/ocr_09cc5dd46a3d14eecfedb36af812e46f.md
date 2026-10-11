The constraints that foreign keys enforce often are not difficult to implement through application logic. Sometimes, it's simply a matter of how you approach the data-entry process. Consider the student and score tables from the grade-keeping project. These are related by a foreign key relationship through the student_id values in each table. Suppose that we had created these as MySQL tables rather than as InnoDB tables. MySQL does not support foreign keys, so in this case the relationship between the tables would be implicit rather than explicit. When you administer a test or quiz and have a new set of scores to add to the database, you'd have to make sure that you don't add score rows containing student_id values that are not listed in the student table.

In some respects, this is just a matter of taking the proper approach to data entry. To avoid inserting scores for nonexistent students, the way you'd enter a set of scores probably would be to use an application that begins with a list of students from the student table. For each one, it would take the score and use the student's ID number to generate a new score table row. With this procedure, you would never enter a row for a student that doesn't exist. Nevertheless, it would still be *possible* to enter a bad row, for example, if you issued an `INSERT` statement manually. (With InnoDB tables and foreign keys, no such possibility exists.)

What about the case where you delete a student row? Suppose that you want to delete student number 13. This also implies you want to delete any score rows for that student. With a *foreign key relationship* in place that specifies cascading delete, you'd simply delete the student table row with the following statement and let MySQL take care of removing the corresponding score table rows automatically:

```
DELETE FROM student WHERE student_id = 13;
```

Without foreign key support, you must explicitly delete rows for all relevant tables to achieve the same effect as cascading on `DELETE`:

```
DELETE FROM student WHERE student_id = 13;
DELETE FROM score WHERE student_id = 13;
```

Another way to do this is to use a multiple-table delete that achieves the same effect as a cascaded delete with a single query. But watch out for a subtle trap. The following statement appears to do the trick, but it's actually not quite correct:

```
DELETE student, score FROM student INNER JOIN score
ON student.student_id = score.student_id WHERE student.student_id = 13;
```

The problem with this statement is that it will fail in the case where the student doesn't have any scores. The `WHERE` clause will find no matches and thus will not delete anything from the student table. In this case, a `LEFT JOIN` is more appropriate, because it will identify which student table row to delete even in the absence of any matching score table rows:

```
DELETE student, score FROM student LEFT JOIN score USING (student_id)
WHERE student.student_id = 13;
```
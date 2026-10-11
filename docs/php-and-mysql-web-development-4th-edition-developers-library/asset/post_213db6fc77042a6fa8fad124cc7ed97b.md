
## 2.8 Performing Multiple-Table Retrievals with Joins

Like INNER JOIN, a LEFT JOIN can be written using an ON clause or a USING() clause to specify the matching conditions. As with INNER JOIN, ON can be used whether or not the joined columns from each table have the same name, but USING() requires that they have the same names.

LEFT JOIN has a few synonyms and variants. LEFT OUTER JOIN is a synonym for LEFT JOIN. MySQL also supports an ODBC-style notation for LEFT OUTER JOIN that uses curly braces and `OJ` (“outer join”):

```text
mysql> SELECT t1.* FROM { OJ t1 LEFT OUTER JOIN t2 ON t1.ii = t2.ij }
       -> WHERE t2.i2 IS NULL;
----------
| ii | c1 |
----------
| 1  | a  |
----------
```

NATURAL LEFT JOIN is similar to LEFT JOIN; it performs a LEFT JOIN, matching all columns that have the same name in the left and right tables. (Thus, no ON or USING clause is given.)

As already mentioned, LEFT JOIN is useful for answering “Which values are missing?” questions. Let’s apply this principle to the tables in the sampdb database and consider a more complex example than those shown earlier using t1 and t2.

For the grade-keeping project, first mentioned in Chapter 1, we have a student table listing students, a grade_event table listing the grade events that have occurred, and a score table listing scores for each grade event for each student. However, if a student was ill on the day of some quiz or test, the score table wouldn’t contain any score for the student for that event. A makeup quiz or test should be given in such cases, but how do we find these missing rows?

The problem is to determine which students have no score for a given grade event, and to do this for each grade event. Another way to say this is that we want to find out which combinations of student and grade event are not present in the score table. This “which values are not present” wording is a tip-off that we want a LEFT JOIN. The join isn’t as simple as in the previous examples, though: We aren’t just looking for values that are not present in a single column; we’re looking for a two-column combination. The combinations we want are all the student/event combinations. These are produced by joining the student table to the grade_event table:

```text
FROM student INNER JOIN grade_event
```

Then we take the result of that join and perform a LEFT JOIN with the score table to find the matches for student ID/event ID pairs:

```text
FROM student INNER JOIN grade_event
LEFT JOIN score ON student.student_id = score.student_id
AND grade_event.event_id = score.event_id
```

Note that the `ON` clause allows the rows in the `score` table to be joined according to matches in different tables named earlier in the join. That's the key for solving this problem. The `LEFT JOIN` forces a row to be generated for each row produced by the cross join of the `student` and `grade_event` tables, even when there is no corresponding `score` table row. The result set rows for these missing score rows can be identified by the fact that the columns from the `score` table will all be `NULL`. We can identify these rows by adding a condition in the `WHERE` clause. Any column from the `score` table will do, but because we're looking for missing scores, it's probably conceptually clearest to test the `score` column:

```text
WHERE score.score IS NULL
```

We can also sort the results using an `ORDER BY` clause. The two most logical orderings are by event per student and by student per event. I'll choose the first:

```text
ORDER BY student.student_id, grade_event.event_id
```

Now all we need to do is name the columns we want to see in the output, and we're done. Here is the final statement:

```sql
SELECT
    student.name,  student.student_id,
    grade_event.date, grade_event.event_id,  grade_event.category
FROM
    student INNER JOIN grade_event
    LEFT JOIN score ON student.student_id = score.student_id
                AND grade_event.event_id = score.event_id
WHERE
    score.score IS NULL
ORDER BY
    student.student_id, grade_event.event_id;
```

Running the query produces these results:

| name | student_id | date | event_id | category |
|---|---|---|---|---|
| Megan | 1 | 2008-09-16 | 4 | Q |
| Joseph | 2 | 2008-09-03 | 1 | Q |
| Katie | 4 | 2008-09-23 | 5 | Q |
| Devi | 13 | 2008-09-03 | 1 | Q |
| Devi | 13 | 2008-10-01 | 6 | T |
| Will | 17 | 2008-09-16 | 4 | Q |
| Avery | 20 | 2008-09-06 | 2 | Q |
| Gregory | 23 | 2008-10-01 | 6 | T |
| Sarah | 24 | 2008-09-23 | 5 | Q |
| Carter | 27 | 2008-09-16 | 4 | Q |
| Carter | 27 | 2008-09-23 | 5 | Q |
| Gabrielle | 29 | 2008-09-16 | 4 | Q |
| Grace | 30 | 2008-09-23 | 5 | Q |

Here's a subtle point. The output displays the student IDs and the event IDs. The student_id column appears in both the student and score tables, so at first you might think that the output column list could name either student.student_id or score.student_id. That's not the case, because the entire basis for being able to find the rows we're interested in is that all the score table columns are returned by the LEFT JOIN as NULL. Selecting score.student_id would produce only a column of NULL values in the output. The same principle applies to deciding which event_id column to display. It appears in both the grade_event and score tables, but the query selects grade_event.event_id because the score.event_id values will always be NULL.

## 2.9 Performing Multiple-Table Retrievals with Subqueries

Subquery support is a capability that allows one SELECT statement to be written within parentheses and nested inside another. Here's an example that looks up the IDs for grade event rows that correspond to tests ('T') and uses them to select scores for those tests:

```sql
SELECT * FROM score
WHERE event_id IN (SELECT event_id FROM grade_event WHERE category = 'T');
```

Subqueries can return different types of information:

- A scalar subquery returns a single value.
- A column subquery returns a single column of one or more values.
- A row subquery returns a single row of one or more values.
- A table subquery returns a table of one or more rows of one or more columns.

Subquery results can be tested in different ways:

- Scalar subquery results can be evaluated using relative comparison operators such as = or <.
- IN and NOT IN test whether a value is present in a set of values returned by a subquery.
- ALL, ANY, and SOME compare a value to the set of values returned by a subquery.
- EXISTS and NOT EXISTS test whether a subquery result is empty.

A scalar subquery is the most restrictive because it produces only a single value. But as a consequence, scalar subqueries can be used in the widest variety of contexts. They are applicable essentially anywhere that you can use a scalar operand, such as a term of an expression, as a function argument, or in the output column list. Column, row, and table subqueries that return more information cannot be used in contexts that require a single value.

Subqueries can be correlated or uncorrelated. This is a function of whether a subquery refers to and is dependent on values in the outer query.

You can use subqueries with statements other than SELECT. However, for statements that modify tables (INSERT, REPLACE, DELETE, UPDATE, LOAD DATA) there is currently a restriction that the subquery cannot refer to the table being modified.

In some cases, subqueries can be rewritten as joins. You might find subquery rewriting techniques useful if you’re writing queries that need to run on an older MySQL server, or if you want to see whether the MySQL optimizer does a better job with a join than a subquery.

The following sections discuss the kinds of operations you can use to test subquery results, how to write correlated subqueries, and how to rewrite subqueries as joins.

### 2.9.1 Subqueries with Relative Comparison Operators

The =, <>, >, >=, <, and <= operators perform relative-value comparisons. When used with a scalar subquery, they find all rows in the outer query that stand in particular relationship to the value returned by the subquery. For example, to identify the scores for the quiz that took place on '2008-09-23', use a scalar subquery to determine the quiz event ID and then match score rows against that ID in the outer SELECT:

```sql
SELECT * FROM score
WHERE event_id =
(SELECT event_id FROM grade_event
 WHERE date = '2008-09-23' AND category = 'Q');
```

With this form of statement, where the subquery is preceded by a value and a relative comparison operator, it is necessary that the subquery produce a single value. That is, it must be a scalar subquery; if it produces multiple values, the statement will fail. In some cases, it may be appropriate to satisfy the single-value requirement by limiting the subquery result with LIMIT 1.

Use of scalar subqueries with relative comparison operators is handy for solving problems where you’d be tempted to use an aggregate function in a WHERE clause. For example, to determine which of the presidents in the president table was born first, you might try this statement:

```sql
SELECT * FROM president WHERE birth = MIN(birth);
```

That doesn’t work because you can’t use aggregates in WHERE clauses. The WHERE clause determines which rows to select, but the value of MIN() isn’t known until after the rows have already been selected. However, you can use a subquery to produce the minimum birth date like this:

```sql
SELECT * FROM president
WHERE birth = (SELECT MIN(birth) FROM president);
```

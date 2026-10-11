Here again the table definition contains something new: the FOREIGN KEY construct. We'll get to this in just a bit.

Create the table by typing the statement into *mysql* or by executing the following command:

```
$ mysq1 sampdb < create_score.sql
```

The *score* column is an **INT** to hold integer score values. If you wanted to allow scores such as 58.5 that have a fractional part, you'd use one of the data types that can represent them, such as **DECIMAL** or **FLOAT**.

The *student_id* and *event_id* columns are integer columns that indicate the student and event to which each score applies. By using them to link to the corresponding ID value columns in the *student* and *grade_event* tables, we'll be able to look up the student name and event date. There are a couple important points to note about the *student_id* and *event_id* columns:

+   - We've made the combination of the two columns a **PRIMARY KEY**. This ensures that we won't have duplicate scores for a student for a given quiz or test. Note that it's the combination of *event_id* and *student_id* that is unique. In the *score* table, neither value is unique by itself. There will be multiple score rows for each *event_id* value (one per student), and multiple rows for each *student_id* value (one for each quiz and test) taken by the student.

+   - For each ID column, a **FOREIGN KEY** clause defines a constraint. The **REFERENCES** part of the clause indicates which table and column the *score* column refers to. The constraint on *event_id* is that each value in the column must match some *event_id* value in the *grade_event* table. Similarly, each *student_id* value in the *score* table must match some *student_id* value in the *student* table.

The **PRIMARY KEY** definition ensures that we won't create duplicate score rows. The **FOREIGN KEY** definitions ensure that we won't have rows with bogus ID values that don't exist in the *grade_event* or *student* tables.

Why is there an index on *student_id*? The reason is that, for any columns in a **FOREIGN KEY** definition, there should be an index on them, or they should be the columns that are listed first in a multiple-column index. For the **FOREIGN KEY** on *event_id*, that column is listed first in the **PRIMARY KEY**. For the **FOREIGN KEY** on *student_id*, the **PRIMARY KEY** cannot be used because *student_id* is not listed first. So, instead, we create a separate index on *student_id*.

InnoDB actually will create an index on columns in a foreign key definition, but it might not use the same index definition you would (as discussed further in Section 2.14.1, “Creating and Using Foreign Keys”). Defining the index explicitly avoids this issue.

# 1.4.6.2.4 The absence Table

The *absence* table for recording lapses in attendance looks like this:

```
CREATE TABLE absence (
```
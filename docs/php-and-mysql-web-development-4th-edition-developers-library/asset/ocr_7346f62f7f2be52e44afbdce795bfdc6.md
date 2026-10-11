# 1.4 A MySQL Tutorial 49

You'll note from Figure 1.7 that I added something to the student table that wasn't in your gradebook: It contains a column for recording sex. This will allow for simple things such as counting the number of boys and girls in the class or more complex things like comparing scores for boys and girls.

We're almost done designing the tables for the grade-keeping project. We need just one more table to record absences for attendance purposes. Its contents are relatively straightforward: a student ID number and a date (see Figure 1.8). Each row in the table indicates that the given student was absent on the given date. At the end of the grading period, we'll call on MySQL's counting abilities to summarize the table's contents to tell us how many days each student was absent.

![](bbox=[0.36, 0.37, 0.64, 0.49])

# 1.4.6.2.1 The student Table

Now that we know what our grade-keeping tables should look like, we're ready to create them. The CREATE TABLE statement for the student table looks like this:

```
```
CREATE TABLE student
(
  name        VARCHAR(20) NOT NULL,
  sex         ENUM('F','M') NOT NULL,
  student_id  INT UNSIGNED NOT NULL AUTO_INCREMENT,
  PRIMARY KEY (student_id)
) ENGINE = InnoDB;
```
```

Observe that I've added something new to the CREATE TABLE statement (the ENGINE clause at the end). I'll explain its purpose shortly.

Type the CREATE TABLE statement into mysql or execute the following command:

```
`mysql sampdb < create_student.sql`
```

The CREATE statement creates a table named student with three columns: name, sex, and student_id.

name is a variable-length string column that can hold up to 20 characters. This name representation is simpler than the one used for the Historical League tables; it uses a single column rather than separate first name and last name columns. That's because I know in advance that no grade-keeping query examples will need to do anything that would work better with separate columns. (Yes, that's cheating. I admit it. In practice, you would use multiple columns.)
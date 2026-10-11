The next line is the SQL query. This query inserts the data into the database with an INSERT statement. A typical INSERT statement looks like this:

```
INSERT INTO table(field1, field2)
VALUES ('data for field 1', 'data for field 2');
```

When you construct the SQL statement in your sql variable, you concatenate the various variables from the form that are accessed with _POST. To demonstrate how this fits together, imagine that you are adding a comment to the blog entry with 2 as an ID, at 2:30 p.m. on August 10, 2005. Assume that the user types "Bob Smith" as the name and "I really like your blog. Cool stuff!" as the comment. Table 4-5 demonstrates how the query is built.

# TABLE 4-5 The sql variable is built up into an INSERT statement

|
|---|---|
| CONCATENATED ELEMENT | SQL STATEMENT |
| INSERT INTO comments(blog_id, dateposted, name, comment) VALUES( | INSERT INTO comments(blog_id, dateposted, name, comment) VALUES( |
| validentry | $INSERT INTO comments(blog_id, dateposted, name, comment) VALUES(2 |
| , NOW(), ' | INSERT INTO comments(blog_id, dateposted, name, comment) VALUES(2, 2005-08-10 14:30:00, ' |
| $_POST['name'] | INSERT INTO comments(blog_id, dateposted, name, comment) VALUES(2, 2005-08-10, 'Bob Smith |
| ', ' | INSERT INTO comments(blog_id, dateposted, name, comment) VALUES(2, 2005-08-10, 'Bob Smith',' |
| $_POST['comment'] | INSERT INTO comments(blog_id, dateposted, name, comment) VALUES(2, 2005-08-10, 'Bob Smith', 'I really like your blog. Cool stuff!' |
| '); | INSERT INTO comments(blog_id, dateposted, name, comment) VALUES(2, 2005-08-10, 'Bob Smith', 'I really like your blog. Cool stuff!'); |
|
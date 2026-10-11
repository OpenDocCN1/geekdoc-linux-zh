# **UPDATE statement**

This statement is used to update rows existing in a table, the syntax as shown:

```
    UPDATE <target_table>
    SET <col_name> = <value> [ , <col_name> = <value> , ... ]
    [ FROM <additional_tables> ]
    [ WHERE <condition> ]
```

The following example will update the field **phone** for the user with the name *Alberto* in the field *name*. As this field is not *unique*, this operation can update several records if the name is duplicated.

```
    UPDATE students SET phone = "657225520" WHERE name = "Alberto";
```

# **DELETE statement**

This statement is used to remove rows from an existing table. The syntax is as follows:

```
    DELETE FROM <table_name>
    [ WHERE <condition> ]
```

In most of the cases, it is important to use the clause **WHERE** to limit the records to be removed. If it is not specified, all the records will be removed. The following example removes the student with the associated *id* to the number 1.

```
    DELETE FROM students WHERE id = 1;
```

# **GRANT statement**

Assign privileges to user accounts and roles. Syntax is complex and depends of the database system used, the basic syntax is as follows:

```
    GRANT privilege
    ON object_type
    TO user_or_role;
```

For example, to provide full access to the user *agonzalez* when it is connecting from localhost to the previous database created called the *school*, the following syntax will perform the action:

```
    GRANT ALL_PRIVILEGES ON school.* TO 'agonzalez@'localhost';
```

# **REVOKE statement**
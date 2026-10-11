+   A trigger can examine the current contents of a row before it is deleted or updated. This capability can be exploited to perform logging of changes to existing rows, for example.

To create a trigger, use the CREATE TRIGGER statement. The definition indicates the particular type of statement for which the trigger activates (INSERT, UPDATE, or DELETE), and whether it activates before or after rows are modified. The basic syntax for trigger creation looks like this:

```
CREATE TRIGGER *trigger_name*  # the trigger name
[BEFORE | AFTER]            # when the trigger activates
[INSERT | UPDATE | DELETE] # what statement activates it
ON *tbl_name*                 # the associated table
FOR EACH ROW *trigger_stm*; # what the trigger does
```

*tbl_name* is the table with which the trigger is associated; *trigger_name* is the name of the trigger itself. For trigger naming, I like to adopt a convention that helps make the trigger purpose and table association clear, such as bi_*tbl_name* or ai_*tbl_name* for a BEFORE INSERT or AFTER INSERT trigger on *tbl_name*.

*trigger_stm* is the trigger body; that is, the statement that executes when the trigger activates. In a trigger body, the syntax NEW.*col_name* can be used to refer to columns in the new row to be inserted or updated in an INSERT or UPDATE trigger. Similarly, OLD.*col_name* can be used to refer to columns in the old row to be deleted or updated in a DELETE or UPDATE trigger. To change a column value within a BEFORE trigger before the value is stored in the table, use SET NEW.*col_name* = *value*.

The following example shows a trigger bi_t for INSERT statements for a table t that has an integer percent column for storing percentage values (0 to 100) and a DATETIME column. The trigger uses BEFORE so that it can examine data values before they are inserted into the table.

```
mysql> CREATE TABLE t (percent INT, dt DATETIME);
mysql> delimiter $
mysql> CREATE TRIGGER bi_t BEFORE INSERT ON t
-> FOR EACH ROW BEGIN
->   SET NEW.dt = CURRENT_TIMESTAMP;
->   IF NEW.percent < 0 THEN
->      SET NEW.percent = 0;
->   ELSEIF NEW.percent > 100 THEN
->      SET NEW.percent = 100;
->   END IF;
-> END$
mysql> delimiter ;
```

The trigger performs two actions:

+   For attempts to insert a percentage value that lies outside the range from 0 to 100, the trigger converts the value to the nearest endpoint.
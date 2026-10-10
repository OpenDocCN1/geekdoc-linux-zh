The variable **n** in the trigger definition represents the new value in an INSERT, that is, the value being inserted. The trigger will check the validity of what is being inserted into the table. If the column ENDING has no value during an INSERT, the trigger will ensure it has the value of the column STARTING plus 1 hour.

*Listing 3.11* shows the statements you can try to test the trigger, and the corresponding output.

```
C:\Program Files\IBM\SQLLIB\BIN>db2 insert into cl_sched (class_code, day, starting) values ('abc',1,current_time)
DB20000I The SQL command completed successfully.

C:\Program Files\IBM\SQLLIB\BIN>db2 select * from cl_sched

CLASS_CODE DAY  STARTING ENDING
--------  ----  ---------- -------
042:BF    4 12:10:00 14:00:00
553:MJA   1 10:30:00 11:00:00
543:CWM   3 09:10:00 10:30:00
778:RES   2 12:10:00 14:00:00
044:HD    3 17:12:30 18:00:00
abc       1 11:06:53 12:06:53

6 record(s) selected.
```

# Listing 3.11 - Testing the before trigger created earlier

In the above listing you can see that there was no value passed for the ENDING column in the INSERT statement; therefore its value is NULL. Also the CURRENT TIME is a special DB2 register returning the time it was invoked. In this example, the current time is 11:06:53, therefore this value is assigned to the STARTING column, while the ENDING column gets what the trigger logic assigns to it, which is 11:06:53 plus 1 hour.

The trigger `validate_sched` shown below extends the functionality of the `default_class_end` trigger previously described to add additional conditions.

```
CREATE TRIGGER validate_sched
NO CASCADE BEFORE INSERT ON cl_sched
REFERENCING NEW AS n
FOR EACH ROW
MODE DB2SQL
BEGIN ATOMIC
-- supply default value for ending time if null
IF (n.ending IS NULL) THEN
SET n.ending = n.starting + 1 HOUR;
END IF;
```
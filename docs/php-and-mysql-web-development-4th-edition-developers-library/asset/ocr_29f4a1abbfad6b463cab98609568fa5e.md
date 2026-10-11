decimal places of accuracy. The advantage of DECIMAL is that values are not subject to roundoff error and calculations are exact.

+   You can represent all monetary values internally as cents using an integer type. The advantage is that calculations are done internally using integers, which is very fast. The disadvantage is that you will need to convert values on input or output by multiplying or dividing by 100.

Some kinds of "numbers" aren't. Telephone numbers, credit card numbers, and Social Security numbers all can be written using non-digit characters such as spaces or dashes and cannot be stored directly in a numeric column unless you strip the non-digits. But even with non-digits stripped, you may want to store values as strings rather than as numbers to avoid loss of leading zeros.

If you need to store date information, do the values include a time? That is, will they ever need to include a time? MySQL doesn't provide a date type that has an optional time part: DATE never has a time, and DATETIME must have a time. If the time really is optional, use a DATE column to record the date, and a separate TIME column to record the time. Then allow the TIME column to be NULL and interpret that as "no time".

```
CREATE TABLE mytbl
(
    date DATE NOT NULL,  # date is required
    time TIME NULL        # time is optional (may be NULL)
);
```

One type of situation in which it's especially important to determine whether you need a time value occurs when you're joining two tables with a master-detail relationship that are "linked" based on date information. Suppose that you're conducting research involving test subjects. Following a standard initial battery of tests, you might run several additional tests, with the choice of tests varying according to the results of the initial tests. You can represent this information using a master-detail relationship, in which the subject identification information and the standard initial tests are stored in a master row and any additional tests are stored as rows in a secondary detail table. That you link together the two tables based on subject ID and the date on which the tests are given.

The question you must answer in this situation is whether you can use just the date or whether you need both date and time. This depends on whether a subject might go through the testing procedure more than once during the same day. If so, record the time (for example, the time that the procedure begins), using either a DATETIME column or separate DATE and TIME columns that both must be filled in. Without the time value, you will not be able to associate a subject's detail rows with the proper master rows if the subject is tested twice in a day.

I've heard people claim: "I don't need a time; I'll never test a subject twice on the same day." Sometimes they're correct, but I have also seen some of these same people turn up later wondering how to prevent detail rows from being mixed up with the wrong
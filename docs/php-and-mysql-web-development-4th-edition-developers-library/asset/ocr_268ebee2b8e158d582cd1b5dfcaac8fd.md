+   - **Storage required.** 3 bytes
+   - **DATETIME**
+       - **Meaning.** A date and time value, in `CCYY-MM-DD hh:mm:ss` format
+       - **Allowable attributes.** None, other than the global attributes
+       - **Range.** `1000-01-01 00:00:00` to `9999-12-31 23:59:59`
+       - **Zero value.** `0000-00-00 00:00:00`
+       - **Default value.** NULL if the column can be NULL, `0000-00-00 00:00:00` if NOT NULL
+   - **Storage required.** 8 bytes
+   - **TIME**
+       - **Meaning.** A time, in `hh:mm:ss` format (or `-hh:mm:ss` for negative values).
+       - **Allowable attributes.** None, other than the global attributes
+       - **Range.** `-838:59:59` to `838:59:59`
+       - **Zero value.** `00:00:00`
+       - **Default value.** NULL if the column can be NULL, `00:00:00` if NOT NULL
+       - **Storage required.** 3 bytes
+       - **Note.** Although `00:00:00` is used as the zero value when illegal values are inserted into a TIME column, it is also a legal value that lies within the normal column range.
+   - **TIMESTAMP**
+       - **Meaning.** A timestamp (date and time), in `CCYY-MM-DD hh:mm:ss` format. The TIMESTAMP type has several special behaviors:
+           - Inserting a NULL into any TIMESTAMP column of a table inserts the current date and time, unless the column has been declared to allow NULL.
+           - One TIMESTAMP column per table can have two auto-modification properties:
+               - **Automatic initialization:** When a row is created, the default value for the column is the current timestamp.
+               - **Automatic updating:** When a row is updated, changing the value of any other column in the row causes the TIMESTAMP column to be updated to the date and time at which the modification occurs.
+       - You can designate which TIMESTAMP should be treated this way, and you can suppress automatic initialization, updating, or both. See Chapter 3 for additional details.
+       - **Allowable attributes.** One TIMESTAMP column in a table can have attributes of DEFAULT CURRENT_TIMESTAMP or ON UPDATE CURRENT_TIMESTAMP, or both. (You cannot use one attribute with one TIMESTAMP column and the other attribute with...
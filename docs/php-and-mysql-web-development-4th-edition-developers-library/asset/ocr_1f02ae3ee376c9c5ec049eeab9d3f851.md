# B.2.3 ENUM and SET Types

+   - `ENUM`('`value1`', '`value2`', ...)

    **Meaning.** An enumeration; column values can be assigned exactly one member of the value list

    **Allowable attributes.** `CHARACTER SET`, `COLLATE`

    **Default value.** `NULL` if the column can be `NULL`, first enumeration value if `NOT NULL`

    **Storage required.** 1 byte for enumerations with 1 to 255 members, 2 bytes for enumerations with 256 to 65535 members

    **Comparisons.** Based on the numeric value of column values

    **Note.** In the data type definition, any trailing spaces present in member values are ignored.

+   - `SET`('`value1`', '`value2`', ...)

    **Meaning.** A set; column values can be assigned zero or more members of the value list

    **Allowable attributes.** `CHARACTER SET`, `COLLATE`

    **Default value.** `NULL` if the column can be `NULL`, ``''`` (empty set) if `NOT NULL`

    **Storage required.** 1 byte (for sets with 1 to 8 members), 2 bytes (9 to 16 members), 3 bytes (17 to 24 members), 4 bytes (25 to 32 members), or 8 bytes (33 to 64 members)

    **Comparisons.** Based on the numeric value of column values

    **Note.** In the data type definition, any trailing spaces present in member values are ignored.

# B.3 Date and Time Types

MySQL provides several types to represent temporal data. Types are available for dates and times, either separate or in combination. There is a special timestamp type that is updated automatically when a row changes, and a type for storing years when you don't need a complete date.

The terms `CC`, `YY`, `MM`, and `DD` in date formats represent century, year, month, and day of month, respectively. The terms `hh`, `mm`, and `ss` in time formats represent hour, minute, and second, respectively.

+   - `DATE`
+       - **Meaning.** A date, in `'`YYYY-MM-DD`'` format
+       - **Allowable attributes.** None, other than the global attributes
+       - **Range.** `'`1000-01-01`'` to `'`9999-12-31`'`
+       - **Zero value.** `'`0000-00-00`'`
+       - **Default value.** `NULL` if the column can be `NULL`, `'`0000-00-00`'` if `NOT NULL`
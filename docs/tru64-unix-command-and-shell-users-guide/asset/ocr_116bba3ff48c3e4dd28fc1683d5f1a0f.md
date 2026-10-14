Some collation rules ignore certain characters. For example, if the hyphen (-) is defined as a character to be ignored, the strings `re-locate` and `relocate` sort to the same position.

> **Note**
> 
> This means that you cannot assume that the range (A to Z, a to z) includes every letter of an alphabet. For example, the Danish alphabet includes three characters that sort after z.

# C.2.2 Date and Time Formats

Users around the world express dates and times with different formatting conventions. When specifying day and month names, people in the United States generally express dates with an expression like the following one:

```
Tuesday, May 22, 1996
```

The French, on the other hand, express dates this way:

```
mardi, 22 mai 1996
```

The following examples show alternative formats for the date, March 20, 1996. A given format is not the only way to write the date in the listed country:

+   - `3/20/96` (United States)
+   - `20/3/96` (Great Britain)
+   - `20.3.96` (France and Germany)
+   - `20-III-96` (Italy)
+   - `96/3/20` (Japan)
+   - `2/3/20` (Japan, Emperor format)

In Japan’s Emperor format, the year (2, in the preceding example) is expressed as the number of years that the current emperor has reigned.

As with dates, there are many conventions for expressing the time of day. In the United States, people often use the 12-hour clock with its a.m. and p.m. designations. People in most other countries use the 24-hour clock to express the time.
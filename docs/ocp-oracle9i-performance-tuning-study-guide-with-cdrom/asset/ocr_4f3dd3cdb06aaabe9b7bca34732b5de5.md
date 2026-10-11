This use of the TKPROF utility would:

+   * Format the trace file `ora_1702.trc` and store the results, sorted by the number of rows returned by each statement, in an output file called `trace.txt`. A discussion of other TKPROF sorting options appears in the next section.
+   * Create a second file called `trace.sql` that contains the SQL commands needed to create a table called `TKPROF_TABLE` and then populate it with the statistics for the SQL statements in the trace file.

Without a sort parameter like FCHROW, the TKPROF utility would list the SQL statements in the formatted output file in the order in which they were executed. When this default sort order is not desired, TKPROF has several additional sorting parameters. The formatted output will be sorted in descending order, according to the option you specify. Multiple sort parameters can also be used simultaneously. In these cases the sorted output will be sorted in the order specified, but is based on the sum of the values for the sorted option.

# TKPROF Sorting Parameters

Each parameter is related to one of the three phases of SQL statement processing: Parse, Execute, or Fetch. *Parsing* refers to the process of getting an SQL statement ready to execute. This process includes checking the statement for syntactic correctness and determining the user's privileges on objects referenced in the statement. TKPROF sort options related to the parse phase of SQL statement processing are shown in Table 3.2.

TABLE 3.2 Sort Options for the Parse Phase of Statement Processing
| Option | Sort Order |
| :--- | :--- |
| PRSCNT | Number of times the statement was parsed |
| PRSCPU | Amount of CPU time spent parsing the statement |
| PRSELA | Elapsed time spent parsing the statement |
| PRSDSK | Number of disk reads that occurred while the statement was being parsed |
| PRSMIS | Number of Library Cache misses while the statement was being parsed |
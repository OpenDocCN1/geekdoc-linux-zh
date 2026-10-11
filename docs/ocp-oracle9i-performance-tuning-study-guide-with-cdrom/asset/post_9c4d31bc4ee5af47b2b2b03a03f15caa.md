
# Chapter 3
# SQL Application Tuning and Design

## ORACLE9i PERFORMANCE TUNING EXAM OBJECTIVES COVERED IN THIS CHAPTER:

- Describe the role of the DBA in tuning applications
- Explain different storage structures and why one storage structure might be preferred over another
- Explain the different types of indexes
- Explain Index Organized Tables
- Describe partitioning methods
- Explain the use of the DBMS_STATS procedure
- Describe Materialized Views and the use of Query Rewrites
- List requirements for OLTP, DSS, and Hybrid Systems
- Describe how the Optimizer is used
- Explain the concept of plan stability
- Use stored outlines
- Describe how hints are used
- Collect statistics on indexes and tables
- Describe the use of histograms
- Copy statistics between databases
- Perform index reorganization
- Monitor indexes to determine usage

Exam objectives are subject to change at any time without prior notice and at Oracle’s sole discretion. Please visit Oracle’s Certification website (http://www.oracle.com/education/certification/) for the current exam objectives listing.

Problems with poorly performing applications can frequently be traced to badly structured SQL statements or inefficient database design. Because of this, Oracle provides you with several tools to help you identify and remedy poorly performing application SQL.

These tools can be very valuable on development systems where application code is still being refined. However, even on production systems, where Oracle’s newer tuning principles recognize that tuning application SQL or design is difficult or impossible, these tools may help you identify SQL statements that might benefit from more broad DBA intervention—like adding an index to improve the performance of a long-running report query.

### Oracle Objective
**Describe the role of the DBA in tuning applications**

Tuning modifications of this type require that you understand all the tuning options available to you, from SQL hints and stored outlines to materialized views and index-organized tables. You must also consider whether the tools available to you are appropriate given the type of system that is being evaluated. For example, Online Transaction Processing Systems have different SQL and design considerations than do Decision Support Systems.

However, no matter the type of system, or what type of tuning problem you face, you must first accurately measure the performance of the current application SQL before identifying areas of possible improvement.

## Measuring SQL Performance

Effective database tuning requires that you take accurate and timely measurements of specific SQL activity occurring within the application.

Once these measurements are taken, you can attempt to improve their performance using a variety of techniques. A complete discussion of SQL statement tuning techniques is beyond the scope of this book and the Performance Tuning OCP exam. However, as a DBA, it is important for you to understand the five most commonly used tools for measuring the performance of SQL statements: the TKPROF utility, Top SQL, Explain Plans, AUTOTRACE, and STATSPACK reports.

## The TKPROF Utility

The Trace Kernel Profile, or *TKPROF*, utility is used to format user trace files that were generated using one of the user session tracing techniques discussed in Chapter 2, “Sources of Tuning Information.” User trace files contain all the SQL statements that the user issued while tracing was active, information about how long each statement took to execute, and the number of resources the statement consumed.

**Oracle Objective**
**Use SQL Trace and TKPROF**

Because the contents of a raw, unformatted trace file are difficult to interpret, the TKPROF utility is used to convert the trace file into a form you can more easily understand. The following sections explain how to use this utility.

### Formatting a User Trace File Using TKPROF

The TKPROF utility is a stand-alone utility that is executed directly from the operating system prompt. The following shows a simple TKPROF formatting example taken from a Unix system:

```
$ tkprof ora_1253.trc trace.txt
```

This example would format a user trace file called **ora_1253.trc** and store the formatted version in a file called **trace.txt**. As this example shows, the first two parameters to follow the TKPROF command are the name of the trace file and the output file, respectively. The TKPROF utility has several additional command line arguments that can also be used when formatting the trace file, depending on what information is desired. These options are specified on the command line immediately after the required trace file name and output file name parameters. A listing of these options is shown in Table 3.1.

**TABLE 3.1** *TKPROF Command Line Options*

| Option | Definition and Usage |
| :--- | :--- |
| EXPLAIN | Generates an Explain Plan for each statement in the trace file by using the PLAN_TABLE in the schema specified by this command. This option must include a valid Oracle username and password. |
| TABLE | Using the schema specified by the EXPLAIN option, the execution plan is stored in the specified table rather than default table, PLAN_TABLE. |
| SYS | Indicates whether the formatted file should include recursive SQL statements (i.e., statements implicitly issued against the data dictionary in support of the primary SQL statements). |
| SORT | Determines the order in which the statements in the formatted trace file will be sorted. The 22 sort options are listed in Tables 3.2, 3.3, and 3.4. |
| RECORD | Specifies the filename into which the SQL statements in the trace file should be written. Allows you to isolate the SQL statements without any accompanying resource usage information. Recursive SQL will be omitted. |
| PRINT | Limits the number of SQL statements included in the resulting formatted trace file to the specified value. |
| INSERT | Creates an SQL script that, when executed, will create a table called TKPROF_TABLE and then populate this table with the raw statistics contained in this trace file. |
| AGGREGATE | Determines whether the statistics from multiple issuers of the same SQL statement will be counted together or independently. |
| WAITS | Calculates summary statistics for wait events that occurred within the trace. Wait events are discussed in Chapter 9, “Tuning Contention.” |

Several examples demonstrating the use of TKPROF with some of these options are shown below.

The following demonstrates the use of the TKPROF with SYS and EXPLAIN parameters on a Unix system:

```
$ tkprof ora_1234.trc trace.txt sys=no explain=jo e/sidney@PROD
```

This use of TKPROF would:

- Format the trace file `ora_1234.trc` and store the results in an output file called `trace.txt`.
- Cause any recursive SQL in the original trace file to be omitted from the formatted trace file, `trace.txt`.
- Include in the formatted trace file, `trace.txt`, Explain Plans of each SQL statement issued. The `PLAN_TABLE` in the user Joe’s schema in the PROD database would be used to generate the Explain Plans.

The following demonstrates the use of TKPROF with RECORD and PRINT parameters on a Windows 2000 system:

```
C:\> tkprof ora00740.trc trace.txt print=10 record=sql.txt
```

This use of the TKPROF utility would:

- Format the trace file `ora00740.trc` and store the first 10 SQL statements in an output file called `trace.txt`.
- Create a file called `sql.txt` that would contain the first ten SQL statements in the original trace file.

The following demonstrates the use of TKPROF with INSERT and SORT parameters on a Unix system:

```
$ tkprof ora_1702.trc trace.txt insert=trace.sql sort=fchrow
```

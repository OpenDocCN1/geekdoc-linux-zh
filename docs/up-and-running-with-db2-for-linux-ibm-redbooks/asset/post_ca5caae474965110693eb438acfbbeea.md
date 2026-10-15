
## Specify input and output files.

Most load operations will have at least one input or output file. Other minor file specifications can be found on the 'Options' page.

### Input file format

- Delimited Text (DEL)
- DEL Options

### Input file location

- Server (UDLNX08)
- Remote host
- Full path and filename of user exit program on database server:
- Full path and filename of input files: /db2home/db2inst1/nso/emp.del
- Full path and filename to store progress messages: /db2home/db2inst1/nso/guioload.msg

Figure 5-23 Specify input and output files

## 5. Specify which partitions participate in the load (Figure 5-24).

You can use the default choice of "Load data into all table partitions" in the window, if you just want to load data into all the partitions where the table resides. Under some conditions, you may want to load data for a specific partition or partitions; then you can choose "Load data into selected table partitions". In addition, in the "Partitioning partitions" group within the window, you also can specify which partitions will be used to do the data partitioning work; in general, you can just leave it and "Let DB2 decide which partitions participate".

![](img/d95c931f4f3da4a6bd0ee55148fefad7_217_0.png)

Figure 5-24 Specify which partitions participate in the load

## 6. Define the input columns and their mapping to the output columns (Figure 5-25).

You can simply use the default mapping if you think this is appropriate for your situation, or you can make some modifications in the window, if needed. For example, if large object (LOB) is involved in your load, then you may need to specify LOB related options in the window.

Figure 5-25 Define column related properties for load

## 7. Specify performance and statistics collection options (Figure 5-26).

You can specify options which will impact load performance, for example, you can specify how the load utility will update the existing indexes, rebuild all indexes, or rebuild indexes incrementally. A full index rebuild is faster than an incremental rebuild. But if the index is very large, it will be quicker to do an incremental rebuild. In addition, options for statistics collection are also provided in this window. If you don't want to make any modifications, leaving the defaults is alright.

![](img/d95c931f4f3da4a6bd0ee55148fefad7_218_0.png)

### Options affecting load performance

- Perform only minimal checking of input data
- Let the load utility update existing indexes
  - Update existing indexes incrementally
  - Rebuild all indexes
  - Let the utility decide between incremental and complete rebuild
- Specify a particular temporary tablespace for index creation TEMPSPACE1

### Options affecting other applications

- Defer placement of dependent tables into check pending until load completion.
- Start load immediately, forcing other applications if necessary

### Options affecting performance after load

- Percentage of each data page left free <default>
- Percentage of each index page left free <default>
- Percentage of the table size appended as free space <default>

### Statistics for the table

Figure 5-26 Specify performance and statistics collection options

## 8. Specify failure options and recovery strategy.

Options regarding failure handling and recovery strategy are covered in this window. For example, if you want the whole load operation to halt when any error occurs during the load operation, then you can check both boxes for error isolation, Load job fails... and Load will rollback in the Crash recovery group in the window, as shown in Figure 5-27.

### Select failure options and recovery strategy.

Use this page to specify failure and recovery options for a load failure. You can also specify forward recovery options if the database that contains the target table is configured for forward recovery.

- 1. Operation
- 2. Type
- 3. Files
- 4. Partitions
- 5. Columns
- 6. Perform...
- 7. Recovery
- 8. Options
- 9. Schedule
- 10. Summary

### Crash recovery

Establish consistency points and generate row count messages during data load

Number of rows between consistency points:

Load job fails if any partition encounters errors in the setup phase

Load will rollback immediately on all partitions if any fail after setup is complete

### Forward recovery

The following options will be valid only if the database is configured for forward recovery at the time the load task runs. If you choose to perform an unrecoverable load, a subsequent roll forward through this load will succeed but render the table unusable.

- Perform a recoverable load
- Do not make a copy of the input data. This will put the tablespace into backup pending.
- Save a copy of the input data. The table will be usable after load completion.

Copy target: Directory

Directory names:

Figure 5-27 Specify failure options and recovery strategy

## 9. Set advanced options.

Here you can specify additional options associated with the load operation which are not covered by the preceding windows, and you can get hints by clicking on the option listed in the window (Figure 5-28).

**NOTE**
*The execution plan is the path that Oracle uses to process the SQL statement. The explain plan is the external representation of this execution plan. For our purposes in this chapter, the terms can be used interchangeably.*

# Viewing the Execution Plan

There are many ways to view the SQL execution plan. This section will cover a few of these methods using SQL\*Plus. There are many third-party tools available, such as RapidSQL from Embarcadero Technologies, TOAD from Quest Software, and SQL Station from Computer Associates, that also aid in the tuning of SQL statements.

**NOTE**
*I wrote an interface that produces the explain plans using the extra predicates discussed in the previous section. This tool I call JSTuner and is downloadable from www.DanHotka.com. I will use this tool in many of the illustrations in this chapter.*

Using the autotrace feature of SQL\*Plus is probably the easiest way to get an explain plan for a given SQL statement. Figure 16-1 shows the autotrace feature and the resulting execution plan.

Sometimes you are trying to tune a long-running SQL statement and all you want is to see the execution plan. This method, again using SQL\*Plus, populates the PLAN\_TABLE, and then you can use SQL to see your execution plan steps. There are many SQL scripts available to view the contents of the PLAN\_TABLE; one such script is included in Figure 16-2. This method uses the STATEMENT\_ID. You will also have to delete the rows from the PLAN\_TABLE after viewing the execution plan. Autotrace performed this cleanup for you but this is a more manual method.

Notice the very first line in Figure 16-2. This line causes the PLAN\_TABLE to be populated with the execution plan for the SQL that follows it. The SHOW\_PLAN.sql script takes the STATEMENT\_ID as input and formats the execution plan. Listing 16-2 illustrates the SHOW\_PLAN.sql script.

**TIP**
*This script and the explain plan syntax could easily be incorporated into the same script for ease of use.*
*The SHOW\_PLAN.sql script can be downloaded from www.DanHotka.com.*
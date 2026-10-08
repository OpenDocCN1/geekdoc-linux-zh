Oracle provides a function for calculating the elapsed time for duration events. Reports can also be generated on the frequency of different types of events, such as connection events. Statistics available include the minimum, maximum, and average times spent doing different events. The Oracle Trace APIs are listed with a brief description in Table 8-9.

# Oracle VS Tables

Oracle provides a set of virtual tables that can be used to access memory structures within the shared global area. Many of these tables contain database performance information that is continuously updated. Table 8-10 lists and describes the contents of some of the more interesting VS tables.

# Table 8-9    Oracle Trace APIs

| Name | Function |
| --- | --- |
| epc_init | Initial trace call; used to register facility with Oracle Trace |
| epc_add_reg_id | Adds a registration ID for a facility |
| epc_remove_reg_id | Removes a registration ID for a facility |
| epc_start_event | Records start of duration event |
| epc_end_event | Records end of duration event |
| epc_event | Records asynchronous event |
| epc_collect | Starts a collection from within a facility |
| epc_cancel | Stops a collection started by epc_collect |
| epc_bind | Binds a process to a collection that is already active |
| epc_flush | Writes collection data buffers to disk |
| epc_context | Stores collection data on per-thread basis |
| epc_delete_context | Indicates the end of thread |
| epc_set_cf_items | Sends cross-facility items to another process |
| epc_cf_value | Assigns values to cross-facility items |
| epc_get_cf_items | Obtains cross-facility items from another process |

# Table 8-10    Oracle VS Tables

| VS Table | Contains |
| --- | --- |
| V$DATABASE | Database information from the control file |
| V$FILESTAT | File read/write statistics |
| V$INSTANCE | Status information for the current instance |
| V$LIBRARYCACHE | Library cache performance information |
| V$LICENSE | Information on license limits |
| V$PROCESS | Process information |
| V$ROWCACHE | Data dictionary performance information |
| V$SESSION | Session information |
| V$SESSTAT | Information on the memory usage for each current session |
| V$SGA | Summary information on system global area |
| V$SGASTAT | Detailed information on system global area |
| V$SYSSTAT | Current system-wide value for each variable in V$SESSTAT |
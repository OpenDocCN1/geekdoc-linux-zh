the FLASHBACK DATABASE command within RMAN. There are several methods of specifying the flashback point, as shown in the following table:

| command | description |
| :--- | :--- |
| FLASHBACK DATABASE TO SCN scn# | Flash back to a specific SCN. |
| FLASHBACK DATABASE TO SEQUENCE sequence# | Flash back to a specific log sequence. |
| FLASHBACK DATABASE TO TIME (SYSDATE-1/24); | Flash back to a specific point in the past. |
| FLASHBACK DATABASE TO TIME timestamp('2004-05-16 14:00:00'); | Flash back to a specific point in time. |

As with the other flashback features, this can be very powerful, or very dangerous. The flashback database feature will revert your database to a previous point in time, thus overwriting any changes that have been made since then. This can be very useful, or it can cause more problems.

# ## Developing a Recovery Strategy

It is very important that you plan your recovery process and recovery strategy so you're prepared should a system failure occur. Several scenarios must be planned for, depending on the type of failure. The types of failure that require recovery are

+   - Instance failure
+   - Media failure
+   - Operator error

Each is different and each calls for a different recovery strategy.

# ## Planning for Instance Recovery

Instance failure typically calls for no operator intervention, as described earlier. The main planning that should be done is in the area of the parallel recovery option. By evaluating your system, you should determine the degree of parallelism for the recovery process. This is set as the Oracle initialization parameter RECOVERY_PARALLELISM.

The number of disk drives and CPUS typically determines the degree of parallelism in your system. My rule of thumb is one process (thread) per every two disk drives, up to twenty. By setting this too high, you may cause additional overhead.
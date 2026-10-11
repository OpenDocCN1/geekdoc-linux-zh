Stats for DB. Sample output displaying this section of a STATSPACK report is shown in Figure 4.9.

# FIGURE 4.9 STATSPACK output showing Data Dictionary Cache hit ratio

```
Dictionary Cache Stats for DB: PROD  Instance: prod  Snap: 1 -2
--"Pct Misses"  should be very low (< 3% in most cases)
--"Cache usage"  is the number of cache entries being used
--"Pct SGA"  is the ratio of usage to allocated size for that cache

     Requests      Get      Pct    Scan   Pct     Mod    Final Pct
     ")           Miss     Reqs   Miss    Reqs   Usage  SGA
Cache -----------------------------------------------------------------
dc_free_extents       4    0.0      0        0     30    98    88
dc_object_ids        39    0.0      0        0    403    99     99
dc_objects            83    1.2      0        0    838    99     99
dc_profiles           2    0.0      0        0      2    11     11
dc_rollback_segments  80    0.0      0        0      1     91     91
dc_segments          56    0.0      0        0    181    94     94
dc_tablespace_s      6    0.0      0        0      9     60     60
dc_user_grants      19    0.0      0        0      19    51     51
dc_usernames        28    3.6      0        0      17    81     81
dc_users            43    0.0      0        0      19    86     86
-------------------------------------------------------------
```

Like the output for the Library Cache, the STATSPACK output for Data Dictionary Cache performance is also expressed in terms of a miss ratio. Figure 4.9 shows that the value for *Pct Miss* for each of the components of the Data Dictionary Cache (e.g., *dc_free_extents*, *dc_object_ids*) ranges from a zero to 3.6 percent miss ratio. Conversely, this means that the Data Dictionary Cache hit ratio was between 96.4 and 100 percent during the monitoring period.

![](bbox=[0.13, 0.56, 0.26, 0.62])

Oracle recommends that consideration be given to tuning the Shared Pool if the STATSPACK output shows that the hit ratio for any single component of the Data Dictionary Cache (e.g., *dc_free_extents*, *dc_object_ids*) is lower than 98 percent for most components.

# Using *REPORT.TXT* to Monitor the Data Dictionary Cache

Data Dictionary information is also contained in the *REPORT.TXT* output produced by UTLBSTAT.SQL and UTLSTAT.SQL. Like STATSPACK, *REPORT.TXT* displays the Data Dictionary Cache statistics separately for each component that is cached. Therefore, you will need to add the *GET_REQS* and *GET_MISS* columns yourself before calculating the overall hit ratio. Figure 4.10 shows the relevant section of a *REPORT.TXT* file.
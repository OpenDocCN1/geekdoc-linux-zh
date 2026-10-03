# Linux Hack

Ajay Kumar Tiwari

Note: /etc/cron.d/sysstat files comes with the sysstat package that includes some default value for the sa1 and sa2, which you can change accordingly.

# Display CPU Statistics using Sar Command

```
# sar -u
```

```
Linux 2.6.9-42.ELsmp (dev-db)
12:00:01 AM CPU %user %nice
12:05:01 AM all 3.700.00
12:10:01 AM all 4.590.00
12:15:01 AM all 3.900.00
12:20:01 AM all 4.060.00
12:25:01 AM all 3.890.00
12:30:01 AM all 3.890.00
Skipped..
Average: all
4.56
0.00
1.00
0.15
94.29
01/01/2009
%system%iowait
0.850.00
1.190.06
0.950.04
1.000.01
0.870.00
0.870.00
%idle
95.45
94.16
95.11
94.93
95.23
95.23
```
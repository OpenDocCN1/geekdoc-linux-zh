# 75

904323600.a Sat Aug 29 01:00:00 1998
904460400.a Sun Aug 30 15:00:00 1998

The following example shows the output from the atq command when executed as superuser.

```
castle% su
Password:
castle# atq
Rank  Execution Date      Owner   Job       Queue   Job Name
1st   Aug 28, 1998 18:00  root    90291200.a  a       tryit
2nd   Aug 28, 1998 17:00  winsor 90294800.a  a       tryit
3rd   Aug 28, 1998 18:00  root    90298400.a  a       tryit
4th   Aug 28, 1998 19:00  ray     904302000.a  a       tryit
5th   Aug 28, 1998 21:00  ray     904309200.a  a       tryit
6th   Aug 29, 1998 01:00  winsor 904323600.a  a       tryit
7th   Aug 29, 1998 07:30  winsor 904347000.a  a       stdin
8th   Aug 30, 1998 15:00  winsor 904460400.a  a       tryit
```

The following example shows the same example sorted by time.

```
castle# atq -c
Rank  Execution Date      Owner   Job       Queue   Job Name
1st   Aug 29, 1998 07:30  winsor 904347000.a  a       stdin
2nd   Aug 28, 1998 17:00  winsor 904948000.a  a       tryit
3rd   Aug 29, 1998 01:00  winsor 904323600.a  a       tryit
4th   Aug 30, 1998 15:00  winsor 904460400.a  a       tryit
5th   Aug 28, 1998 16:00  root    90291200.a  a       tryit
6th   Aug 28, 1998 18:00  root    902984000.a  a       tryit
7th   Aug 28, 1998 19:00  ray     904302000.a  a       tryit
8th   Aug 28, 1998 21:00  ray     904309200.a  a       tryit
```

The following example shows the value returned by the atq -n command. This option lists the number of items in the queue.

```
castle# atq -n
castle#nnThe following example shows the jobs queued only by user ray.
castle# atq ray
Rank  Execution Date      Owner   Job       Queue   Job Name
1st   Aug 28, 1998 19:00  ray     904302000.a  a       tryit
2nd   Aug 28, 1998 21:00  ray     904309200.a  a       tryit
castle#
```

Files

```
/var/spool/cron/atjobs
Spool area for jobs.
```
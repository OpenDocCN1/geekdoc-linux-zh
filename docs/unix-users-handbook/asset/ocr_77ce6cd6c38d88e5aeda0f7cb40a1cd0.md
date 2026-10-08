You could use the **while** loop to execute commands for some number of iterations. The **while** loop is in the following format:

```
while (expression)
	command(s)
end
```

The following program called **netcheck** runs **netstat** at the desired interval, and prints out the heading once and the status of le0 nine times:

![](bbox=[0.85, 0.26, 0.95, 0.35])

```
#!/bin/csh
# program to run netstat at every specified interval
# Usage: netcheck interval

set limit=9		# set limit on number times
			# to run netstat

echo " "
netstat -i | grep Name	# print netstat line with headings
set count=0
while ($count<$limit)	# if limit hasn't reached
			# limit run netstat
		netstat -i | grep le0
		sleep $1		# sleep for interval
				# specified on command line
		@ count++		# increment limit
end
echo "count has reached $limit, run netcheck again to see le0 status"
```

Here is an example run of the **netcheck** program:

```
martyp $ netcheck 3
Name Mtu Net/Dest Address Ipkts Ierrs Opks Oerrs Collis Queue
le0 1500 sunsys sunsys 314374989 0 17252200 52135 7580906
le0 1500 sunsys sunsys 314375038 0 17252203 52135 7580906
le0 1500 sunsys sunsys 314375114 0 17252206 52135 7580906
le0 1500 sunsys sunsys 314375185 0 17252209 52135 7580906
```
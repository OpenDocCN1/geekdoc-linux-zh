```
$file = $ARGV[0] || '/var/log/uptime.log'; ## Path to log file
$uptime = `~/usr/bin/uptime`;
## Store output from uptime

###++
### Parse the output of the uptime command and store the numbers of
### users and the three system load averages into: $users, $load1,
### $load2 and $load3.
###--

$uptime =~ /\\(\\d+\\) +user.+?(\\d.+?), +(..?), +(.+?)/;
$users = $1;
$load1 = $2;
$load2 = $3;
$load3 = $4;

###++
### We can also write the above like this:
###
###
$uptime =~ /\\(\\d+\\) +user.+?(\\d.+?), +(.+?), +(.+)/;
### ($users, $load1, $load2, $load3) = ($1, $2, $3, $4);
###
### or even:
###
###
($users, $load1, $load2, $load3)
### = $uptime =~ /\\(\\d+\\) +user.+?(\\d.+?), +(.+?), +(.+?)/;
###--

###++
### Store the data in a log file; open modes:
###
### >> = append, > = write, < (or nothing) = read
###--

open (FILE, ">>$file") || die "Cannot append uptime data to $file: $!\n";
print FILE join (':', time, $users, $load1, $load2, $load3), "\n";
close (FILE);

exit (0);
```

One note, before we start discussing the code. Our application accepts a command line argument and uses its value to determine where to archive the load average data. This provides us with the flexibility to archive the data to different files without modifying the code at all. If you were curious as to the significance of the `/home/nutt/uptime.log` file in the crontab entry above, now you know; it refers to the log file.
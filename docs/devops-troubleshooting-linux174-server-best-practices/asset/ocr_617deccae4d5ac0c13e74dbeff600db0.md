or a particular hour in that day:

```
```
$ egrep '^10.1.2.3.:04\\/Jul\\/2012:12' /var/log/apache2/access.log
```
```

Using perl, you can pull even more interesting statistics from Apache logs. For instance, you may have noticed extra load on your web server today, and you'd like to know if any of that load is coming from a particular host. This perl one-liner acts like the earlier demonstrated egrep command in that it pulls out the IP and a specific date from the logs; but it goes a step further and keeps a tally of each IP it finds. Ultimately it outputs the complete list of IPs and their tally:

```
```
$ perl -e 'while(<>){ if(m\\/(\\d+.\\d+.\\d+.\\d+):?04\\/Jul\\/2012){ ${$_}++; }}
  ->foreach( keys %v ){ print "$v{$_}{$_}\n"; }' /var/log/apache2/access.log | sort -n
...
213   27.171.3.72
217   64.2.73.9
2040  10.2.1.3
```
```

Here you can see that the same internal IP address (10.2.1.3) has created about ten times the number of requests of any other IP in the logs. If you were investigating a high load problem and saw this, you would pull all of the log entries coming from 10.2.1.3 and see what that internal server is doing.

In case you find that one-liner hard to parse, here's the same command in a regular file:

```
```
#!/usr/bin/perl

while(<>){
    if(m\\/(\\d+.\\d+.\\d+.\\d+):?04\\/Jul\\/2012){
        ${$_}++;
    }
}

foreach( keys %v){
    print "$v{$_}{$_}\n";
}
```
```
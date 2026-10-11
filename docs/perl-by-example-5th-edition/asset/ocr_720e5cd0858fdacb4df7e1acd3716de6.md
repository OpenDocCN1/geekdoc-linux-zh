# The localtime Function.

The localtime function converts the UTC to a nine-element array with the local time zone.

# FORMAT

```
localtime(EXPR);  
localtime EXPR;  
($sec, $min, $hour, $mday, $mon, $year, $wday, $yday,  
  $isdst)=localtime(time);
```

# EXAMPLE 16.46

(At the Command Line)

```
1   $ perl -e "print scalar (localtime);"  
       Wed Jun 25 15:26:16 2014
```

(In Script)

```
2   $localtime=localtime;  
    print $localtime;
```

# EXPLANATION

+   1. If the *localtime* function is used in scalar context, its return value is output similar to the UNIX/VMS/32 *date* command. The *scalar* function forces scalar context.
+   2. The return value of *localtime* is assigned to a scalar.

# EXAMPLE 16.47

(The Script)

```
use warnings;  
1 my ($sec, $min, $hour, $mday, $mon, $year, $wday, $yday, $isdst)=  
    localtime(time);  
2 my  %weekday=(  
    "0"=>"Sunday",  
    "1"=>"Monday",  
    "2"=>"Tuesday",  
    "3"=>"Wednesday",  
    "4"=>"Thursday",  
    "5"=>"Friday",  
    "6"=>"Saturday",  
  );  
  if ( $hour > 12 ) {  
    print "The hour is ", $hour - 12 , " o'".clock.\n";  
  }  
  else {  
    print "The hour is $hour o'".clock.\n";  
  }  
4 print qq/Today is $weekday{\"$wday\"}.\n/;  # day starts at zero  
5 print "It is ", $mon + 1, ", "/$mday/", ", 1900+$year,"\n";  
6 print "The isdst is $isdst.\n";
```
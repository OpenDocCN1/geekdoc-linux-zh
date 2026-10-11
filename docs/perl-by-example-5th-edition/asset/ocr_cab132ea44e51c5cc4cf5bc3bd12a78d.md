# 10.3 Passing Arguments

# EXAMPLE 10.39

```
(The Script)
```
#!/usr/bin/env perl
use warnings;
1 if ( scalar @ARGV < 1 ) { die "Usage: $0 <argument>";
2 open(my $pw, "<", "/etc/passwd") || die "Can't open /etc/passwd: $!";
3 my $username=$shift; # Same as shift @ARGV
4 while( my $pline = <$pw>){
5 unles$ /$pline =~ /$username/){ print "$username is not
a user here.\n"; next;}
}
6 close $pw;
7 open(LOGGEDON, "who |" ) || die "Can't execute who $1" ;
8 while( $logged = <LOGGEDON> ){
if ( $logged =~ /$username/){ $logged_on = 1; last;}
}
9 close LOGGEDON;
die "$username is not logged on.\n" if ! $logged_on;
print "Username is logged on and running these processes.\n";
10 open( PROC, "ps -aux |" ) || die "Can't execute ps: $1";
while(my $line=<PROC>){
print "$line" if $line =~ /$username;//
}
11 close PROC;
print "\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\n";
print "So long.\n";
```

(Output)
```
S checkcon
1 Usage: checkcon <argument> at checkcon line 6.
S checkcon joe
5 Joe is not a user here.
S checkcon ellie
8 ellie is logged on and running these processes:
ellie 3925 6.4 4.5 212 464 p5 R 12:18 0:00 ps -aux
ellie 1383 0.8 8.4 360 876 p4 S Dec 26 11:34 /usr/local/QW3/bin/xvview
ellie 173 0.8 13.4 1932 1392 co S Dec 20 3:89:19 /usr/local/QW3/bin/xnews
ellie 164 0.0 0.0 100 0 c0 IW Dec 20 0:00 -c
« some of the output was cut to save space »
ellie 3822 0.0 0.0 0 0 p5 2 12/18 0:00 sh -c 'ps -aux | grep '^'
ellie 3823 0.0 1.1 28 112 p5 3 12/18 0:00 /bin/perl checkcon ellie
ellie 3821 0.0 5.6 144 580 p5 S 12/18 0:00 grep ellie
ellie 3824 0.0 1.8 32 192 p5 S 12/18 0:00 grep '^ellie
ellie 3815 0.0 1.9 24 196 p4 S 12:18 0:00 script checkcon.tac
```

**
```

337
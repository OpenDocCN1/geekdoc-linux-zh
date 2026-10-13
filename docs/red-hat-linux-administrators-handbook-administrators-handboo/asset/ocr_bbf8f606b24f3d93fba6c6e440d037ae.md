```
```perl
SBANG

foreach $signal (keys %SIG){
print <<SIG;
\$$SIG{$signal} = sub { print "Caught a $signal signal.\n"; };
SIG

}

print <<MAIN;

print "Hello, my PID is \$\$.\n";
print "Use kill -signal \$\$ command to experiment on me.\n";

# Set a 10 sec. alarm event.
alarm(10);

# Loop forever.
while(1){
sleep(1); # Sleep for a second.
}

MAIN
```
```

This relatively small Perl script generates another Perl script. Run the script as follows:

```
gen_signal_demo.pl > signal_demo.pl
```

The generated script will have signal handlers for all the signals available on your system. The generated script defines signal handlers using the following construct:

```
$SIG{shortened signal name} = sub { # handler code };
```
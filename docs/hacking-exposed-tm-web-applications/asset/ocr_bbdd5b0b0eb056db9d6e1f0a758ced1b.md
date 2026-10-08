```
print "possible SQL injection:\n$uri\n\n";
}
# modify this regex to add more matches for input validation errors
if ($Shtml =~ /(VBScript)|(\?>)|(invalid)/) {
    print "possible input validation:\n$uri\n\n";
}
return;
}

sub halo4 {
    my $uri = shift(@);
    my $param, %sqltest, $res;
    my $args, $page, $res;

    ($page, $args) = split(/\?, $uri);
    if ($args) {
        @temp = split(/@/, $args);
        foreach (@temp) {
            m/(.*)=(.*);
            \$Sparam($1) = $2;
        }
        # place SQL injection test in front of value
        foreach $key (keys $param) {
            $Temp = "$page?$args";
            $Temp = s/\key=\$param(\$key)/\$sql_test\$param(\$key)/;
            LW::http_do_request(\$hin, \sqltest, {'uri'=>$temp);
            print "$hin($whisker)->->'$uri\n" if ($DEBUG);
            parse_output(\$hin, \sqltest);
        }
        # other tests that will be added...
        # place SQL injection at end of value
        # replace value with SQL injection
        # support multiple SQL tests (e.g. @@servername, xp_cmdshell, ...)
        # check out http://www.webhackingexposed.com/ for updates
    }
    return 1;
}

# injected with a poison...
```
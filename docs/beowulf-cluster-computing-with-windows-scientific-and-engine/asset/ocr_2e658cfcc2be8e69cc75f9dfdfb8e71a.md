```
```text
{
    print "Successfully removed.\n";
}
else
{
    print "Failed to remove service: " . GetError() . "\n";
}
print "finished.\n";
} # sub Remove

sub GetError
{
    return( Win32::FormatMessage( Win32::Daemon::GetLastError() ));
}

sub Log
{
    ($sec,$min,$hour,$mday,$mon,$year,$yday,$syday,$isdst) = localtime(time);
    $time = sprintf("%02d%02d%02d%02d%02d",$mon+1,$mday,$year+1900,$hour,$min);
    open(LOG,"+>>$LogDir\\Model_log" );
    print LOG "$time&$_[0]\n";
    close(LOG);
}
```
```

# 7.1.3  Login Nodes

Login nodes are a mechanism to provide remote users with a consistent interface and tools to your cluster. Typically, login nodes have compilers, debuggers, programming environments such as Interix or Cygwin, and scheduler interface tools. Login nodes usually are accessible via telnet or the Windows Terminal Server (with or without Citrix Metaframe, depending on whether you have clients accessing the cluster from a non-Windows platform). In many environments login nodes are not necessary, and simply installing scheduler interface commands on the users’ workstations in the same Windows domain is sufficient.

# 7.1.4  Compute Nodes

Chapter 3 of this book provides a complete description of compute node hardware options and their effect on performance. Typically, compute nodes have relatively little software installed on them. The usual software includes runtime libraries, message-passing software, and applications such as Matlab, Mathematica, SAS, and scripting languages, as needed.
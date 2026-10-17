
```perl
sub kicknamed
open PID, "/etc/named.pid";
$pid = <PID>;
kill $SIGUP, $pid;
# kicknamed

# Delete all hosts from batchparms
sub delbatch
{
    local( $sysnam, $backup, $dummy );
    local( $uid, $gid, $mode );

    # Backup up older versions
    #backupfile( $swsbat, );
    $backup = $swsbat;
    open ORIGINAL, "$backup" || warn "Cannot open $swsbat, $!\n" && link $backup, $swsbat && return;
    open NEW, ">$swsbat" || warn "Cannot create $swsbat, $!\n" && link $backup, $swsbat && return;

    while( <ORIGINAL> ) {
        if( /^$sysnam/ ) {
            print NEW;
            next;
        }
        ($sysnam, $dummy) = split /:/;
        print NEW if (!exists $delete{$sysnam});
    }
    close ORIGINAL;
    close NEW;
    # Set ownership and permissions
    &setperm( $backup, $swsbat );
} # delbatch

# Add all hosts to batchparms
sub addbatch
{
    local( $sysnam, $backup, $dummy );
    local( $uid, $gid, $mode );

    # Backup up older versions
    #backupfile( $swsbat, );
    $backup = $swsbat;
    open ORIGINAL, "$backup" || warn "Cannot open $swsbat, $!\n" && link $backup, $swsbat && return;
    open NEW, ">$swsbat" || warn "Cannot create $swsbat, $!\n" && link $backup, $swsbat && return;

    while( <ORIGINAL> ) {print NEW;}
    close ORIGINAL;

    foreach $sysnam (keys %add) {
        print NEW <<EOF
$sysnam u 100000 20 batcher
| compun | v1uxx
EOF
    }
    close NEW;
    # Set ownership and permissions
    &setperm( $backup, $swsbat );
} # addbatch
```

如 `Listing 16.1` 所示，添加主机是在函数 `addhost` 中完成的。它会先扫描活动的 `sys` 文件，查看主机是否已存在。如果存在，它会向 `root` 发送警告邮件并退出。如果不存在，它会备份 `sys` 文件，打开模板，并将主机添加到 `sys` 文件的底部。`sys` 文件还会用新系统的名称替换 `%%%` 标记。

### Listing 16.1 (continued)

```perl
# Delete all hosts from sendmail.uunames
sub delmail
{
  local( $sysnam, $backup, $dummy );
  local( $uid, $gid, $mode );

# Back up older versions
&backupfile( $mailnam );
$backup = $mailnam . ".o";
open ORIGINAL, "$backup" || warn "Cannot open $mailnam, $!\n" && link $backup,
$mailnam && return;
open NEW, ">$mailnam" || warn "Cannot create $mailnam, $!\n" && link $backup,
$mailnam && return;

while( <ORIGINAL> ) {
  if( /^#/ || /^\s*$/ ) {
    print NEW;
  }
  next;
}
chomp;
print NEW if (exists $delete{$_});

close ORIGINAL;
close NEW;
# Set ownership and permissions
&setperm( $backup, $mailnam );
} # delmail

# Add all hosts to sendmail.uunames
sub addmail
{
  local( $sysnam, $backup, $dummy );
  local( $uid, $gid, $mode );

# Back up older versions
&backupfile( $mailnam );
$backup = $mailnam . ".o";
open ORIGINAL, "$backup" || warn "Cannot open $mailnam, $!\n" && link $backup,
$mailnam && return;
open NEW, ">$mailnam" || warn "Cannot create $mailnam, $!\n" && link $backup,
$mailnam && return;

while( <ORIGINAL> ) {print NEW $_;}
close ORIGINAL;

foreach $sysnam (keys %add) {
  print NEW "$sysnam\n";
}
close NEW;
# Set ownership and permissions
&setperm( $backup, $mailnam );
} # addmail
```

### Listing 16.1 (continued)

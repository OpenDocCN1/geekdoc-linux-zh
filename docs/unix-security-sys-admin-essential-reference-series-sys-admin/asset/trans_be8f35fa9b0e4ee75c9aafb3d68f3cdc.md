

## 清单 16.1（续）

```
# Add all hosts to newsconfig
sub addnews
{
    local( $sysnam, $backup, $dummy );
    local( $uid, $gid, $mode );

    # Back up older versions
    $backupfile = $newsconf;
    $backup = $newsconf . ".o";
    open ORIGINAL, "$backup" || warn "Cannot open $newsconf, $!\n" && link $backup, $newsconf && return;
    open NEW, ">$newsconf" || warn "Cannot create $newsconf, $!\n" && link $backup, $newsconf && return;

    while( <ORIGINAL> ) {print NEW;}
    close ORIGINAL;

    foreach $sysnam (keys %add) {
        print NEW <<EOF
$sysnam:news.misc.comp.eunet,hacktic.nl,ninet,reseau.to,$sysnam,all),general:
    f:$sysnam/togo
EOF
    }
    close NEW;
    # Set ownership and permissions
    &setperm( $backup, $newsconf );
}
# addnews

# Add all hosts to ntpnconfig
sub addntp
{
    local( $sysnam, $backup, $dummy );
    local( $uid, $gid, $mode );

    # Back up older versions
    $backupfile = $newsntp;
    $backup = $newsntp . ".o";
    open ORIGINAL, "$backup" || warn "Cannot open $newsntp, $!\n" && link $backup, $newsntp && return;
    open NEW, ">$newsntp" || warn "Cannot create $newsntp, $!\n" && link $backup, $newsntp && return;

    while( <ORIGINAL> ) {print NEW;}
    close ORIGINAL;

    foreach $sysnam (keys %add) {
        print NEW <<EOF
$sysnam.reseau.nl both post
EOF
    }
    close NEW;
    # Set ownership and permissions
    &setperm( $backup, $newsntp );
}
# addntp
```

远程系统允许发送和接收邮件和新闻，同时它还可以通过 UUCP 公共存储 /usr/spool/uucppublic 上传或下载文件。远程系统永远不会被呼叫（参见时间配置行）。最后，远程系统用于拨入的用户名称为 uuxqt。

## 清单 16.1（续）

```
# Add all hosts to named
sub addnamed
{
    local( $sysnam, $backup, $dummy );
    local( $uid, $gid, $mode );
    # First the forward mapping. Back up older versions
    &backupfile( $namedfwd );
    $backup = $namedfwd . ".o";
    open ORIGINAL, "$backup" || warn "Cannot open $namedfwd, $!\n" && link $backup, $namedfwd && return;
    open NEW, ">$namedfwd" || warn "Cannot create $namedfwd, $!\n" && link $backup, $namedfwd && return;
    while( <ORIGINAL> ) { print NEW;
    }
    close ORIGINAL;
    foreach $sysnam (keys %add) {
        print NEW <<EOF
$sysnam  IN  A  $add{$sysnam}
EOF
    }
    close NEW;
    # Set ownership and permissions
    &setperm( $backup, $namedfwd );
    # Secondly the reverse mapping. Back up older versions
    &backupfile( $namedrev );
    $backup = $namedrev . ".o";
    open ORIGINAL, "$backup" || warn "Cannot open $namedrev, $!\n" && link $backup, $namedrev && return;
    open NEW, ">$namedrev" || warn "Cannot create $namedrev, $!\n" && link $backup, $namedrev && return;
    while( <ORIGINAL> ) { print NEW;
    }
    close ORIGINAL;
    foreach $sysnam (keys %add) {
        local( $hostnum, $fullname );
        $fullname = $sysnam . ".reseau.nl.";
        $hostnum = $add{$sysnam};
        $hostnum =~ s/\./(10-9)+/\/1/;
        print NEW <<EOF
$hostnum PTR  $fullname
EOF
    }
    close NEW;
    # Set ownership and permissions
    &setperm( $backup, $namedrev );
}
# addnamed
```

## 清单 16.1（续）

```
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


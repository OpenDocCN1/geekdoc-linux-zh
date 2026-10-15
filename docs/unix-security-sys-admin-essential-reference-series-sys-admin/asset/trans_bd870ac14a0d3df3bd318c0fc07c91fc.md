
# 清单 16.1（续）

```
# Check system for pending batches
sub uucpbatch
{
    local( $sysnam ) = @_; 

    open UUSTAT, "uustat -s $sysnam" || warn "Cannot start $uustat, $!\n" && return 1;
    while( <UUSTAT> ) {
        close UUSTAT;
        return 1;
    }
    close UUSTAT;
    return 0;
}
# uucpbatch

# Delete one UUCP host from uucp configuration
sub deluucp
{
    local( $deleteme ) = @_; 
    local( $sysnam, $backup, $dummy );
    local( $uid, $gid, $mode );

    # Back up older versions
    &backupfile( $uuconf );
    $backup = $uuconf . ".o";

    open ORIGINAL, "$backup" || warn "Cannot open $uuconf, $!\n" && link $backup, $uuconf && return;
    open NEW, ">$uuconf" || warn "Cannot create $uuconf, $!\n" && link $backup, $uuconf && return;

    while( <ORIGINAL> ) {
        if( /^\*START .*\$/ ) {
            chop;
            $sysnam = $.;
            $sysnam =~ s/^\*START //;
            if( $sysnam ne $deleteme ) {
                while( <ORIGINAL> ) {
                    last if (/^\*END .*\$/);
                }
            }
            else {
                print NEW;
                while( <ORIGINAL> ) {
                    print NEW;
                    last if ( /^\*END .*\$/);
                }
            }
        }
        else { print NEW; }
    }
    close ORIGINAL;
    close NEW;
    # Set ownership and permissions
    &setperm( $backup, $uuconf );
    &deluser( $deleteme );
}
# deluucp
```

## 将主机添加到 UUCP 配置

将主机添加到 UUCP 网络设置需要几个步骤。为简单起见，仅支持拨号 UUCP 连接。外出人员经常在路上，因此无法通过固定的电话号码联系到他们。第一步是将机器添加到已知 UUCP 主机列表中。这些是受信任的主机，允许拨入并传输数据。这些机器的列表保存在 Taylor 配置目录中名为 sys 的配置文件中。该配置目录通常位于 UUCP 用户主目录下名为 conf 的子目录中。这个 conf 文件相当于 HDB 中的 Systems 文件。

# 清单 16.1（续）

```
# Add UUCP host to uucp configuration
sub adduucp
{
    local( $sysnam, $backup, $dummy );
    local( $uid, $gid, $mode );
    # Back up older versions
    $backupfile = "$uucconf/";
    $backup = $uucconf . ".o";
    open ORIGINAL, "$backup" || warn "Cannot open $uucconf, $!\n" && link $backup, $uucconf && return;
    open NEW, ">$uucconf" || warn "Cannot create $uucconf, $!\n" && link $backup, $uucconf && return;
    while( <ORIGINAL > ) { print NEW; }
    close ORIGINAL;
    foreach $sysnam (keys %add) {
        print NEW <<EOF
#START $sysnam
system $sysnam
time Never
baud 38400
port Direct
phone *
called-login uucp$sysnam
send-request yes
receive-request yes
called-transfer yes
remote-send /usr/spool/uucppublic /usr/spool/news
local-receive /usr/spool/uucppublic /usr/spool/news
remote-receive /bin/rmail /usr/local/lib/news/bin/rnews
myname lrnate
#END $sysnam
EOF
    }
    $adduser( $sysnam );
    close NEW;
    # Set ownership and permissions
    &setperm( $backup, $uucconf );
}
# adduucp
```

# 清单 16.1（续）

```
# Notify root of successful action for UUCP
sub notifyuucp
{
    local( $action, @hostlist ) = @_;

    open MAILTO, "|mail root" || warn "Cannot start mail program, $!\n" && return;
    print MAILTO <<EOF
Subject: UUCP hosts $action.

The following UUCP hosts have been $action :

@hostlist
EOF
    ; # notifyuucp

# Notify root of successful action for LAN
sub notifylan
{
    local( $action, @hostlist ) = @_;

    open MAILTO, "|mail root" || warn "Cannot start mail program, $!\n" && return;
    print MAILTO <<EOF
Subject: LAN hosts $action.

The following LAN hosts have been $action :

@hostlist
EOF
    ; # notifylan

# Delete host from news config for LAN
sub delnews lan
{
    # First the nntp access
    &delnntp( );
    # Secondly the sys file
    &delnews( );
} # delnews lan

# Add host to news config for LAN
sub addnews lan
{
    # First the nntp access
    &addnntp( );
    # Secondly the sys file
    &addnews( );
} # addnews lan

# Delete host from news and news config for UUCP
sub deluucp mailnews
{
    # First the batch params
    &delbatch( );
    # Secondly the mail setup
    &delmail( );
    # Lastly the sys file
    &delnews( );
} # deluucp mailnews
```


Adding a host to this file is done by adding a number of configuration lines describing the characteristics of this host. Most of these characteristics are equal among the different hosts, the sole difference being the name of the UUCP machine. To add a host, simply fill out a template file that is concatenated to the existing sys file. The %% tokens in this template will be replaced by the actual name of the UUCP machine. To be able to delete a host later, the part added will be delimited by special comment lines that determine the beginning and end of a host section. The template is shown in Listing 16.2. As you can see, a number of %% tokens are present, and the beginning and ending of this host section are marked with START and END.

# Listing 16.1 (continued)

```
# Add host to news config for UUCP
sub adducpmanews
{
    # First the batch params
    $addbatch( );
    # Secondly the mail setup
    $addmail( );
    # Lastly the sys file
    $addnews( );
}
# adducpmanews

# Backup a file
sub backupfile
{
    local( $file ) = @_;
    local( $backup );

    # Back up older versions
    $backup = "$file"."~ooo";
    unlink $backup if( -e $backup );
    $backup = "$file"."~oo";
    rename $backup, "$backup"."~o" if( -e $backup );
    $backup = "$file"."~o";
    rename $backup, "$backup"."~o" if( -e $backup );
    rename $file, $backup;
}
# backupfile

# Set permissions on new file as they were on the old one
sub setperm
{
    local( $new, $old );

    ($dummy, $dummy, $mode, $dummy, $uid, $gid, $dummy) = stat $old;
    chown $uid, $gid, $new;
    chmod $mode, $new;
}
# setperm
```
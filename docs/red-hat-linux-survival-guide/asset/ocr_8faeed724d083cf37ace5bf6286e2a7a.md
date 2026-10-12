# Listing 15-6 Continued

```
# Get the length with the EXT
$dir_len = length($dir);

foreach $domain_ext (@domain_types){ $dir =~ s/\.$domain_ext//g; }

# Get the new length without the EXT
$temp_len = length($dir);

# If the user has not entered an extension then show syntax.
&syntax if($temp_len == $dir_len);

$named_file = $NAMED_PATH . '/' . $dir . $NAMED_FILE_EXT ;
$thesite_dir = $BASE_DIR . '/' . $dir;
$htdocs_dir = $BASE_DIR . '/' . $dir . '/' . $HTDOCS;
$cgibin_dir = $BASE_DIR . '/' . $dir . '/' . $CGIBIN;

die "$thesite_dir already exist! Aborted!\n" if(-e $thesite_dir);

system("mkdir $thesite_dir");
system("mkdir $htdocs_dir");
system("mkdir $cgibin_dir");

&createNamedFile($named_file,$site,"$dir$NAMED_FILE_EXT");
&createIndexFile($htdocs_dir,$site);
&createVirtualHostConf( domain=>$site,
                    website=>"www.$site",
                    cgibin=>$cgibin_dir,
                    htdocs=>$htdocs_dir);

system("chown -R $USER.$GROUP $thesite_dir");
system("chmod -R $PERMISSION $thesite_dir");

open(FP,">$LOG_FILE") || die "Can't write to log file.\n";
print FP "$date created www.$site [$htdocs_dir] site.\n";
close(FP);
```
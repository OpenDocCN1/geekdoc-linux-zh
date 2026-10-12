# Listing 8-6 *Continued*

```
foreach ($domain_ext {foreach ($domain_types) { $dir =~ s/\.\n
domain_ext//g; }

# Get the new length without the EXT
$temp_len = length($dir);

# If the user has not entered an extension, then show
# syntax.
$syntax if($temp_len == $dir_len);

$named_file = $NAMED_PATH . '/' . $dir . $NAMED_FILE_EXT
;

$testsite_dir = $BASE_DIR . '/' . $dir;

$htdocs_dir = $BASE_DIR . '/' . $dir . '/' . $HTDOCS;

$cgibin_dir = $BASE_DIR . '/' . $dir . '/' . $CGIBIN;

die "$testsite_dir already exists! Aborted!\n" if(-e
$testsite_dir);

system("mkdir $testsite_dir");

system("mkdir $htdocs_dir");

system("mkdir $cgibin_dir");

&createNamedFile($named_file,$site,"$dir$NAMED_FILE_EXT")
;

&createIndexFile($htdocs_dir,$site);

&createVirtualHostConf (domain=>$site,

website=>"$www.$site",

cgibin=>$cgibin_dir,

htdocs=>$htdocs_dir);

system("chown -R $USER.$GROUP $testsite_dir");

system("chmod -R $PERMISSION $testsite_dir");
```
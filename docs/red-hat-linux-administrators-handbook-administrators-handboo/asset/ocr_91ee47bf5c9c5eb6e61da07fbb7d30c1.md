```
my $LOG_FILE           = "$BASE_DIR/makesite.log";

my $dir = $site;
my @domain_types = qw(com net org edu);
my ($domain_ext, $thesite_dir, $public_dir,
$htdocs_dir, $cgibin_dir, $named_file,
$dir_len, $temp_len);

my $tm = localtime(time);
my $date = sprintf("%s-%02s-%02d-%02d", $tm-
>year+1900,
                                    $tm->mon+1,
                                    $tm->mday,
                                    $tm->hour,
                                    $tm->min);

my $serial = sprintf("%s%02d%02d000", $tm-
>year+1900,
                                    $tm->mon+1,
                                    $tm->mday);

$site =~ y/[A-Z]/[a-z]/;

# Get the length with the EXT
$dir_len = length($dir);

foreach $domain_ext (@domain_types){ $dir =~
s/\\.$domain_ext//g; }

# Get the new length without the EXT
$temp_len = length($dir);

# If the user has not entered an extension, then show
syntax.
```
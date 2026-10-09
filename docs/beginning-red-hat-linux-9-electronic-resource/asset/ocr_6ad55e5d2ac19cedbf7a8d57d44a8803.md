We have not talked about references at all in this chapter. We can use references to create complex data structures using the three basic data types that we are familiar with, namely scalars, arrays and hashes. We will look at references in more detail as we discuss this application.

```
sub process_dir
{
    $dir = shift;        ## Argument; from @_ or $_[0]
    my    (@min, %files, $size, $file, @sorted);
    local *PIPE2;                  ## Localize filehandle

##++
## Open a pipe to the /usr/bin/du command, with the -ab arguments;
## this is defined by the SDU constant. The -a switch returns sizes
## for all files, not just directories, and the -b switch returns
## the sizes in bytes -- instead of the default unit blocks.
##
## Sample output:
##     140        /home/postgres/global
##--

open (PIPE2, "$DU $dir |") || die "Cannot create pipe: $!\n";

$min    = 0;              ## Keep track of smallest file
%files = ();              ## Initialize hash

while (<PIPE2>) {                        ## Read record for file
    ($size, $file) = /^(\d+)\s(.+)\s*$;/;     ## Get the size and file
                                             ## from du

    last if ($file eq $dir);    ## End loop if we are finished
    next if (-d $file);        ## Ignore if file is directory

    if ($size > $min) {
        $files{$file} = $size;             ## Store each file and size

##++
## If we have more than 15 files in the %files hash, then
## we sort the values based on the file size and delete the
## file with the smallest size. At any given time, we will
## only have that number of files in the hash.
##--

    if (scalar keys %files > $NO_FILES) {
        @sorted= sort { %files{$a} <=> %files{$b} } keys %files;
        $min     = %files{ $sorted[1] };

        delete %files{ $sorted[0] };   ## Delete smallest file
    }
}

close (PIPE2);             ## Close pipe

```
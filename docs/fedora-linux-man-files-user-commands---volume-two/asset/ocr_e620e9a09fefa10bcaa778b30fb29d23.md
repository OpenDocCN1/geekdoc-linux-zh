**NOTE:** see the NOTE for the --shared option, and also the --dissociate option.

+   -dissociate  
+   Borrow the objects from reference repositories specified with the --reference options only to reduce network transfer and stop borrowing from them after a clone is made by making necessary local copies of borrowed objects.

+   -quiet, -q  
+   Operate quietly. Progress is not reported to the standard error stream. This flag is also passed to the ‘sync’ command when given.

+   -verbose, -v  
+   Run verbosely. Does not affect the reporting of progress status to the standard error stream.

+   -progress  
+   Progress status is reported on the standard error stream by default when it is attached to a terminal, unless -q is specified. This flag forces progress status even if the standard error stream is not directed to a terminal.

+   -no-checkout, -n  
+   No checkout of HEAD is performed after the clone is complete.

+   -bare  
+   Make a *bare* Git repository. That is, instead of creating <directory> and placing the administrative files in <directory>/.git, make the <directory> itself the $GIT_DIR. This obviously implies the -n because there is nowhere to check out the working tree. Also the branch heads at the remote are copied directly to corresponding local branch heads, without mapping them to refs/remotes/origin/. When this option is used, neither remote-tracking branches nor the related configuration variables are created.

+   -mirror  
+   Set up a mirror of the source repository. This implies --bare. Compared to --bare, --mirror not only maps local branches of the source to local branches of the target, it maps all refs (including remote-tracking branches, notes etc.) and sets up a refspec configuration such that all these refs are overwritten by a git remote update in the target repository.

+   -origin <name>, -o <name>  
+   Instead of using the remote name origin to keep track of the upstream repository, use <name>.

+   -branch <name>, -b <name>  
+   Instead of pointing the newly created HEAD to the branch pointed to by the cloned repository’s HEAD, point to <name> branch instead. In a non-bare repository, this is the branch that will be checked out. --branch can also take tags and detaches the
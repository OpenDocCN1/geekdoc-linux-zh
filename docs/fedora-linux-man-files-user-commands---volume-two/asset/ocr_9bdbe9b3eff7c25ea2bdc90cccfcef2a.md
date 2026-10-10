# ## NOTES

If you are creating a branch that you want to checkout immediately, it is easier to use the git checkout command with its -b option to create a branch and check it out with a single command.

The options --contains, --merged and --no-merged serve three related but different purposes:

—contains <commit> is used to find all branches which will need special attention if <commit> were to be rebased or amended, since those branches contain the specified <commit>.

—merged is used to find all branches which can be safely deleted, since those branches are fully contained by HEAD.

—no-merged is used to find branches which are candidates for merging into HEAD, since those branches are not fully contained by HEAD.
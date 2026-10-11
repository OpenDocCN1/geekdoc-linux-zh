-I, --match-case  Search for manual pages case-sensitively.

−regex Show all pages with any part of either their
names or their descriptions matching each
page argument as a regular expression, as
with apropos. Since there is usually no
reasonable way to pick a “best” page when
searching for a regular expression, this option
implies -a.

−wildcard Show all pages with any part of either their
names or their descriptions matching each
page argument using shell-style wildcards, as
with apropos −wildcard. The page
argument must match the entire name or
description, or match on word boundaries in
the description. Since there is usually no
reasonable way to pick a “best” page when
searching for a wildcard, this option implies -
a.

−names-only If the −regex or −wildcard option is used,
match only page names, not page
descriptions, as with whatis. Otherwise, this
option has no effect.

-a, --all By default, man will exit after displaying the
most suitable manual page it finds. Using this
option forces man to display all the manual
pages with names that match the search
criteria.

-u, --update This option causes man to perform an inode-
level consistency check on its database caches
to ensure that they are an accurate
representation of the filesystem. It will only
have a useful effect if man is installed with
the setuidbit set.

−no-subpages By default, man will try to interpret pairs of
manual page names given on the command
line as equivalent to a single manual page
name containing a hyphen or an underscore.
This supports the common pattern of
programs that implement a number of
subcommands, allowing them to provide
manual pages for each that can be accessed
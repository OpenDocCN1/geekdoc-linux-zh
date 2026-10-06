# NIS Configuration

The main NIS configuration file is /etc/nswitch.conf. Here are the contents of that file as it's distributed with Red Hat Linux:

```
# /etc/nswitch.conf
#n# An example Name Service Switch config file. This file
# should be sorted with the most-used services at the
# beginning.
#n# The entry '[NOTFOUND=return]' means that the search for an
# entry should stop if the search in the previous entry
# turned up nothing. Note that if the search failed due to
# some other reason (like no NIS server responding)
# the search continues with the next entry.
#n# Legal entries are:
```

```
# nisplus or nis      Use NIS+ (NIS version 3)
# nis or yp            Use NIS (NIS version 2),
#                      also called YP
# dns                  Use DNS (Domain Name
                      Service)
# files                Use the local files
# db                   Use the local database
                      (.db) files
# compat               Use NIS on compat mode
# [NOTFOUND=return]    Stop searching if not found
                      so far
```

```
# To use db, put the "db" in front of "files" for entries
# you want to be looked up first in the databases
#n# Example:
#passwd               db files nisplus nis
#shadow               db files nisplus nis
#group                db files nisplus nis
```
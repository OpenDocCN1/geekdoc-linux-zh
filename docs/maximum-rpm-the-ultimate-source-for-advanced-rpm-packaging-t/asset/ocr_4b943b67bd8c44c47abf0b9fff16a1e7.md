# ## 21.2.5. RPM Database Manipulation

The functions in this section perform the basic operations on the RPM database. This includes opening and closing the database, as well as creating the database. A function also exists to re-build a database that has been corrupted.

Every function that accesses the RPM database in some fashion makes use of the `rpmdb` structure. This structure is used as a handle to refer to a particular RPM database.

# ### 21.2.5.1. `rpmdbOpen()`—Open RPM Database

This function opens the RPM database located in `RPMVAR_DBPATH`, returning the `rpmdb` structure `db`. If `root` is specified, it is prepended to `RPMVAR_DBPATH` prior to opening. The `mode` and `perms` parameters are identical to `open(2)`'s `flags` and `mode` parameters, respectively:

```
```C
#include <rpm/rpmdb.h>

int rpmdbOpen(char * root,
               rpmdb * dbp,
               int mode,
               int perms);
```
```

The function returns `1` on error, and `0` on success.

# ### 21.2.5.2. `rpmdbClose()`—Close RPM Database

This function closes the RPM database specified by the `rpmdb` structure `db`. The `db` structure is also freed:

```
```C
#include <rpm/rpmdb.h>

void rpmdbClose(rpmdb db);
```
```

# ### 21.2.5.3. `rpmdbInit()`—Create RPM Database

This function creates a new RPM database to be located in `RPMVAR_DBPATH`. If the database already exists, it is left unchanged. If `root` is specified, it is prepended to `RPMVAR_DBPATH` prior to creation. The `perms` parameter is identical to `open(2)`'s `mode` parameter:

```
```C
#include <rpm/rpmdb.h>

int rpmdbInit(char * root,
              int perms);
```
```

The function returns `1` on error, and `0` on success.
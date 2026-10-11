# ### 21.2.12.2. rpmFreeSignature()—Free Signature Read by rpmReadPackageInfo()

This function frees the signature h:

```
#include <rpm/rpm-lib.h>
#include <rpm/header.h>

void rpmFreeSignature(Header h);
```

# ### 21.2.13. Header Manipulation

The header is one of the key data structures in rpm-lib. The functions in this section perform basic manipulations of the header.

The header is actually a data structure. It is not necessary to fully understand the actual data structure, but it is necessary to understand the basic concepts on which the header is based.

The header serves as a kind of miniature database. It can be searched for specific information, which can then be retrieved easily. As in a database, the information contained in the header can be of varying sizes.

# #### 21.2.13.1. headerRead()—Read a Header

This function reads a header from file fd, converting it from network byte order to the host system's byte order:

```
#include <rpm/rpm-lib.h>
#include <rpm/header.h>

Header headerRead(int fd,
                  int magicp);
```

If `magicp` is defined to be `HEADER_MAGIC_YES`, `headerRead()` will expect header magic numbers and will return an error if they are not present. Likewise, if `magicp` is defined to be `HEADER_MAGIC_NO`, `headerRead()` will not check the header's magic numbers and will return an error if they are present.

On error, this function returns **NULL**.

# #### 21.2.13.2. headerWrite()—Write a Header

This function writes the header h to the file fd, converting it from host byte order to network byte order. If `magicp` is defined to be `HEADER_MAGIC_YES`, `headerWrite()` will add the appropriate magic numbers to the header being written. If `magicp` is defined to be `HEADER_MAGIC_NO`, `headerWrite()` will not include magic numbers:

```
#include <rpm/rpm-lib.h>
#include <rpm/header.h>
```
void headerWrite(int fd,
    Header h,
    int magicp);

# 21.2.13.3. headerCopy()—Copy a Header

This function returns a copy of header h:

#include <rpm/rpmlib.h>
#include <rpm/header.h>

Header headerCopy(Header h);

# 21.2.13.4. headerSizeof()—Calculate a Header's Size

This function returns the number of bytes the header h takes up on disk. Note that in versions of RPM prior to 2.3.3, this function also changes the location of the data in the header. The result is that pointers from headerGetEntry() will no longer be valid. Therefore, any pointers acquired before calling headerSizeof() should be discarded:

#include <rpm/rpmlib.h>
#include <rpm/header.h>

unsigned int headerSizeof(Header h,
    int magicp);

# 21.2.13.5. headerNew()—Create a New Header

This function returns a new header.

#include <rpm/rpmlib.h>
#include <rpm/header.h>

Header headerNew(void);

# 21.2.13.6. headerFree()—Deallocate a Header

This function deallocates the header specified by h:

#include <rpm/rpmlib.h>
#include <rpm/header.h>

void headerFree(Header h);

# 21.2.13.7. headerDump()—Print Header Structure in Human-Readable Form

This function prints the structure of the header h to the file f. If the flags parameter is defined to be HEADER_DUMP_INLINE, the header's data is also printed:

#include <rpm/rpmlib.h>
#include <rpm/header.h>

void headerDump(Header h,
    FILE \*f,
    int flags);
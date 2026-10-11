
Standard stuff here. The first argument is supposed to be an RPM package file. It is opened here. If there is no argument on the command line, the program will use stdIn instead:

```c
if (argc == 1) {
    fd = 0;
} else {
    fd = open(argv[1], O_RDONLY, 0644);
}

if (fd < 0) {
    perror("open");
    exit(1);
}
```

Here things start to get interesting! The signature and headers are read from the package file that was just opened. Notice in the preceding code that we've defined sig and h to be of type header. That means we can use rpmlib's header-related functions on them. After a little bit of error checking, it's time to move on...

```c
stat = rpmReadPackageInfo(fd, &sig, &h);
if (stat) {
    fprintf(stderr,
        "rpmReadPackageInfo error status: %d\n%s\n",
        stat, strerror(errno));
    exit(stat);
}
```

Now that we have the package's header, we get the package name (specified by the RPMTAG_NAME in the call to headerGetEntry). Next, we see if the package has preinstall (RPMTAG_PREIN) or postinstall (RPMTAG_POSTIN) scripts. If it does, we print out a message, along with the package name:

```c
headerGetEntry(h, RPMTAG_NAME, &type, (void **) &name, &count);

if (headerIsEntry(h, RPMTAG_PREIN)) {
    printf("There is a preinstall script for %s\n", name);
}

if (headerIsEntry(h, RPMTAG_POSTIN)) {
    printf("There is a postinstall script for %s\n", name);
}
```

Turning to the other Header structure we've read, we print out the package's signatures in human-readable form. When we're done, we free the block of signatures:

```c
printf("Dumping signatures...\n");
headerDump(sig, stdout, 1);

rpmFreeSignature(sig);
```

We now set up an iterator for the package's header. This will allow us to step through each entry in the header:

```c
printf("Iterating through the header...\n");

iter = headerInitIterator(h);
```

This loop uses headerNextIterator() to return each entry's tag, type, data, and size. By using a switch statement on the tag, we can perform different operations on each type of entry in the header:

```c
while (headerNextIterator(iter, &iterTag, &type, p, &count)) {
    switch (iterTag) {
    case RPMTAG_SUMMARY:
        blather = p;
        printf("The Summary: %s\n", blather);
        break;
    case RPMTAG_FILENAMES:
        printf("There are %d files in this package\n", count);
        break;
    }
}
```

This is the housecleaning section of the program. First we free the iterator that we’ve been using, and finally the header itself:

```c
headerFreeIterator(iter);
headerFree(h);
}
```

Running this program on a package gives us the following output:

```text
# ./dump_amanda-client-2.3.0-2.i386.rpm
There is a postinstall script for amanda-client
Dumping signatures...
Entry count: 2
Data count: 20

Entry:
000 (1000) NAME INT32_TYPE 0x00000000 00000001
Data: 0000 0x00029f5d (171869)
Entry:
001 (1003) SERIAL BIN_TYPE 0x00000004 00000016
Data: 00027 01 f9 97 d8 2c 36 40
Data: 008 c6 4a 91 45 32 13 d1 62
Iterating through the header...
The Summary: Client-side Amanda package
There are 11 files in this package
#
```

### 21.3.2. Example #2

This example delves a bit more into the database-related side of rpmlib. After initializing rpmlib's variables by reading the appropriate rpmrc files, the code traverses the database records, looking for a specific package. That package's header is then dumped in its entirety.

As before, this is the normal way of including all of rpmlib's definitions:

```c
#include <errno.h>
#include <fcntl.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <stdlib.h>
#include <rpm/rpmlib.h>
```

Here are the data declarations. Note the declaration of db; this is how we will be accessing the RPM database:

```c
void main(int argc, char ** argv)
{
    Header h;
    int offset;
    int dspBlockNum = 0;              /* default to all */
    int blockNum = 0;
    int_32 type, count;
    char * name;
    rpmdb db;
```

Before opening the RPM database, it’s necessary to know where the database resides. This information is stored in rpmrc files, which are read by rpmReadConfigFiles(). To show that this function is really doing its job, we retrieve the RPM database path before and after the rpmrc files are read. Note that we test the return value of rpmGetVar(RPM_DBPATH) and, if it is null, we insert (none) in the printf() output. This prevents possible core dumps if no database path has been set; and besides, it’s more user friendly:

```c
printf("The database path is: %s\n",
        rpmGetVar(RPMVAR_DBPATH) ? rpmGetVar(RPM_DBPATH) : "(none)");

rpmReadConfigFiles(NULL, NULL, NULL, 0);

printf("The database path is: %s\n",
        rpmGetVar(RPMVAR_DBPATH) ? rpmGetVar(RPM_DBPATH) : "(none)");
```

Here we’re opening the RPM database and doing some cursory error checking to make sure we should continue:

```c
if (rpmdbOpen("", &db, O_RDONLY, 0644) != 0) {
    fprintf(stderr, "cannot open /var/lib/rpm/packages.rpm\n");
    exit(1);
}
```

We get the offset of the first database record:

```c
offset = rpmdbFirstRecNum(db);
```

Here we start a while loop based on the record offset. As long as there is a non-zero offset (meaning that there is still an available record), we get the record. If there’s a problem getting the record, we exit:

```c
while (offset) {
    h = rpmdbGetRecord(db, offset);
    if (!h) {
        fprintf(stderr, "headerRead failed\n");
        exit(1);
    }
```

Next, we get the package name entry from the record and compare it with the name of the package we're interested in. If it matches, we dump the contents of the entire record:

```c
headerGetEntry(h, RPMTAG_NAME, &type, (void **) &name, &count);
if (strcmp(name, argv[1]) == 0)
    headerDump(h, stdout, 1);
```

At the end of the loop, we free the record and get the offset to the next record:

```c
headerFree(h);

offset = rpmdbNextRecNum(db, offset);
}
```

At the end, we close the database and exit:

```c
rpmdbClose(db);
}
```

Here's the program's output, edited for brevity (notice that the database path changes from (null) to /var/lib/rpm after the rpmrc files are read):

```text
# ./showdb amanda-client
The database path is: (null)
The database path is: /var/lib/rpm
Entry count: 37
Data count: 5219

Entry      CT       TAG                  TYPE                OFFSET      COUNT
           : 000 (1000)NAME          STRING_TYPE        0x00000000 00000001
Entry      Data: 000 amanda-client
           : 001 (1001)VERSION      STRING_TYPE        0x0000000e 00000001
           Data: 000 2.3.0
Entry      : 002 (1002)RELEASE      STRING_TYPE        0x00000014 00000001
           Data: 000 7
Entry      : 003 (1004)SUMMARY      STRING_TYPE        0x00000016 00000001
           Data: 000 Client-side Amanda package
Entry      : 004 (1005)DESCRIPTION STRING_TYPE        0x00000031 00000001
           ...
Entry      : 017 (1027)FILENAMES   STRING_ARRAY_TYPE  0x00000df3 00000015
           Data: 000 /usr/doc/amanda-client-2.3.0-7
           Data: 001 /usr/doc/amanda-client-2.3.0-7/COPYRIGHT
           Data: 002 /usr/doc/amanda-client-2.3.0-7/INSTALL
           Data: 003 /usr/doc/amanda-client-2.3.0-7/README
           Data: 004 /usr/doc/amanda-client-2.3.0-7/SYSTEM.NOTES
           Data: 005 /usr/doc/amanda-client-2.3.0-7/WHATS.NEW
           Data: 006 /usr/doc/amanda-client-2.3.0-7/amanda-client.README
           ...
Entry      : 034 (1049)REQUIRENAME STRING_ARRAY_TYPE  0x0000141c 00000006
           Data: 000 libc.so.5
           Data: 001 libdb.so.2
           Data: 002 grep
           Data: 003 sed
           Data: 004 NetKit-B
           Data: 005 dump
           ...
```

As you can see, everything that you could possibly want to know about an installed package is available using this method.

### 21.3.3. Example #3

This example is similar in function to the previous one, except that it uses rpmlib’s search functions to find the desired package record. Here we include rpmlib’s definitions:

```c
#include <errno.h>
#include <fcntl.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <stdlib.h>

#include <rpm/rpmlib.h>
```

Here are the storage declarations:

```c
void main(int argc, char ** argv)
{
    Header h;
    int stat;
    rpmdb db;
    dbiIndexSet matches;
```

In this section, we do some argument processing, process the rpmrc files, and open the RPM database:

```c
if (argc != 2) {
    fprintf(stderr, "showdb2 <search term>\n");
    exit(1);
}

rpmReadConfigFiles(NULL, NULL, NULL, 0);

if (rpmdbOpen("", &db, O_RDONLY, 0644) != 0) {
    fprintf(stderr, "cannot open /var/lib/rpm/packages.rpm\n");
    exit(1);
}
```

In this section, we use rpmdbFindPackage() to search for the desired package:

```c
stat = rpmdbFindPackage(db, argv[1], &matches);
printf("Status is: %d\n", stat);
if (stat == 0) {
    if (matches.count) {
        printf("Number of matches: %d\n", matches.count);
        h = rpmdbGetRecord(db, matches.recs[0].recOffset);
        if (h) headerDump(h, stdout, 1);
        headerFree(h);
        dbiFreeIndexRecord(matches);
    }
}
```

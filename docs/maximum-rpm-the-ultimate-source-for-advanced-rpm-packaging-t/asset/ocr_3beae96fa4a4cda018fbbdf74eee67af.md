```
short type;  
short archnum;  
char name[86];  
short osnum;  
short signature_type;  
char reserved[16];
};
```

Let's take a look at an actual package file and examine the various pieces of data that make up the lead. In the following display, the number to the left of the colon is the byte offset, in hexadecimal, from the start of the file. The eight groups of four characters show the hex value of the bytes in the file—2 bytes per group of four characters. Finally, the characters on the right show the ASCII values of the data bytes. When a data byte's value results in a non-printable character, a dot (.) is inserted instead. Here are the first 32 bytes of a package file—in this case, the package file rpm-2.2.1-1.1386.rpm:

```
00000000: edab eedb 0300 0000 0001 7270 6d2d 322e rpm-2. 
00000010: 322e 312d 3100 0000 0000 0000 0000 2.1.1.…….…….
```

The first 4 bytes (edab eedb) are the magic values that identify the file as an RPM package file. Both the file command and RPM use these magic numbers to determine whether a file is legitimate.

The next 2 bytes (0300) indicate the RPM file format version. In this case, the file’s major version number is 3, and the minor version number is 0. Versions of RPM later than 2.1 create version 3.0 package files.

The next 2 bytes (0000) determine what type of RPM file the file is. There are presently two types defined:

+   - Binary package file (type=0000)
+   - Source package file (type=0001)

In this case, the file is a binary package file.

The next 2 bytes (0001) are used to store the architecture that the package was built for. In this case, the number 1 refers to the i386 architecture. (Note that the architecture used internally by RPM is actually stored in the header. This value is strictly for file(1)’s use.) In the case of a source package file, these two bytes should be ignored, as source packages are not built for a specific architecture.

The next 66 bytes (starting with 7270 6d2d) contain the name of the package. The name must end with a null byte, which leaves 65 bytes for RPM’s usual name-version-release-style name. In this case, we can read the name from the right side of the output:

rpm-2.2.1-1
Since the name rpm-2.2.1-1 is shorter than the 65 bytes allocated for the name, the leftover bytes are filled with nulls.
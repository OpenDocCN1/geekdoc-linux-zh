peeking. Storing the plaintext password as part of a command line in an automated script is even worse. Whenever possible, use the non-echoing, interactive prompt to enter passwords. (And where security is truly important, use strong encryption such as Pretty Good Privacy instead of the relatively weak encryption provided by standard zipfile utilities.)

**-q**

Perform operations quietly (**-qq** = even quieter). Ordinarily *unzip* prints the names of the files it's extracting or testing, the extraction methods, any file or zipfile comments that may be stored in the archive, and possibly a summary which finished with each archive. The **-q**[**-q**] options suppress the printing of some or all of these messages.

**-s**

[OS/2, NT, MS-DOS] convert spaces in filenames to underscores. Since all PC operating systems allow spaces in filenames, *unzip* by default extracts filenames with spaces intact (e.g., "E DATA . SF" ). This can be awkward, however, since MS-DOS in particular does not gracefully support spaces in filenames. Conversion of spaces to underscores can eliminate the awkwardness in some cases.

**-U**

(Obsolete; to be removed in a future release.) Leave filenames uppercase if created under MS-DOS, VMS, etc. See **-L** above.

**-V**

Retain (VMS) file version numbers. VMS files can be stored with a version number, in the format file .ext ; ## . By default the " ; ##" version numbers are stripped, but this option allows them to be retained. (On file systems that limit filenames to particularly short lengths, the version numbers may be truncated or stripped regardless of this option.)

**-X**

[VMS, Unix, OS/2, NT] Restore owner/protection info (UICs) under VMS, or user and group info (UID/GID) under Unix, or access control lists (ACLs) under certain network-enabled versions of OS/2 (Warp Server with IBM LAN Server/Requester 3.0 to 5.0; Warp Connect with IBM Peer 1.0), or security ACLs under
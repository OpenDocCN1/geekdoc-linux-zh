There are no special requirements for the software being added to the repository. However, when a program is added or updated, CVS read through the file looking for special strings. If they are present, CVS replaces these strings with the latest information about this copy of the program. CVS documentation refers to these strings as *keywords*, although they are not keywords in the Bash sense.

+   • $Author$—The login name of the user who checked in the revision.
+   
+   • $Date$—The date and time (UTC) the revision was checked in.
+   
+   • $Header$—A standard header containing the full pathname of the RCS file, the revision number, the date (UTC), the author, and so forth.
+   
+   • $Id$—Same as $Header$, except that the RCS filename is without a path.
+   
+   • $Name$—If tags are being used, this is the tag name used to check out this file.
+   
+   • $Locker$—The login name of the user who locked the revision (empty if not locked, which is the normal case unless *cvs admin -l* is in use).
+   
+   • $Log$—The log message supplied during the commit, preceded by a header containing the RCS filename, the revision number, the author, and the date (UTC). Existing log messages are not replaced. Instead, the new log message is inserted after *$Log$*.

+   • $RCSfile$—The name of the CVS file without a path.
+   
+   • $Revision$—The revision number assigned to the revision.
+   
+   • $Source$—The full pathname of the CVS file.
+   
+   • $State$—The state assigned to the revision.

The CVS keywords can be added anywhere in a script, but they should appear in a comment or in a quoted string if not in a comment. This prevents the keyword from being treated as an executable shell command.

```
# CVS: $Header$ 

When the script is added to the repository, CVS will fill in the header information.

# CVS: $Header: /home/repository/scripts/t.sh,v 1.1 2001/03/26 
20:35:27 kburch Exp $
```

The CVS keyword header should be placed in the header of a script.

```
#!/bin/bash
#
# flush.sh: Flush disks if nobody is on the computer
#
# Ken O. Burch
# CVS: $Header$
```

CVS is controlled using the Linux *cvs* command. *cvs* is always followed by a CVS command word and any parameters for that command.
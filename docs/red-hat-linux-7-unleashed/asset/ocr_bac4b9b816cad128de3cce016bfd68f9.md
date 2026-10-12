+   * `add`—Adds new files in cvs records.
+   * `import`—Adds new sources into the repository.
+   * `remove`—Eliminates files from the repository.
+   * `commit`—Publishes changes to other repository developers.

RCS and CVS may be used for more than software development projects. These tools may also be used for document preparation and workgroup editing of documents, and will work with any text files. Both systems use registration and control files to accomplish revision management. Both systems also offer the opportunity to revisit any step or branch in a revision *history*, and to restore previous versions of a project. This mechanism is extremely important in cross-platform development or for software maintenance.

Tracking information is usually continued in separate control files, and each document within a project may contain information automatically updated with each change to a project using a process called *keyword substitution*. CVS can use keywords similar to RCS, which are usually included inside C comment strings (`/* */`) near the top of a document. A sample of the available keywords includes

+   * `$Author$`—Username of person performing last check-in.
+   * `$Date$`—Date and time of last check-in.
+   * `$Header$`—Inserts the pathname of the document's RCS file, revision number, date and time, *author*, and state.
+   * `$Id$`—Same as `$Header$`, but without full pathname.
+   * `$Name$`—A symbolic name (see the co man page).
+   * `$Revision$`—The assigned revision number (such as 1.1).
+   * `$Source$`—RCS file's full pathname.
+   * `$State$`—The state of the document, such as `Exp` for experimental, `Rel` for released, or `Stab` for stable.

These keywords may also be used to insert version information into compiled programs by using character strings in program source code. For example, given an extremely short C program named foo.c:

```
```c
/* $Header$ */
#include <stdio.h>
static char rsrcid() = "$Header$";
main() {
  printf('Hello, Linux!\n');
}
```
```
# PROCESSING OF TEXT FILES 279

```
(Linux):"/examples> diff hello.c hello.c
4c4
  < printf("Hello World!\n");
  > printf("Hello Welt!\n");
(Linux):"/examples> diff -u hello.c hello.c
--- hello.c Sun Nov 2 10:44:09 1997
+++ hello.c Sun Nov 2 10:45:04 1997
@@ -1,5 +1,5 @@
#include <stdio.h>
main() {
  - printf("Hello World!\n");
  + printf("Hello Welt!\n");
}
(Linux):"/examples> diff -y --width=40 hello.c hello.c
#include <stdio.h>
main() {
  printf("Hello World!\n"); | printf("Hello Welt!\n");
}
```

**Listing 10.22** Applying the program.

Personally, I think that unified diffs provide better readability; in both cases you can insert the changes using patching them into slightly modified files.

The third example in Listing 10.22 shows the representation of both versions next to each other. This is often useful to get a quick overview of modifications, when dealing with files with short lines and a terminal with many columns.

The Emacs editor has special modes (ediff and emerge) to show the differences between files and, if necessary, to adapt the files appropriately. Under X, differences are shown in different colours, and changes can be performed with a single keystroke. ediff can be used under Emacs for two or three files (ediff, ediff3), buffers (ediff-buffers, ediff-buffers3), or directories (ediff-directories, ediff-directories3). In addition, it is possible to compare revisions created by the Revision Control System (see Section 11.5).

When you call ediff, Emacs asks for two files to compare with each other. These files are loaded into two buffers, A and B. You can now navigate through these files with single keystrokes. The ? key displays a menu with the available shortcuts. If you wish to try this out, just copy any file (for example
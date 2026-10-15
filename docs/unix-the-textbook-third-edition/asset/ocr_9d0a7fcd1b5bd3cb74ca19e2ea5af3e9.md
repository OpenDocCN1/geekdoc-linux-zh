```
nothing added to commit but untracked files present (use "git add" to track)
%
```

10. Now lets make a change in the file hello.c, and track the changes with some of the forms of the git diff command. First, edit the file with your favorite text editor, and on the fourth line, add Torvalds after the word Linus, as shown in the following command output:

```
% nl hello.c
  1 #include <stdio.h>
  2 int main ()
  3 {
  4     printf("%s\n", "Hello Linus Torvalds");
  5     return 0;
  6 }
%
```

11. Examine the status of the repository. The output shows that the file has been changed since the last commit, but has not been staged for a new commit yet.

```
% git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
        modified:   hello.c
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        a.out
no changes added to commit (use "git add" and/or "git commit -a")
%
```

12. Now we use git diff to see the difference between what is in the working directory and the index.

```
% git diff
diff --git a/hello.c b/hello.c
index f907257..621aad0 100644
--- a/hello.c
+++ b/hello.c
@@ -1,6 +1,6 @@
#include <stdio.h>
int main ()
{
-    printf("%s\n", "Hello Linus");
```
matching to specify which chapters match to the filename argument of the cp command.

```
[studenterver vacation] $ cd ~/documents/my_bestseller
[studenterver my_bestseller]$ $ cp chapters/mystery_chapter[56].ofd changes
[studenterver my_bestseller]$ $ ls chapters
myst_chapter3.ofd mystery_chapter5.ofd
myst_chapter4.ofd mystery_chapter6.ofd
[studenterver my_bestseller]$ $ ls changes
myst_chapter5.ofd mystery_chapter6.ofd
```

15. Change your current date to the changes directory.
Use the date +F with command substitution to copy mystery_chapter5.ofd to a new file which includes the full date. The date should have the form my_chapter5_YYYY-MM-DD.ofd.
Make another copy of mystery_chapter5.ofd, appending the current timestamp (as the number of seconds in the epoch, 1970-01-01 00:00:00) to ensure a unique filename. Use command substitution with the date +%s to accomplish this.

```
[studenterver my_bestseller]$ $ cd changes
[studenterver changes]$ $(date +F) cp mystery_chapter5.ofd \
> mystery_chapter5_$(date +%F).ofd
[studenterver changes]$ $ cp mystery_chapter5.ofd \
> mystery_chapter5_$(date +s).ofd
[studenterver changes]$ $ ls
mystery_chapter5_149254876.ofd mystery_chapter5.ofd
mystery_chapter5_2017-04-18.ofd mystery_chapter6.ofd
```

16. After further review, decide that the chapters are not necessary. Delete the directory.
If necessary, navigate to the changes directory and delete all the files in the directory.
You cannot delete a directory while it is the current working directory. Change to the parent of the changes directory. Try to delete the directory using the rm command -r recursive option. This attempt should fail. Finally, use the rdir command to delete the empty directory, which will succeed.

```
[studenterver changes]$ $ rm mystery*
[studenterver changes]$ $ cd ..
[studenterver my_bestseller]$ $ rm changes
rm: cannot remove 'changes': Is a directory
[studenterver my_bestseller]$ $ rdir changes
[studenterver my_bestseller]$ $ ls
chapters editor vacation
```

17. When the vacation is over, the vacation directory is no longer needed. Delete it using the rm command with the recursive option.
When finished, return to the student's home directory.

```
[studenterver my_bestseller]$ $ rm - vacation
[studenterver my_bestseller]$ $ ls
chapters editor
[studenterver my_bestseller]$ $ cd
```
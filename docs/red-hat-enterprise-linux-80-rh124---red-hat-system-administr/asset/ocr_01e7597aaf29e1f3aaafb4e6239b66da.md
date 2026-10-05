subdirectory, use brace expansion with a range to specify the chapter filenames to move and
el relative path for the destination directory.

```
[student@serverchap]$ ls my_chapter(1..2).odd ../editor
[student@serverchap]$ ls
myst_chapter3.odd mystery_chapter5.odd mystery_chapter7.odd
myst_chapter4.odd mystery_chapter6.odd mystery_chapter8.odd
[student@serverchap]$ ls ../editor
myst_chapter1.odd mystery_chapter2.odd
```

+   11. When you are wanted to write chapters 7 and 8. Use a single command to move the
files from the chapters to the vacation directory. Specify the chapter filenames
using brace expansion with a list of strings and without using wildcard characters.

```
[student@serverchap]$ ls my_chapter{7,8}.odd ..
[student@serverchap]$ ls
myst_chapter3.odd mystery_chapter5.odd
myst_chapter4.odd mystery_chapter6.odd
[student@serverchap]$ ls ../vacation
myst_chapter7.odd mystery_chapter8.odd
```

+   12. Change your working directory to ~/Videos/season2, and then copy the first episode
the season to the vacation directory.

```
[student@season2]$ cd ~/videos/season2
[student@season2]$ cp *episode1.ogg ~/Documents/my_bestseller/vacation
```

+   13. Use a single command to change from your working directory to ~/Documents/
_bestseller vacation directory. Use the previous working directory
argument to return to the season2 directory (This will succeed if the last directory
change with the cd command was accomplished with one command rather than several
cd commands). From the season2 directory, copy the episode 2 file into the vacation
directory. Use the shortcut to return to the vacation directory.

```
[student@season2]$ cd ~/Documents/my_bestseller/vacation
[student@vacation]$ ls
myst_chapter7.odd mystery_chapter8.odd tv_season2_episode1.ogg
[student@vacation]$ cd -
/home/ec2~/videos/season2
[student@season2]$ cp *episode2.ogg ~/Documents/my_bestseller/vacation
[student@vacation]$ cd
/home/ec2~/Documents/my_bestseller/vacation
[student@vacation]$ ls
myst_chapter7.odd tv_season2_episode1.ogg
myst_chapter8.odd tv_season2_episode2.ogg
```

+   14. The authors of chapters 5 and 6 want to experiment with possible changes. Copy both files
from the ~/Documents/my_bestseller/chapters directory to the ~/Documents/
my_bestseller/changes directory to prevent these changes by modifying original files.
Navigate to the ~/Documents/my_bestseller directory. Use square-bracket pattern
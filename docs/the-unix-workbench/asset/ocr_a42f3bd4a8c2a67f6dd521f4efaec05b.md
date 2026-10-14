```
## -rw-rw-r-- 1 sean sean 138 Jun 26 12:51 addseq\
.sh
## -rw-rw-r-- 1 sean sean 146 Jun 26 14:45 addseq\
2.sh
## -rw-rw-r-- 1 sean sean 140 Jan 29 10:06 bigmat\
h.sh
```

The left column of this table contains a series of individual characters and dashes. The first hyphen (-) signifies that each of the entries in this list are files. If any of them were directories then instead of a hyphen there would be a d. Excluding the first hyphen we have the following string: rw-rw-r--. This string reflects the permissions that are set up for this file. There are three permissions that we can grant: the ability to read the file (r), write to or edit the file (w), or execute the file (x) as a program. These three permissions can be granted on three different levels of access which correspond to each of the three sets of rwx in the permissions string: the owner of the file, the group that the file belongs to, and everyone other than the owner and the members of a group. Since you created the file you are the owner of the file, and you can set the permissions for files that you own using the chmod command.

The chmod command takes two arguments. The first argument is a string which specifies how we’re going to change permissions for a file, and the second argument is the path to the file. The first argument has to be composed in a very specific way. First we can specify which set of users we’re going to change permissions for:
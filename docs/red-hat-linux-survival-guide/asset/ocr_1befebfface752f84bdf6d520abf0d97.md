```
locate foo
/usr/lib/texmf/tex/latex/misc/footnpag.sty
/usr/share/automake/footer.am
/usr/share/games/fortunes/food
/usr/share/games/fortunes/food.dat
/usr/share/gimp/patterns/moonfoot.pat
```

The output of locate contains the keyword “foo” in the absolute path or does not have any output.

# ls

Syntax: ls [-laRl] file or directory

The ls command allows you to list files (and subdirectories) in a directory. It is one of the most popular programs used in Linux. The following Table A-3 shows some of the more popular options for ls.

Table A-3 Popular Options for ls

| Option | What It Displays |
| -1 | Only the file and directory names in the current directory |
| -l | A long listing containing file and directory permission information, size, modification date, and so on |
| -a | All files and directories (including the ones that have a leading period in their names) within the current directory |
| -R | Displays the contents of the subdirectories (if any) recursively |

# mkdir

Syntax: mkdir directory . . .

To make a directory, use the mkdir command. You have only two restrictions when choosing a directory name: (1) File names can be up to 255 characters long, and (2) directory names can contain any character except the /. For example, the following example creates three subdirectories in the current directory:

```
mkdir dir1 dir2 dir3
```
depending on what kind of file it is, do something different with the file. So you could take output from a find command, for example, that found every file that you hadn’t changed in the last month to create a filelist, and then do something with those files, depending on what sorts of files they were. You could remove all of them with "tmp" in the name, move any with "sav" in the name to an archive directory, and so forth. Figure 13-2 shows a script to do just that.

# How should I use the select statement?

The Korn shell’s select construct is a unique way to build a simple menu and branch based on the response to that menu. The select statement doesn’t really line up with any corresponding statement in C or Pascal or any other language we know about. But it certainly makes it easy for you to do things that might otherwise be a nuisance. The basic syntax of select is

```
select var [in list]
do
    statements that act on or use $var
 done
```

![](bbox=[0.18, 0.62, 0.88, 0.91])

Figure 13-2 Case lets you do different things with different files, all in one easy to understand statement
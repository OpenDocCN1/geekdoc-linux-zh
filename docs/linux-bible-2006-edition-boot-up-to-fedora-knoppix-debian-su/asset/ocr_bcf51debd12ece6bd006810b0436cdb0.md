# Chapter 29 ✦ Programming Tools and Utilities 805

6. Do as the instructions recommend: Execute the command `cvs commit` to make the added files and directories permanent. You'll first see a screen (which is actually a vi editor session) asking you to enter a log message. If you don't want to enter a log message, press `Esc`, type `ZZ` to save and exit. After you see the vi commit, the output should resemble the following:

```
$ cvs commit
cvs commit: Examining
RCS file: /space/cvs/newhello/hello.c.v
done
Checking in hello.c;
/space/cvs/newhello/hello.c.v <-- hello.c
initial revision: 1.1
done
RCS file: /space/cvs/newhello/msg.c.v
done
Checking in msg.c;
/space/cvs/newhello/msg.c.v <-- msg.c
initial revision: 1.1
done
RCS file: /space/cvs/newhello/showit.c.v
done
Checking in main.c;
/space/cvs/newhello/main.c.v <-- main.c
initial revision: 1.1
done
```

Notice that CVS RCS file-naming conventions to work with files in the repository. This is because CVS is built on top of RCS and retains compatibility with the basic RCS feature set.

CVS handles checking files in and out slightly differently than RCS. When checking out file, it is not necessary to specifically request a lock to get a writable-copy of the file. To work on a file, you need to use the `checkout` or `co` command:

```
$ ~/projects
$ cvs -d /space/cvs co newhello
cvs checkout newhello
U newhello/hello.c
U newhello/msg.c
U newhello/main.c
```

The **checkout** command used in this example specifies the path to the repository using the `-d` option. This is unnecessary if you set the `$CVSROOT environment variable. After you have made changes to files, you can check them in using the `cvs commit` command (commit is comparable to RCS's `ci` command):

```
$ cd ~/project/newhello
$ cvs commit
cvs commit: Examining .
```
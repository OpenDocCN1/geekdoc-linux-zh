# command cp

# Syntax:

```
cp file1 file2
cp file1 [file2 ...] directory
cp -r dir1 dir2
cp -r dir1 [dir2 ...] directory
```

copies files or directories. The original file/directory remains unmodified.

# option:

-r directories are copied recursively with all sub-directories.

# Several possibilities:

```
cp file1 file2
```

file1 is copied to file2. Attention: if file2 already exists, it is overwritten (mostly without warning), and the original file2 is lost!!!

```
cp file1 [file2 file3] dir
```

If dir exists, file1 [, file2, file3] are copied into dir. If dir does not exist, you get an error warning (for more than two arguments), or, for two arguments, dir is interpreted as a file name and file1 is copied to a file named dir.

```
cp -r dir1 dir2
```

If dir2 already exists, dir1 is recursively copied into dir2. If dir2 does not exist, a recursive copy of dir1 is created and named dir2.

```
cp -r dir1 dir2 dir3 dir4
```

If dir4 already exists, dir1, dir2, dir3 are copied into dir4. If dir4 does not exist, you get an error warning, as well as for other combinations of files and directories within the command.

# Example:

```
wegner@arber:~ > ls
hello* hello.cpp hello.f90 nsmail/ numerik/
wegner@arber:~ > cp hello.cpp hello2.cpp
wegner@arber:~ > ls
hello* hello.f90 nsmail/
hello.cpp hello2.cpp numerik/
wegner@arber:~ > cp hello.cpp numerik
wegner@arber:~ > ls numerik
hello.cpp
wegner@arber:~ >
```

# Exercise:

+   a) Check whether the directory ubung0 is present in your home directory. If not, copy, via scp, the directory ubung0 from account/host numprakt@ltsp08.usm.uni-muenchen.de to your home directory.

+   b) Copy the files from ubung0 into your directory yourname.exercise!
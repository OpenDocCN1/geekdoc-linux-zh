# command mv

# Syntax:

```
mv file1 file2
mv file1 [file2 ...] directory
mv dir1 dir2
mv dir1 [dir2 ...] directory
```

Rename or move files or directories. Similar to cp, but original is 'destroyed'. First command from above renames files, other commands move files/directories. (Actually, only the pointer in the 'inode table' is changed, but there is no physical move – except if you move the file to another file system).

Note: no option [-r] required

Several possibilities, analogue to cp.

# Example:

```
wegner@arber:~> ls
hello*      hello.f90  nsmail/
hello.cpp   hello2.cpp numerik/
wegner@arber:~> mv hello2.cpp hello3.cpp
wegner@arber:~> ls
hello*      hello.f90  nsmail/
hello.cpp   hello3.cpp numerik/
wegner@arber:~> ls numerik
hello.cpp
wegner@arber:~> mv hello3.cpp numerik
wegner@arber:~> ls
hello*  hello.cpp  hello.f90  nsmail/  numerik/
wegner@arber:~> ls numerik
hello.cpp  hello3.cpp
wegner@arber:~>
```

# Exercise:

+   1. Rename your directory yourname.exercise to yourname.exercise0! This will be your working directory for the following exercises.
+   2. Move the file .plan from yourname.exercise0 to your home directory! Try to move an arbitrary file from your home directory to the root directory. What happens?
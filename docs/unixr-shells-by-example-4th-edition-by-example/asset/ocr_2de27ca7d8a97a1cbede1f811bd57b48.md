# 4.4 grep with Pipes

Instead of taking its input from a file, grep often gets its input from a pipe.

# EXAMPLE 4.29

```
% ls -l
drwxrwxrwx 2 ellie 2441 Jan 6 12:34 dir1
-rw-r--r-- 1 ellie 1538 Jan 2 15:50 file1
-rw-r--r-- 1 ellie 1539 Jan 3 13:36 file2
-rw-r--r-- 2 ellie 2341 Jan 6 12:34 grades

% ls -l | grep '^d'
drwxrwxrwx 2 ellie 2441 Jan 6 12:34 dir1
drwxrwxrwx 2 ellie 2341 Jan 6 12:34 grades
```

# EXPLANATION

The output of the ls command is piped to grep. All lines of output that begin with a d are printed; that is, all directories are printed.

# 4.4.1 grep Review

Table 4.3 contains examples of grep commands and what they do.

# Table 4.3 Review of grep

| Command | What It Does |
|---|---|
| grep '\<Tom\>' file | Prints lines containing the word Tom. |
| grep 'Tom Savage' file | Prints lines containing Tom Savage. |
| grep '^Tommy' file | Prints lines if Tommy is at the beginning of the line. |
| grep '\.bak$' file | Prints lines ending in .bak. Single quotes protect the dollar sign ($) from interpretation. |
| grep '[Pp]yramid' * | Prints lines from all files containing pyramid or Pyramid in the current working directory. |
| grep '[A-Z]' file | Prints lines containing at least one capital letter. |
| grep '[0-9]' file | Prints lines containing at least one number. |
| grep '[A-Z][...][0-9]' file | Prints lines containing five-character patterns starting with a capital letter and ending with a number. |
| grep -w '[Tt]est' files | Prints lines with the word Test and/or test. |
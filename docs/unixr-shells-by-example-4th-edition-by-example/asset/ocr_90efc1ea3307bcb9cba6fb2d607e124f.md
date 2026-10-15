# EXAMPLE 10.20

```
(The Script)
#!/bin/tcsh -f
# Scriptname: filecheck
# Usage: filecheck filename
1 alias Usage 'echo "  Usage: $0 filename\n" ; exit 1'
2 alias Error 'echo "  Error: \!* ; exit 2'
3 set file=$1
4 if ( $#argv == 0 ) then
    Usage
endif
5 if ( ! -e $file ) then
    Error "$file does not exist"
endif

(The Command Line)
% filecheck
Usage: filecheck filename
% echo $status
1

% filecheck xyzfile
Error: xyzfile does not exist
% echo $status
2
```

# 10.6.12 Using the Status Variable in a Script

The status variable can be used in a script to test the status of a command. The status variable is assigned the value of the last command that was executed.

# EXAMPLE 10.21

```
(The Script)
#!/bin/csh -f
1 ypmatch $1 passwd > /dev/null
2 if ( $status == 0 ) then
3    echo Found $1 in the NIS database
endif
```

# EXPLANATION

+   1. The ypmatch program checks the NIS database to see if the name of the user, passed in as the first argument, is in the database.
+   2. If the status returned from the last command is 0, the then block is executed.
+   3. This line is executed if the if test expression evaluated to be true.
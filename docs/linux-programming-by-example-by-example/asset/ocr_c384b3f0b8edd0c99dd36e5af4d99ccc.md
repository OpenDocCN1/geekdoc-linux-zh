# Output

```
```
RCS/howdy.c,v  -->  howdy.c
revision 2.1 (locked)
done
```
```

When used with `ci`, `-f` forces RCS to check in a file even if it has not changed.

# RCS Keywords

RCS keywords are special, macro-like tokens used to insert and maintain identifying information in source, object, and binary files. These tokens take the form `$KEYWORD$`. When a file containing RCS keywords is checked out, RCS expands `$KEYWORD$` to `$KEYWORD: VALUE$`.

# $Id$

That peculiar string at the top of the listing for howdy.c, `$ Id $`, is an RCS keyword. The first time you checked out `howdy.c`, RCS expanded it to something like

```
```
$ Id: howdy.c,v 1.1 1999/07/20 04:56:08 kwall Exp kwall $
```
```

The format of the `$ Id $` string is as follows:

```
```
$KEYWORD: FILENAME REV_NUM DATE TIME AUTHOR STATE LOCKER $
```
```

On your system, most of these fields will have different values. If you checked out the file with a lock, you will also see your login name after the Exp entry.

# $Log$

RCS replaces the `$ Log $` keyword with the log message you supplied during check in. Rather than replacing the previous log entry, though, RCS inserts the new log message above the last log entry.

# Example

![](bbox=[0.04, 0.68, 0.1, 0.73])

# Example

This code listing shows how the `$ Log $` keyword is expanded after several check ins.

![](bbox=[0.04, 0.8, 0.14, 0.84])

# Output
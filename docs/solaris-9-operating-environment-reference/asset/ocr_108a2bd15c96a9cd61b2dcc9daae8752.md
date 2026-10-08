# localedef

# Operands

localename Identify the locale. If the name contains one or more slash characters, interpret localename as a path name where the created locale definitions are stored. This capability can be restricted to users with appropriate privileges. (You can process one category by specifying just one localename, although you can process several categories in one execution.)

localedef creates a temporary C source file that represents the locale's data. localedef calls the C compiler to compile this C source file into a shared object. This object is named localename.so.1 localedef also creates a text file localename for information only.

If you specify the -m32 option, localedef calls the C compiler for generating 32-bit objects and generates a 32-bit locale object. If you specify the -m64 option, localedef calls the C compiler for generating 64-bit objects and it generates a 64-bit locale object.

If you do not specify the -m option, localedef calls the C compiler for generating 32-bit objects and generates a 32-bit locale object. If you specify no options other than -c, -f, and -i, and if the system supports localedef additionally calls the C compiler for generating 64-bit objects and generates a 64-bit locale object.

If you specify the -m32 option, localedef generates a 32-bit locale object named localename.so.version_number.

If you specify the -m64 option, localedef generates a 64-bit locale object named localename.so.version_number.

If you do not specify the -m option, localedef generates a 32-bit locale object named localename.so.version_number, and if appropriate, generates a 64-bit locale object named 64-bit_architecture_name localename.so.version_number.

You must move the shared object for the 32-bit environment to:

```
/usr/lib/local/localename/localename.so.version_number
```

You must move the shared object for the 64-bit environment to:

```
/usr/lib/local/localename/sparcv9/localename.so.version_number
```

localedef also generates a text file named localename that is used for information only.

# Environment Variables

environ(5) for definitions of the following environment variables that affect the execution of localedef: LC_TYPE, LC_MESSAGES, and NLPATH.
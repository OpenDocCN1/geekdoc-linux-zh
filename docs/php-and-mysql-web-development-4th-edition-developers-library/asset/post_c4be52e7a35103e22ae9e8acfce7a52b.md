
3. Point the `buffer` member of each parameter to the variable where the corresponding column value should be stored when rows are fetched.

4. Set the `is_unsigned` member for the integer parameter to zero.

5. For the string parameter, set the `buffer_length` value to the maximum number of bytes that should be fetched, and set `length` to the address of an `unsigned long` variable. At fetch time, this variable will be set to the actual number of bytes fetched.

6. For every parameter, set the `is_null` member to the address of a `my_bool` variable. At fetch time, these variables will be set to indicate whether the fetched values are *NULL*. (Our program ignores these variables after fetching rows because we know that the test table contains no *NULL* values. In the general case, you should check them.)

After setting up the parameters, we bind the array to the statement by calling `mysql_stmt_bind_result()`, and then execute the statement.

At this point, you can immediately begin fetching rows by calling `mysql_stmt_fetch()`. Our program demonstrates an optional step that you can do first: It calls `mysql_stmt_store_result()`, which fetches the entire result set and buffers it in client memory. The advantage of doing this is that you can call `mysql_stmt_num_rows()` to find out how many rows are in the result set. The disadvantage is that it uses more memory on the client side.

The row-fetching loop involves calling `mysql_stmt_fetch()` until it returns a non-zero value. After each fetch, the variables associated with the parameter structures contain the column values for the current row.

Once all the rows have been fetched, a call to `mysql_stmt_free_result()` releases any memory associated with the result set.

At this point, `select_rows()` returns to the caller, which invokes `mysql_stmt_close()` to dispose of the prepared statement handler.

The preceding discussion provides a broad overview of the prepared statement interface and some of its key functions. The client library includes several other related functions; for more information, consult Appendix G (online).

## 8 Writing MySQL Programs Using Perl DBI

This chapter describes how to use the Perl DBI interface for MySQL. It does not discuss DBI philosophy or architecture. For information about those aspects of DBI (particularly in comparison with the C and PHP APIs), see Chapter 6, “Introduction to MySQL Programming.”

The examples discussed here draw on our sample database, sampdb, using the tables created for the grade-keeping project and for the Historical League in Chapter 1, “Getting Started with MySQL.” To get the most from this chapter, it's best if you know something about Perl. If you don't, you may be able to get along with purely your own scripts simply by copying the sample code you see here, but you will probably find a good Perl book a worthwhile investment. One such book is Programming Perl, Third Edition by Wall, Christiansen, and Orwant (O’Reilly, 2000).

DBI is currently at version 1.601, although most of the discussion here applies to earlier versions as well. DBI requires at least Perl 5.6.0 (and 5.6.1 is preferred to 5.6.0). You must also have the DBD::mysql Perl module installed, as well as the MySQL C client library and header files. If you plan to write Web-based DBI scripts in the manner discussed here, you should also obtain the CGL.pm module. In this chapter, CGL.pm is used in conjunction with the Apache Web server. If you need to obtain any of these packages, see Appendix A, “Obtaining and Installing Software.” Instructions for obtaining the example scripts developed in this chapter are also given in that appendix. They are part of the sampdb distribution, which you can download to avoid retyping the scripts yourself. The scripts used in this chapter are located under the perlapi directory of the distribution.

For the most part, this chapter describes Perl DBI methods and variables only as they are needed for the discussion here. For a more comprehensive listing of methods and variables, see Appendix H, “Perl DBI API Reference” (online). You can use that appendix as a reference for further background on any part of DBI that you're trying to use. Online documentation is available by running the following commands:

```
perldoc DBI
```

```
% perldoc DBI::FAQ
% perldoc DBD::mysql
```

At the database driver (DBD) level, the driver for MySQL is built on top of the MySQL C client library, and therefore shares some of its characteristics. See Chapter 7, “Writing MySQL Programs Using C,” for more information about the client library.

### 8.1 Perl Script Characteristics

Perl scripts are text files, so you can create them using any text editor. All Perl scripts in this chapter follow the Unix convention that they begin with a #! (shebang) line that specifies the pathname of the program to use for executing the script. The line I use is as follows:

```
#!/usr/bin/perl
```

On Unix, you’ll need to modify the #! line if the pathname to Perl is different on your system, such as /usr/local/bin/perl5 or /opt/bin/perl. Otherwise, Perl scripts won’t run properly on your system.

You can invoke a Perl script myscript.pl as follows on any system to run it:

```
% perl myscript.pl
```

However, you may also be able to execute the script without naming the perl program explicitly. On Unix, do this by changing the file mode with chmod to make the script executable:

```
% chmod +x myscript.pl
```

Then you can run the script just by typing its name:

```
% ./myscript.pl
```

That is the script invocation style that will be used for examples shown in this chapter. The leading “./” should be used if the script is located in your current directory (“.”) and your shell does not have the current directory in its search path. Otherwise, you can omit the “./” from the command name:

### 8.2 Perl DBI Overview

This section provides background information for DBI that you’ll need for writing your own scripts and for understanding scripts written by others. If you’re already familiar with DBI, you may want to skip directly to Section 8.3, “Putting DBI to Work.”

#### 8.2.1 DBI Data Types

In some ways, using the Perl DBI API is similar to using the C client library described in Chapter 7. When you use the C client library, you call functions and access MySQL-related data primarily by means of pointers to structures or to arrays. When you use the DBI API, you also call functions and use pointers to structures, except that functions are called “methods,” pointers are called “references,” pointer variables are called “handles,” and the structures that handles point to are called “objects.”

DBI uses several kinds of handles. These tend to be referred to in DBI documentation by the conventional names shown in Table 8.1. The way you use these handles will become clear as we go along. Several conventional names for non-handle variables are used as well (see Table 8.2). This chapter doesn’t actually use every one of these variable names, but it’s useful to know them when you read DBI scripts written by other people.

| Name | Meaning |
| :--- | :--- |
| $dbh | A handle to a database object |
| $sth | A handle to a statement (query) object |
| $fh | A handle to an open file |
| $h | A “generic” handle; the meaning depends on context |

*Table 8.1 Conventional Perl DBI Handle Variable Names*

| Name | Meaning |
| :--- | :--- |
| $rc | The return code from operations that return true or false |
| $rv | The return value from operations that return an integer |
| $rows | The return value from operations that return a row count |
| @ary | An array (list) representing a row of values returned by a query |

*Table 8.2 Conventional Perl DBI Non-Handle Variable Names*

#### 8.2.2 A Simple DBI Script

Let’s start with a simple script, *dump_members.pl*, that illustrates several standard concepts in DBI programming, such as connecting to and disconnecting from the MySQL server, issuing SQL statements, and retrieving data. This script produces output consisting of the

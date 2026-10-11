Now you don't need to edit the script each time you run it. Just tell it what you're looking for on the command line:

```
```
% ./interests.sh depression
% ./interests.sh Jefferson
```
```

The `interests.sh` script is located in the *misc* directory of the `sampdb` distribution. An equivalent Windows batch file, *interests.bat*, is provided there as well.

# Note

I suggest that you not install scripts like these publicly because they do not perform any safety checks on the arguments and thus are subject to SQL injection attacks. Suppose someone invokes the script like this:

```
```bash
% ./interests.sh "Jefferson";"DROP DATABASE sampdb;"
```
```

The effect of this is to “inject” a *DROP DATABASE* statement into the statement to the *mysql* input in such a way that it actually executes.

# 1.6 Where to Now?

You know quite a bit about using MySQL now. You can set up a database and create tables. You can put rows into those tables, retrieve them in various ways, change them, or delete them. But the tutorial in this chapter only scratches the surface, and there’s still a lot to know about MySQL. You can see this by considering the current state of our *sampdb* database. We’ve created it and its tables and populated them with some initial data. During the process we’ve seen how to write some of the queries needed for answering questions about the information in the database. But much remains to be done. For example, we have no convenient interactive way to enter new score rows for the grade-keeping project or new member entries for the Historical League directory. We have no convenient way to edit existing rows. And we still can’t generate the printed or online forms of the League directory. These tasks and others are revisited in the upcoming chapters, particularly in Chapter 8, “Writing MySQL Programs Using Perl DBI,” and Chapter 9, “Writing MySQL Programs Using PHP”.

Where you go next in this book depends on what you’re interested in. If you want to see how to finish the job we’ve started with our Historical League and grade-keeping projects, Part II covers how to write MySQL-based programs. If you’re going to serve as the MySQL administrator for your site, Part III of this book deals with administrative tasks. However, I recommend acquiring additional general background in using MySQL first, by reading the remaining chapters in Part I. These chapters provide further information on the syntax and use of SQL statements, discuss how MySQL handles data, and show how to make your queries run faster. A good grounding in these topics will stand you in good stead no matter the context in which you use MySQL—whether you’re running *mysql*, writing your own programs, or acting as a database administrator.

Listing 29.7 shows the new script.

```php
<?php
    include("DB.php");
    $dsn = "mysql://ubuntu:alm65z@10.0.0.1/dentists";
    $conn = DB::connect($dsn);

    if (DB::isError($conn)) {
        echo $conn->getMessage() . "\n";
    } else {
        echo "Connected successfully!\n";
    }

    $result = $conn->query("SELECT ID, Name FROM patients;");

    while ($result->fetchInto($row, DB_FETCHMODE_ASSOC)) {
        extract($row, EXTR_PREFIX_ALL, 'pat');
        echo "$pat_ID is $pat_Name\n";
    }
?>
```

The first half is identical to the previous script, with all the new action happening if we get a successful connection.

Going along with the saying “never leave to PHP what you can clean up yourself,” the current script has problems. We do not clean up the query result, and we do not close the database connection. If this code were being used in a longer script that ran for several minutes, this would be a huge waste of resources. Fortunately, we can free up the memory associated with these two by calling `$result->free()` and `$conn->disconnect()`. If we add those two function calls to the end of the script, it will be complete.

### Reference

- http://www.phpbuilder.net—A large PHP scripts and tutorials site where you can learn new techniques and also chat with other PHP developers.
- http://www.zend.com—The home page of a company founded by two of the key developers of PHP. Zend develops and sells proprietary software, including a powerful IDE and a code cache, to aid PHP developers.
- http://pear.php.net/—The home of the PEAR project contains a large collection of software you can download and try, and it has thorough documentation for it all.
- http://www.phparch.com/—There are quite a few good PHP magazines around, but *PHP Architect* probably leads the way. It posts some of its articles online for free, and its forums are good, too.

Quality books on PHP abound, and you are certainly spoiled for choice. For beginning developers, the best available is *PHP and MySQL Web Development* (Sams Publishing), ISBN 0-672-32672-8. For a concise, to-the-point book covering all aspects of PHP, check out *PHP in a Nutshell* (O'Reilly). Finally, for advanced developers, you can consult *Advanced PHP Programming* (Sams Publishing), ISBN 0-672-32561-6.

## CHAPTER 30 C/C++ Programming Tools for Ubuntu

Learning how to use a computer language such as C or C++ can be more complex and difficult than learning shell scripting. You must learn to think in terms of machine resources and the way actions are accomplished within the computer, taking into account the operating system, language syntax, and assorted development tools, rather than thinking in terms of user-oriented commands.

Of course, the main benefit of learning C or C++ is that Linux and nearly all its related software is open source—if a program doesn’t work the way you want it to, you can change it! You can also find a lot of “hidden” documentation in programmer comments inside the source to nearly all Linux programs.

This chapter focuses on C- and C++-related tools for Linux, such as the GNU C Compiler Collection (GCC) system, and prototyping environments for GNOME and the K Desktop Environment (KDE). The information presented here introduces some of the commands used to compile C and C++ programs, along with information about related programming tools.

### IN THIS CHAPTER

- Programming in C with Linux
- Elements of the C/C++ Language
- Using the C Programming Project Management Tools Provided with Ubuntu
- Using the GNU C Compiler
- A Simple C Program
- Graphical Development Tools
- Reference

### Programming in C with Linux

C is the programming language most frequently associated with UNIX-like operating systems such as Linux or BSD. Since the 1970s, the bulk of the UNIX operating system and its applications have been written in C. Because the C language doesn’t directly rely on any specific hardware architecture, UNIX was one of the first portable operating systems. In other words, the majority of the code that makes up UNIX does not know and doesn’t care which

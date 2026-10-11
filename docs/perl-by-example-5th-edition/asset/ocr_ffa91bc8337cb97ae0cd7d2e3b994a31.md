# EXPLANATION (CONTINUED)

+   5. The reference $passwd, when printed, shows that it contains the address of a typeglob (alias).

+   6, 7. The expression in the while loop causes a line to be read from the /etc/passwd file and assigned to the $ _variable. The line is printed to the screen. The loop will continue until all the lines have been read and printed.

+   9. The seek function resets the read pointer for this file back to the beginning of the file.

# 12.2 What You Should Know

+   1. What is the difference between a symbolic and a hard reference?

+   2. What is a typeglob?

+   3. How do you create a reference to a hash?

+   4. How can you tell an anonymous array from a named array?

+   5. How do you dereference $ref where $ref = { 'Name' => "John" }, ?
+   6. How do you dereference $p where $p = \$x;?

+   7. What is meant by a nested hash?

+   8. How do you create a two-dimensional array?

+   9. What is the advantage of passing by reference?

+   10. What is the purpose of the ref function?

+   11. How would you create an array of hashes using a reference?

# 12.3 What's Next?

Next, we will expand your horizons and go from the "introverted" Perl programmer to the "extroverted" programmer. Instead of writing stand-alone scripts, you will start learning how to use the libraries and modules already provided by Perl. You will explore CPAN and learn how to download and use modules that other programmers have written.

You will understand packages and namespaces and how to export and import symbols, how to use the standard Perl library, and how to create your own. You will learn how to create procedural modules and how to store and use them.
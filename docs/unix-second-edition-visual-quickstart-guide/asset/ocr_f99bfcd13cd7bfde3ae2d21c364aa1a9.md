# Naming Directories (and Files)

As you start creating directories (and files), keep in mind the following guidelines:

+   - Directories and files must have unique names. For example, you cannot name a directory Golf and a file Golf. You can, however, have a directory called Golf and a file called golf. The difference in capitalization makes each name unique. By the way, directories are often named with an initial cap, and filenames are often all lowercase.

Directory and filenames should not include the following characters: angle brackets (< >), braces ({ }), brackets ([ ]), parentheses ( () ), double quotes (",), single quotes ('), asterisks (*), question marks (?), pipe symbols (|), slashes (/ \), carets (^), exclamation points (!), pound signs (#), dollar signs ($), ampersands (&), and tildes (~).

Different shells handle special characters differently, and some will have no problems at all with these characters. Generally, though, they’re more trouble than they’re worth.

+   - Generally, avoid names that include spaces and hyphens (-). You can use these, but they’re often more trouble than they’re worth—that is, some programs don’t deal with them correctly, so you have to use odd workarounds. Instead, stick to periods (.) and underscores (_) to separate words, characters, or numbers.

+   - Use names that describe the directory’s or file’s contents so you easily remember them.

# To create a directory:

+   1. ls
+   Start by listing existing directories to make sure that the planned name doesn’t conflict with an existing directory or filename.

+   2. mkdir Newdirectory
+   Type the mkdir command to make a new directory; in this case, it’s called Newdirectory. Refer to the sidebar Naming Directories (and Files) for guidelines.

+   3. ls -l
+   Now you can use ls -l (the -l flag specifies a long format) to look at the listing for your new directory (Code Listing 2.1). The d at the far left of the listing for Newdirectory indicates that it’s a directory and not a file. Of course, after you trust Unix to do as you say, you can skip this verification step.

# Tips

+   - If you attempt to create a directory with a file or directory name that already exists, Unix will not overwrite the existing directory. Instead, you’ll be told that a file by that name already exists. Try again with a different name.

+   - Create several directories and subdirectories at once with the -p flag. For example, if you want to create a new subdirectory called Projects with a subdirectory called Cooking in that and a subdirectory called Desserts in that, you can use mkdir -p Projects/Cooking/Desserts and get it all done at once. Without the -p flag, you have to create Projects, Cooking, then Desserts in order, which is a longer recipe to make the same tree structure.
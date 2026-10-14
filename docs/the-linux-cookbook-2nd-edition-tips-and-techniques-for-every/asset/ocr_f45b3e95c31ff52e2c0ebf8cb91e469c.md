+   - \n Outputs a newline character.
+   - \r Outputs a carriage return.
+   - \t Outputs a horizontal tab character.
+   - \\ Outputs a backslash character.
+   - %% Outputs a percent sign character.
+   - %b Outputs file's size, rounded up in 512-byte blocks.
+   - %f Outputs base file name.
+   - %h Outputs the leading directories of file's name.
+   - %k Outputs file's size, rounded up in 1 K blocks.
+   - %s Outputs file's size in bytes.

# 7.3 Finding Directories

To find directories that have a particular name, use find with the -name option, giving the glob expression to match, and also giving the -type option with the d argument, which specifies that directories are the only files that should be searched for.

⇒ Here are two ways to use this.

+   - To find all of the directories in your home directory tree with a name of audio, type:
+     $ find ~ -name audio -type d RET
+   - To find all of the directories in your home directory tree with the string "audio" anywhere in their names, type:
+     $ find ~ -name *audio* -type d RET

# 7.4 Finding Files in Directory Listings

The following recipes show how to find the largest and smallest files and directories in a given directory or tree by listing them by size. They also show how to find the number of files in a given directory.

# 7.4.1 Finding the Largest Files in a Directory

To find the largest files in a given directory, list its contents using ls with the -S option, which sorts files in descending order by their size (normally, ls
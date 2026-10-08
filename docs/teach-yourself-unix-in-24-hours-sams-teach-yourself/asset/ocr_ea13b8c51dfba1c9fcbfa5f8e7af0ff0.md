# Searching for Information and Files

The find command is a powerful command in UNIX. It helps you find files by owner, filename, and other attributes. The most awkward part of the command is the required elements of the -exec option, and that's where the xargs command helps immensely.

# Task 19.2: Using find with xargs

You can use find to search for files, and you can use grep to search within files, but what if you want to search a combination? That's where xargs is helpful.

+   * Few days ago

The output is interesting, but it doesn't contain any filenames!
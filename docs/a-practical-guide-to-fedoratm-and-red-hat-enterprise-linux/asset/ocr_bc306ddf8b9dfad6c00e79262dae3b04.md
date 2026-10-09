```
$ find / -name memo55 > memo.out &
[1] 18236

$ bigjob &
[2] 18237

$ jobs
[1]- Running      find / -name memo55 > memo.out &
[2]+ Running      bigjob &
$ kill %1
$ RETURN
[1]- Terminated   find / -name memo55 > memo.out
$
```

# ## FILENAME GENERATION/Pathname Expansion

Wildcards, globbing  When you specify an abbreviated filename that contains *special characters*, also called *metacharacters*, the shell can generate filenames that match the names of existing files. These special characters are also referred to as *wildcards* because they act much as the jokers do in a deck of cards. When one of these characters appears in an argument on the command line, the shell expands that argument in sorted order into a list of filenames and passes the list to the program called by the command line. Filenames that contain these special characters are called *ambiguous file references* because they do not refer to one specific file. The process the shell performs on these filenames is called *pathname expansion* or *globbing*.

Ambiguous file references can quickly refer to a group of files with similar names, saving the effort of typing the names individually. They can also help find a file whose name you do not remember in its entirety. If no filename matches the ambiguous file reference, the shell generally passes the unexpanded reference—special characters and all—to the command. See “Brace Expansion” on page 405 for a technique that generates strings that do not necessarily match filenames.

# ### The ? Special Character

The question mark (?) is a special character that causes the shell to generate filenames. It matches any single character in the name of an existing file. The following command uses this special character in an argument to the `lpr` utility:

```
$ lpr memo?
```

The shell expands the **memo?** argument and generates a list of files in the working directory that have names composed of **memo** followed by any single character. The shell then passes this list to `lpr`. The `lpr` utility never “knows” the shell generated the filenames it was called with. If no filename matches the ambiguous file reference, the shell passes the string itself (**memo?**) to `lpr` or, if it is set up to do so, passes a null string (see `nullob` on page 402).
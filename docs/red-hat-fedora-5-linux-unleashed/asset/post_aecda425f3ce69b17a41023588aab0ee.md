
## Finding Files by Searching with find

The find command is one of the darkest and least understood areas of Linux, but it is also one of the most powerful. Admittedly, the find command does not help itself by using X-style parameters. The UNIX standard is -c, -s, and so on, whereas the GNU standard is --dosomething, --mooby, and so forth. X-style parameters merge the two by having words preceded by only one dash.

However, the biggest problem with find is that it has more options than most people can remember—it truly is capable of doing most things you could want. The most basic usage is this:

```
find -name "*.txt"
```

That query searches the current directory and all subdirectories for files that end in .txt. The previous search finds files ending in .txt but not .TXT, .Txt, or other case variations. To search without case sensitivity, use -iname instead of -name. You can optionally specify where the search should start before the -name parameter, like this:

```
find /home -name "*.txt"
```

Another useful test is -size, which lets you specify how big the files should be to match. You can specify your size in kilobytes and optionally also use + or - to specify greater than or less than. For example:

```
find /home -name "*.txt" -size 100k
find /home -name "*.txt" -size +100k
find /home -name "*.txt" -size -100k
```

The first brings up files of exactly 100KB, the second only files greater than 100KB, and the last only files less than 100KB.

Moving on, the -user option enables you to specify the user that owns the files you are looking for. So, to search for all files in /home that end with .txt, are under 100KB, and are owned by user paul, you would use this:

```
find /home -name "*.txt" -size -100k -user paul
```

You can flip any of the conditions by specifying -not before them. For example, you can add a -not before -user paul to find matching files owned by everyone but paul:

```
find /home -name "*.txt" -size -100k -not -user paul
```

You can add as many -not parameters as you need, even using -not -not to cancel each other out! Yes, that is pointless. I keep in mind, though, that -not -size -100k is essentially equivalent to -size !100k, with the exception that the former will match files of exactly 100Kb whereas the latter will not.

You can use -perm to specify which permissions a file should have for it to be matched. This is tricky, so read carefully. The permissions are specified in the same way as with the find command: u for user, g for group, o for others, r for read, w for write, and x for execute. However, before you give the permissions, you need to specify a plus, a minus, or a blank space. If you specify neither a plus nor a minus, the files must exactly match the mode you give. If you specify +, the files must match all the modes you specify. If you specify - the files must match any the modes you specify. Confused yet?

The confusion can be cleared up with some examples. This next command finds all files that have permission u=r (readable for other users). Notice that if you remove the -name parameter, it is equivalent to * because all filenames are matched.

```
find /home -perm -0=r
```

Any files that have 0=r set are returned from that query. Those files also might have u=rw and w/r+ permissions, but as long as they have 0=r, they will match. This next query matches all files that have o=rw set:

```
find /home -perm o=rw
```

However, that query does not match files that are o=r or o=w. To be matched, a file must be readable and writable by other users. If you want to match readable or writable (or both), you need to use +, like this:

```
find /home -perm +0=rw
```

Similarly, this next query matches files that are only readable by user, group, and others:

```
find /home -perm -ugo=r
```

Whereas this query matches files as long as they are readable by the user, or by the group, or by others, or by any combination of the three:

```
find /home -perm +ugo=r
```

If you use neither + nor -, you are specifying the exact permissions to search for. For example, the next query searches for files that are readable by user, group, and others but not writable or executable by anyone:

```
find /home -perm ugo=r
```

You can be as specific as you need to be with the permissions. For example, this query finds all files that are readable for the user, group, and others and writable by the user:

```
find /home -perm ugo=r,u=w
```

To find files that are not readable by others, use the `-not` condition, like this:

```
find /home -not -perm +0=r
```

Now, on to the most advanced aspect of the find command: the `-exec` parameter. This enables you to execute an external program each time a match is made, passing in the name of the matched file wherever you want it. This has very specific syntax: Your command and its parameters should follow immediately after `-exec`, terminated by `;`. You can insert the filename match at any point using `{}`, an opening and a closing brace side by side.

So, you can match all text files on the entire system (that is, searching recursively from `/` rather than from `/home` as in our previous examples) over 10KB, owned by paul, that are not readable by other users, and then use chmod to enable reading, like this:

```
find / -name "*.txt" -size +10k -user paul -not -perm +0=r -exec chmod 0+r {} ;
```

When you type your own `-exec` parameters, be sure to include a space before `;`. Otherwise, you might see an error such as missing argument to `-exec`.

Do you see now why some people think the find command is scary? Many people learn just enough about find to be able to use it in a very basic way, but hopefully you will see how much it can do if you give it a chance.

## Searching for a String in Input with grep

The grep command, like find, is an incredibly powerful search tool in the right hands. Unlike find, though, grep processes any text, whether in files, or just in standard input.

The basic usage of grep is this:

```
grep "some text" *
```

That query searches all files in the current directory (but not subdirectories) for the string `some text` and prints matching lines along with the name of the file. To enable recursive searching in subdirectories, use the `-r` parameter, like this:

```
grep -r "some text" *
```

Each time a string is matched within a file, the filename and the match are printed. If a file contains multiple matches, each of the matches is printed. You can alter this behavior with the `-l` parameter (lowercase *L*), which forces grep to print the name of each file that contains at least one match, without printing the matching text. If a file contains more than one match, it is still printed only once. Alternatively, the `-c` parameter prints each filename that was searched and includes the number of matches at the end, even if there were no matches.

You have a lot of control when specifying the pattern to search for. You can, as previously, specify a simple string like `some text`, or you can invert that search by specifying the `-v` parameter. For example, this returns all the lines of the file myfile.txt that do not contain the word hello:

```
grep -v 'hello' myfile.txt
```

You can also use regular expressions for your search term. For example, you can search myfile.txt for all references to cat, sat, or mat with this command:

```
grep '[cns]at' myfile.txt
```

Adding the -i parameter to that removes case sensitivity, matching Cat, CAT, MaT, and so on:

```
grep -i [cns]at myfile.txt
```

The output can also be controlled to some extent with the -n and -color parameters. The first tells grep to print the line number for each match, which is where it appears in the source file. The -color parameter tells grep to color the search terms in the output, which helps them stand out when among all the other text on the line. You choose which color you want using the GREP_COLOR environment variable: export GREP_COLOR=36 gives you cyan, and export GREP_COLOR=32 gives you lime green.

This next example uses these two parameters to number and color all matches to the previous command:

```
grep -in -color [cns]at myfile.txt
```

Later you will see how important grep is for piping with other commands.

## Paging Through Output with less

The less command enables you to view large amounts of text in a more convenient way than the cat command. For example, your /etc/passwd file is probably more than a screen long, so if you run cat /etc/passwd, you are not able to see what the lines at the top were. Using less /etc/passwd enables you to use the cursor keys to scroll up and down the output freely. Type q to quit and return to the shell.

On the surface, less sounds like a very easy command; however, it has the infamy of being one of the few Linux commands that have a parameter for every letter of the alphabet. That is, -a does something, -b does something else, -c, -d, -0, ..., -x, -y, -z—they all do things, with some letters even differentiating between upper- and lowercase. Furthermore, these are only the parameters used to invoke less. After you are viewing your text, even more commands are available to you. Make no mistake—less is a complex beast to master.

Input to less can be divided into two categories: what you type before running less and what you type while running it. The former category is easy, so we will start there.

We have already discussed how many parameters less is capable of taking, but they can be distilled down to three that are very useful: -M, -N, and +. Adding -M (this is different

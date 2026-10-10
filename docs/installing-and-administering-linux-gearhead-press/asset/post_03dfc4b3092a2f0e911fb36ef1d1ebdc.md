
## grep Syntax and Metacharacters

other syntax that would work? The next section should help answer these questions.

Meanwhile, we know that `grep` can search in specified files for specified regular expressions, which can include text patterns and metacharacters. In Example 8.12, we saw a metacharacter used with `grep` to search for every file that begins with the character R (`grep ^R`).

We also mentioned how the metacharacters used with `grep` might or might not mean the same as the metacharacters used by the shell. Take a look at Table 8.2. Can you see how `grep` metacharacters might cause confusion as well as unreliable and undesirable results? For this reason, we recommend that you surround `grep` expressions containing metacharacters with single quotes. Double quotes might be acceptable in some situations, but you will get the most reliable performance by using single quotes.

The following are three examples of `grep` metacharacter usage:

- `[a-f]` means any *one* character from the range a through f
- `^a` means any lines beginning with a
- `z$` means any lines ending with z

### Table 8.2 Metacharacters in grep and the Shell

| METACHARACTER | MEANING IN GREP | MEANING IN THE SHELL |
| :--- | :--- | :--- |
| `.` | Match any character | If followed by *filename*, execute *filename* |
| `*` | Match zero or more preceding | Match zero or more |
| `^` | Match beginning of line | Bourne shell pipe symbol |
| `$` | Match end of line | Variable (generally, the user prompt) |
| `\` | Escape the character following | Escape the character following |
| `[ ]` | Match one from this set or range | Match from this set or range |
| `{ }` | Match this range of instances | |
| `+` | Match one or more preceding | |
| `?` | Match zero or one preceding | Match zero or one |

## grep Options

### Table 8.3 Selected grep Options

| OPTION | DESCRIPTION |
| :--- | :--- |
| -v | Print the lines that do not match the specified pattern. |
| -c | Print only a count of the matching lines. |
| -l | Print only the names of the files with matching lines. |
| -n | Print matching lines and their line numbers in the respective files. |
| -i | Ignore the case of the letters when making comparisons. |
| -w | Perform a whole word search. |

Table 8.3 presents some of the more common grep options. All of these options are used in Example 8.7, where we present the poem titled “Fleas.”

### Example 8.13 Applying grep to “Fleas”

Sancho, inspired by Don Quixote’s poetic prowess (questionable though these examples might be), has written this poem and has saved it in his home directory. After you read it, you will probably wonder why:

```bash
$ cat fleas<Enter>
Fleas

You bite those bugs and give a yelp
You scratch anon, sometimes it helps
You chase your tail, you drag your butt
Oh, but you’re suffering, my dear old mutt

I rub your belly and your back
To stem that burning itch attack
I scratch your ears, and scratch your head,
But those cursed fleas fill me with dread!

They are entrenched, they won’t go ‘way
Do what you will, they’re here to stay
You long for the “powders”, you yearn for the “collars”
Perhaps a mud pit in which to waller?

But, you know what? You see, old friend?
To rout those fleas, reach your happy end?
There is just one way to escape their wrath,
Yes, amigo, you must have a bash!
```

It might not be good, but it was fast. And besides, Sancho can now use “Fleas” to practice his **grep** skills. For example:

To search for all lines containing the word you, in both upper-case and lower-case variants of *y*:

```bash
$ grep -i you fleas<Enter>
```

To perform the search by using only metacharacters:

```bash
$ grep '[Yy]ou' fleas<Enter>
```

To perform the search using the **egrep** command (discussed later):

```bash
$ egrep 'you|You' fleas<Enter>
```

To search for all lines containing at least one character but to return only a line count of those lines:

```bash
$ grep -c '.' fleas<Enter>
```

To search for all files that contain the word you, whether in lowercase or uppercase:

```bash
$ grep -lI you *<Enter>
```

This example illustrates how you can combine options. Note that when subdirectories are encountered during the search, the following message appears: *grep: directoryname: Is a directory*.

To search for all lines that do not contain the word you, lowercase or not:

```bash
$ grep -vI you fleas<Enter>
```

This example illustrates the combination of options, but the displayed output includes all blank lines, as well.

To search for all lines in the *fleas* file, number them and send the output to the *fleas.num* file:

```bash
$ grep -n '.*' fleas > fleas.num<Enter>
```

Note how this example uses `grep` options and metacharacters and then uses redirection to send the output to the `fleas.num` file. To view the results, type `$ cat fleas.num<Enter>`.

To search for all occurrences of the whole word *you* in the poem:

```bash
$ grep -w 'you' fleas<Enter>
```

Note that the words *your* and *You're* are also in the poem. If *whole* word had not been specified by the `-w` option, the occurrence of those words would also have been displayed.

## More Examples of `grep` with Metacharacters

In this section, we provide more examples of `grep` in action to help ensure that you understand how to use this powerful command. These examples are representative of the tasks that administrators typically encounter.

Select all lines (blank lines and non-blank lines) from the `RFL_Tell` file:

```bash
$ grep '.*' RFL_Tell
```

When you ask for this type of output, you are probably assuming that the file has blank lines. Single quotes surround the regular expression, because without them, the shell will interfere with `grep`'s execution by imposing the shell's interpretation on the asterisk.

Select only the blank lines in `RFL_Tell`:

```bash
$ grep '^$' RFL_Tell<Enter>
```

Select all the lines in the `RFL_Tell` file that begin with the letter *M* and end with the number *7*, with any number of characters in between:

```bash
$ grep 'M.*7' RFL_Tell2
```

This request asks for lines that have a particular pattern within a file.

Select all the lines in the RFI_Tel2 file that contain a plus sign (+):

```bash
$ grep '\+' RFI_Tel2<Enter>
```

## Other grep Commands: egrep and fgrep

We have already discussed how `grep` can be extremely useful when you have to extract text from a data stream, such as a text file. (Yes, `grep` can be used for other types of data streams, but this usage is not covered here.) The command’s functionality or performance for extracting text in particular situations is further enhanced by the `egrep` and `fgrep` commands.

### egrep: Searching for Alternates

The `grep` command itself cannot be used for the type of search request where you want to find all strings containing one item or another. The extended `grep` command, `egrep`, enables OR searches by letting you put a pipe symbol ( | ) between your specified alternate search expressions, as shown in Example 8.14. The `egrep` command also works with `grep`’s metacharacters and options. The `egrep` command is a little slower than a normal `grep`, mostly because it executes more than one `grep` process.

#### Example 8.14 egrep

Lady Dulcinea wants to know how many 800 numbers the RFI has to pay for. She also wants to know whether RFI has any 900 numbers:

```bash
$ egrep '800|900' RFI_Tel3<Enter>
Emergencies - +34 91 800 09 87
Human Resources - +34 91 900 55 87
```

Although she is not sure why the human resources department has a 900 number, she is satisfied that the emergencies number is an 800 number.

### Faster Searching for Fixed Strings with fgrep

The `fgrep` command is similar to `grep` but does not provide the regular expression capability. Instead, you are limited to searching for fixed text strings, as shown in Example 8.15. This command enables you to use the same options as `grep` with the exception of any that deal with metacharacters or other aspects of regular expressions. Because `fgrep` does not require the extra translation, it requires fewer processor resources.

#### Example 8.15 fgrep

At one point, Perez needs to call Lady Dulcinea. He has saved his copy of the `RFL_Tel2` file in the `admin` subdirectory of his home directory. Here is how he can quickly access her phone number:

```bash
$ fgrep 'Dulcinea' ./admin/RFL_Tel2<Enter>
A. Lorenzo (Lady Dulcinea) – Tel: +34 91 555 01 23
```

## Sorting Output: The `sort` Command

You use the `sort` command to sort the output of a file or the `stdout` of a process before it is sent to the screen or wherever you want it to go. Thus, `sort` helps to ensure that the output is in an acceptable order or that it is presented how you want. It works by reading `stdin` (which might be the `stdout` of another process), processing the data, and sending it to `stdout` or wherever you designate. The `sort` command’s syntax is as follows:

```bash
$ sort [-t delimiter] [+field[,column]] [options] [file(s)]<Enter>
```

The processes of the `sort` command use dictionary or ASCII ordering by default, which you can override with options—several of which appear in Table 8.4. For information on `sort`’s many other options, consult your information sources.

### Example 8.16 `sort` with Spaces and Tabs

In Example 8.16, Juana first uses the `cat` command to display the contents of the `Innfile` file. Then, by adding `+1` in the `+field` position (see the syntax), she can sort the contents of the file according to the second field of each line. Look at how tabs have priority over spaces:

```bash
$ cat Innfile<Enter>
Filename: /home/gutieju/a/admin/Innfile
file[Space]bar>Inn No. 4
file[Space]bar>Inn No. 7
file[Tab]S>Inn No. 8
file[Tab]S>Inn No. 1
file[Space]bar>Inn No. 8
```

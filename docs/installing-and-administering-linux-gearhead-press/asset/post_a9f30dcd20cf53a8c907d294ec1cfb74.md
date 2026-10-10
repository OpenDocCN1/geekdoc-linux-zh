
This command uses most of the same options as `gzip` (see your information sources). For example, we will use the `-v` option with `gunzip` in Example 9.18.

## Example 9.18 gunzip

Once Don Quixote's niece receives the telephone list (filename: `RFI_Phones`; see Example 9.16) from Juana at RFI, she uncompresses it so that she can read and print it. Here is how she uses `gunzip` to do so:

```bash
$ gunzip -v RFI_Phones.gz <Enter>
RFI_Phones.gz : 50.0% - replaced with RFI_Phones
```

> **NOTE** The `zip` and `unzip` commands might also be available with your Linux distribution. You might prefer to use them instead to compress and uncompress files.

## Displaying Nonprintable Characters: The cat Command Options

Here, we discuss three options that you can use in conjunction with the now-familiar `cat` command (refer to Chapter 5 for our original discussion of `cat`) to determine the following:

- Whether invisible or otherwise unprintable characters exist in text files or filenames (that is, directories)
- The nature of the spaces in your text files

The second determination might be important because of unexpected `diff` command output or problems with output from the `sort` command. When someone is composing a document or specifying a file or directory name, there are key sequences that can be entered accidentally that will cause unexpected results in documents or file or directory names. Take a look at Table 9.4, for instance, for a listing of some odd key sequences that are sometimes entered when you use the `vi` text editor. The table also shows what the key sequences will look like during the creation of the file in `vi`, when the same file is `cat`'d at the command line and also when it is `cat`'d with the `cat`'s `-etv` options.

The fact that no characters will show up with `cat` makes these what we call nonprintable. Thus, it might not be possible to resolve these issues or problems based on the typical viewing of directory or file contents. Using `cat` with the options discussed here might help you determine how at least some of the file contents or names were created and therefore might help you figure out how to read or manipulate them later. The syntax is the same as for `cat` in other circumstances, of course:

```bash
$ cat [-options] [file(s)] <Enter>
```

The options used in Example 9.19 are defined in Table 9.5.

| OPTION | DESCRIPTION |
|---|---|
| -e | Display `$` to indicate the end-of-line key; that is, Enter or Return. |
| -t | Display `^I` to indicate a Tab used as a space. |
| -v | Display `^G` to indicate the otherwise invisible Ctrl-G key sequence. |

## Example 9.19 cat for Displaying Nonprintable Characters

Juana checks her “Requests” files (`Req-K1`, `Req-K2`, and `Req-K3`) every morning. In late July, she reads this garbled message that originates from Don Quixote:

```bash
$ cat Req-K1 <Enter>
Date: July @, 2001
   Subject: Request for Advance Funds for August Trip
Status: Urgent
Deadline: ASA
From: Quixote de

       a Mancha

need 100 Euros as an advance. For the August trip.
Sancho will requisition his own funds, etc.
zizante needs new equipment [shoes, blanket] and provisions.
Will likely leave  August     at }:3] HRS
lus, can someone make an appointment for me at Toledo spa?
now the manager?
hope this meets with your approval and
Very much appreciate your cooperation. t to . ady Dulcinea’s, too.
Signed, Q de
         a M
```

She calls the Don and discusses the situation. Once everything is satisfactory, she calls Freston, who suggests that she do the following with the same message:

```bash
$ cat -stv Req-K1 <Enter>
Date: July @\, 2001$
^\Subject: Request for Advance Funds for August Trip$
Status: Urgent$
Deadline: ASA^P$
From: Quixote de ^La Mancha$
$
^"I need i\"100 Euros as an advance. For the August trip.$
Sancho will requisition his own funds, etc.$
zizante needs new equipment [shoes, blanket] and provisions.$
Will likely leave ^"August     ^ _ at }:3] HRS$
^"Plus, can someone make an appointment for me at Toledo spa?
^Know the manager?
^"I hope this meets with your approval ^"I and ^lady DulM^-inea’s,
too.$
^{[Avery much appreM^-iate your M^-operation. t to .$
Signed, Q de ^La M$
```

It helped Juana decipher *some* of the key sequences but not all. To determine all of them, Juana would have to see the original document in Don Quixote's files. Again, the options used in Example 9.19 were defined previously in Table 9.5.

## Use cat in a Pipe Sequence for ? in Filenames

When executing listings of directory contents, you might sometimes encounter filenames containing a question mark (`?`). The creator of such a filename might have intentionally inserted the question mark, but this symbol can also indicate the presence of other characters that cannot be readily interpreted by the shell. When dealing with these odd filenames in directories, you can use `cat` as the second process in a piped set of commands.

For example, a typical `ls` command might reveal the following:

```bash
testfile1    te?stfile2
```

Now, we try `cat`:

```bash
$ ls | cat -vt
```

The output might look something like the following:

```text
testfile1
te^Gatfile2
```

This example shows a Ctrl-G (that is, `^G`) in the middle of what otherwise would have been called `testfile2`. How do you correct the filename? You could simply rename the file as follows:

```bash
$ mv te^Gatfile2 testfile2
```

> **NOTE** You cannot enter `te^Gatfile2` at the command line. If you try, you will hear an error “beep” from Linux.

If the correction strategy fails, you can try another technique. First, you need to obtain the inode number of the file with `ls -i`. (Remember that the filename displayed is probably `te?stfile2` because a simple `ls -i` does not display the hidden Ctrl-G characters.)

Assume that the inode number for the file is 1311. Now, enter the following:

```bash
$ find . -inum 1311 -exec mv {} testfile2 <Enter>
```

> **NOTE** Artificially creating this situation is a bit difficult. But things such as these do happen. We stuck to Ctrl-G (or `^G`, if you prefer that style of notation) as our chosen invisible character because it is the only one that Linux enables us to use.

## Assigning Unique Filenames: Appending Information

Sometimes an application—or a user or a programmer, too—has to assign a unique name to a file. In this section, we discuss two methods of assigning unique names:

- Automatically appending the process number as a suffix to the end of a filename
- Automatically appending the date as a suffix to the end of a filename

## Appending a Process Number to a Filename

By appending two dollar signs to the end of a filename, as shown here and in Example 9.20, the shell automatically appends a two- to five-digit process number to the end of that filename. This technique will likely produce a unique filename every time. The syntax is as follows:

```bash
$ touch filename$$ <Enter>
```

## Example 9.20 Appending a Process Number to a Filename

Every day, Pedro Alonso, in RFI's Citrus Division, orders new equipment, fertilizer, seed, cuttings, and so on. He needs a way to make the daily orders files unique. What he does is:

```bash
$ touch citdiv_order$$ <Enter>
$ ls citdiv_order* <Enter>
citdiv_order342 citdiv_order1105 citdiv_order12038
```

> **NOTE** For both techniques, we are using the `touch` command to create example files. You, of course, can create files in many ways.

## Appending a Date to a Filename

Although appending a process number to a filename will produce a unique filename, some people prefer the suffix to tell them a little more about the file. This reason is why the other method, appending a date as the suffix, is popular.

But before we discuss the appending date suffix method, let’s take a closer look at the possible output of the `date` command. The following is a typical shell response to the `date` command when used by itself:

```bash
$ date <Enter>
Wed Jul 14 12:48:32 CDT 2001
```

When creating filenames, though, you probably do *not* want to include the text names of the day or month (such as Wed or July). Instead, you want to use their numerical equivalents (such as 07 for July). The numerical equivalent of the preceding date is generated as follows:

```bash
$ date +'%y%m%d%H%M%S' <Enter>
000714124832
```

Here, we ask the shell for the date in the format of year (y), month (m), day (d), hour (H), minute (M), and second (S).

As seen in Example 9.21, the filename is formatted as a basic filename, followed by a dot as a separator, followed by the date as an extension in the month-day-hour format. If you will be generating more than one filename per hour, though, you should add more precise date fields (minute or even second) to the format to prevent files from being overwritten (and thus, losing valuable information). The syntax is:

```bash
$ touch filename.'date +'[options]' <Enter>
```

No matter what you decide, be aware of the command syntax. Note that two types of metacharacters are used: the single quotation mark (`'`) and the back quote (`` ` ``).

## Example 9.21 Appending the Date to a Filename

After just a few weeks, the `cividov_order$$` files are starting to confuse Pedro and his other Citrus Division colleagues. Preston suggests that they use the


3. Linux substitutes values for the three variables that the `mail` utility uses. The `$1` variable is the first argument that passes from the command line as you call the program. This argument contains the subject line of the e-mail. `$friends` is the `for in` variable that contains `bob@mycomputer`. The `$2` variable is the second argument that passes from the command line, which contains the name of the file that contains the e-mail message.

I removed the switches from this program to make it easier for you to read. Nothing’s preventing you from leaving the switches in your program if you use the `for in` loop.

4. Linux then calls the `mail` utility, which sends the e-mail.

5. Linux reads the `done` command, which tells it to go to the top of the `for in` loop and read the next e-mail address on the wordlist. This address is `mary@mycomputer`. If it finds no more e-mail addresses, Linux executes the instructions following the `done` command. The program contains no more instructions, so Linux ends the program.

## Test your programming knowledge

- 1. Why do you create your own switches for your program?
  - a. So that you can display arguments on-screen.
  - b. So that you can identify information passing as arguments to your program.
  - c. So that you can turn on and off switches by using your program.
  - d. Because you fancy becoming an electrician.
- 2. What’s a wordlist?
  - a. The technical term that you use to describe switches.
  - b. The technical name for instructions written in your program.
  - c. A new type of word puzzle.
  - d. A list of values that you assign to the `for in` variable.

**Answers:** 1) *b.* See “Using switches to identify arguments.” 2) *d.* See “Looping through addresses.”

# Part IX

# The Part of Tens

# The 5th Wave By Rich Tennant

After spending hours trying to get the system up and running, Carl discovers that everything had been plugged into a "Clapper" light socket when he tries to kill a mosquito.

![](img/05279073f26be7df99b3c487360dec6a_268_0.png)

# In this part . . .

In this part, I get to tell you all sort of things that just don't come up in the regular chapters. Here you can find out about the most useful Linux utilities (and I know you're just waiting for the chance). You can also stumble across sources for more Linux programming information. And to top everything off, you even get a whole potpourri of topics that I can't fit elsewhere in the book.

# Chapter 22
## Ten of the Most Useful Linux Utilities

### In This Chapter

- Making your printing look fancy
- Checking the spelling in your documents
- Sorting information in your files
- Checking differences in files
- Comparing two files
- Making changes in a large file
- Splitting up large files
- Searching through a file
- Moving files between computers
- Cutting fields from a database file

One of the biggest challenges that you face in building a Linux program is assembling a bunch of utility programs that you or someone else has written. The whole philosophy of Linux, in fact, revolves around creating small utility programs, each program performing one task very well.

Programmers distribute hundreds of utility programs for the Linux operating system, and even more are available on the Internet. This book isn't big enough to discuss all the utilities out there, but I want to show you my top-ten list of useful Linux utilities. (My list may, of course, vary from David Letterman's list.)

## Accessing the Details

![](img/05279073f26be7df99b3c487360dec6a_271_0.png)

I present only the basic information for using each utility — just enough to whet your appetite. You can use the man pages in the online documentation (available on most Linux computers) to find out the details on how to use each of these utility programs.

To read everything that you can about the troff utility (which I discuss in the following section), for example, type the following command:

```bash
man troff
```

After you press Enter, Linux displays the manual pages that discuss the troff utility in detail.

![](img/05279073f26be7df99b3c487360dec6a_271_1.png)

You enter on the command line (at the Linux prompt) all the commands that I mention in this chapter. So if you're using the bash shell, your command looks as follows:

```bash
$ man troff
```

## Printing Fancy Stuff: troff

Most of the printing that you do in Linux is of the plain-Jane type. Whichever fonts and type sizes are available on your printer are the ones that you use for your document. Linux can also do all that fancy stuff that you see in Windows and Mac programs, such as designing page layouts and using fancy type.

If you have a printer that offers these features, Linux can send instructions to your printer to make your documents look fancy. The trick is to use the troff utility. It interprets special codes into commands that tell the printer to use those fancy features.

If you want Hello, world. to appear in 12-point type in your document, for example, you type the following line in the document file. (A document file is a file on your computer's disk that contains the text that you want to print in your document. You can create this file by using a text editor such as vi or from one of your own programs.)

```bash
.ps 12
Hello, world.
```

The .ps 12 special code tells the troff utility that, from this point on, you want to use 12-point size in your document. The troff utility then sends to the printer a printer code for 12-point size. If you want to change to another point size, you need to enter a different code into your document.

You use the `troff` utility to send a greeting to the printer, as follows:

```bash
troff greeting
```

And then you change the font to Roman, as in the following example:

```bash
.ps 12
.ft roman
Hello, world.
```

This example tells the `troff` utility that you want to use 12-point size (`.ps 12`) in the Roman font type (`.ft roman`). These settings remain in effect until you change the values by using the format commands `.ps` and `.ft`.

![](img/05279073f26be7df99b3c487360dec6a_272_0.png)

Keep in mind that using these codes in your documents involves one **major drawback**: Only the `troff` utility reads them. Don’t forget that you use the `lp` utility, too, to print your document (refer to Chapter 17). The `lp` utility, however, prints all the characters that you enter into the document. The `lp` utility doesn’t recognize, for example, that `.ps12` is a special code that it’s not to print because you’re using the code to give the `troff` utility an instruction.

## Checking Your Spelling: `spell`

Few people pose a threat to the national spelling-bee champion’s crown, and the typical error-filled business document proves my point. A **misspelling** is where the writer doesn’t know the correct spelling of the word. In comparison, a **typographical error** (typo) is where the writer knows the correct spelling of the word but inadvertently presses the wrong key on the keyboard while typing. Most people can come up with a host of excuses for such errors, as the following list attests:

- “My secretary is a poor proofreader.” (Do you even have a secretary?)
- “I was in a rush and didn’t catch that mistake.” (You read the document ten times.)
- “He’s never going to notice that it’s misspelled.” (Oh, how you wish that this one were true!)
- “She knows what I mean.” (She also knows that you *don’t* know — how to spell, that is.)

Now you have no excuse for misspellings or typos in the documents you create in Linux unless you’re just too lazy to use `spell`. This simple spell-checker utility reads your documents and then displays the words that it can’t find in its dictionary file.

Suppose that you type the following text in a document and then save the document in a file that you name letter:

```text
Dear Mary,
We had a go time Saturday. Let's do it again soon.
```

Use the following command to have spell take a look at the file:

```bash
spell letter
```

The following lines then appear on-screen:

```text
nab
goo
```

Using the spell utility has a few drawbacks, however, as I describe in the following list:

- The spell utility catches any word that it doesn't find in its dictionary file, but the word may not necessarily be a misspelling. The spell utility really compares the words in your document against those that the programmer entered into the spell utility's dictionary. In an address where the town is Ridgefield Park, for example, the spell utility reports that Ridgefield is an incorrect spelling. In fact, Ridgefield is correct but just doesn't appear in the spell utility's dictionary.
- The spell utility lists misspelled words — but because it doesn't show you where they appear in the document, you must find them yourself.

## Sorting Stuff in Your Files: sort

Your programs can produce a list of names, but someone who uses your program may want you to sort the list. You can spend many evenings researching ways to write a program to sort the list, or you can simply use the sort utility.

Suppose that you place some names in a file that you call names. You can type the following line to sort the list:

```bash
sort names
```

The sort utility rearranges a list in ascending order (where the As come before the Bs and the 1s come before the 2s) and places a lowercase letter ahead of its equivalent uppercase letter. You also can change the utility to sort in descending order (where the Bs come before the As and the 2s come before the 1s) by using the -r option, as follows:

```bash
sort -r names
```

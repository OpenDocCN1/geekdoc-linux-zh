
## Workshop

The Workshop summarizes the key terms you’ve learned and poses some questions about the topics presented in this lesson. It also provides you with a preview of what you will learn in the next hour.

## Key Terms

**control key notation** This notational convention in Unix denotes the use of a Control key. There are three common conventions (Ctrl-C, ^C, and C-c) that all denote the Control-c character, produced by pressing the Control key (labeled Control or Ctrl on your keyboard) and, while holding it down, pressing the c key.

**interactive program** An interactive Unix application is one that expects the user to enter information and then responds as appropriate. The `ls` command is not interactive, but the `more` program, which displays text a screenful at a time, is interactive.

**null character** Each character in Unix has a specific value, and any character with a numeric value of zero is known as a null or null character.

**pipeline** A pipeline is a series of Unix commands chained by |, the pipe character.

## Exercises

- 1. Many people who use Unix systems tend to stick with file-naming conventions. Indeed, Unix has many of its own, including `.c` for C source files, `.gz` for gzip compressed files, and a single dot prefix for dot files. Yet `file` often ignores filenames when it ascertains what type of content is within. (Test it yourself.) Why?
- 2. Do you remember the television game show “Name That Tune?” If so, you’ll recall that contestants had to identify a popular song by hearing just the first few notes. The `file` command is similar; the program must guess at the type of the file by checking only the first few characters. Do you think it would be more accurate or less accurate if it checked more of the file? Why should or shouldn’t it do so? (Think about this one.)
- 3. Use `more` to check some possible file types that can be recognized with the `file` command by peeking in the configuration file `/etc/magic`.
- 4. How did the `cat` command get its name? Do you find that to be a helpful mnemonic?
- 5. Here’s an oddity:
  
  `cat LISTS | more`
  
  What will this command do?
- 6. If you were looking at an absolutely huge file, and you were pretty sure that what you wanted was near the bottom, what command would you use, and why?
- 7. What if the information were near the top?

## Preview of the Next Hour

Many non-alphanumeric characters have special functions in Unix, as you have doubtless learned by accidentally typing a slash, an asterisk, a question mark, a quotation mark, or just about any other punctuation character. What might surprise you is that they all have different specific meanings that are more or less consistent throughout the system. The next hour explains considerably more about how pipelines work and how programs are used as filters. Among the new commands you will learn are `sort`, `wc`, `nl`, `uniq`, and `spell`. You also will learn how to work with filename wildcards on the command line to refer to groups of files all at once.

## Hour 8. Filters, Pipes, and Wildcards!

### Goals for This Hour

In this hour, you will learn

- The secrets of file redirection
- How to count words and lines using `wc`
- How to sort information in a file using `sort`
- Working with wildcards
- Searching files with `grep`
- Creating regular expressions
- The rest of the `grep` family

If you’ve ever learned a foreign language, you know that the most common approach is to start by building your vocabulary (which always includes the names of the months, for some inexplicable reason) and then learning about the rules of sentence construction. The Unix command line is much like a language in this regard. Now that you’ve learned many Unix “words,” it’s time to learn how to put them together as “sentences,” using file redirection, filters, and pipes.

One of the trickiest aspects of Unix is the concept of wildcards and regular expressions. A *wildcard* allows you to “guess” at a filename or to specify a group of filenames. *Regular expressions* match patterns and are different from, and more powerful than, wildcards.

In this important lesson, you’ll also meet the wonderful command `grep`, which is based on regular expressions, along with the commands `wc`, `sort`, and `uniq`.

This hour begins by focusing on one aspect of constructing powerful custom commands in Unix by using file redirection. The introduction of some filters—programs intended to be used as part of command pipes—follows. Next you’ll learn another aspect of creating your own Unix commands: using pipelines.

### Maximizing the Command Line

Now that you’ve learned some of the individual words of the Unix command vocabulary, it’s time to get into some of the fun and power of the Unix system: combining individual commands into *pipes* or *filters* to perform complex and sophisticated tasks.

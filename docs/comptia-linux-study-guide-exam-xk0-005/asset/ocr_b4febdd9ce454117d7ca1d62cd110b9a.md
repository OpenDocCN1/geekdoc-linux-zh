![](bbox=[0.13, 0.1, 0.34, 0.27])

Managing a Linux server involves many important steps and decisions based on data. Trying to gather the information you need in an agile and efficient manner is crucial. There are many Linux structures and tools that can help you uncover the knowledge you seek quickly.

In this chapter, we'll add more items to your Linux command-line tool belt. We'll cover filtering and formatting text and the basics of redirection, all the way to editing text. Commands and concepts in this chapter will be built upon and used in later chapters.

# Processing Text Files

Once you have found or created a text file, you may need to process it in some way to extract needed information. Understanding how to filter and format text will assist you in this endeavor. In the following sections, we'll take a look at tools and methods that will aid you in processing text files.

# Filtering Text

To sift through the data in a large text file, it helps to quickly extract small data sections. The cut utility is a handy tool for doing this. It will allow you to view particular fields within a file's records. The command's basic syntax is as follows:

```
```bash
cut OPTION... [FILE]...
```
```

Before we delve into using this command, here are a few basics you should understand about the cut command:

+   * **Text File Records** A text file record is a single file line that ends in a newline line-feed, which is the ASCII character LF. You can see if your text file uses this end-of-line character via the cat -E command. It will display every newline linefeed as a $ . If your text file records end in the ASCII character NUL, you can also use cut on them, but you must use the -z option.
+   * **Text File Record Delimiter** For some of the cut command options to be properly used, fields must exist within each text file record. These fields are not database-style fields but instead data that is separated by some delimiter. A delimiter is one or more characters that create a boundary between different data items within a record. A single space can
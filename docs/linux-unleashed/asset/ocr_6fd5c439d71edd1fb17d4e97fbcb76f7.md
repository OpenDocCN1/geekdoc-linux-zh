The *awk* programming language was created by the three people who gave their last-name initials to the language: Alfred Aho, Peter Weinberger, and Brian Kernighan. The *gawk* program included with Linux is the GNU implementation of that programming language.

The *gawk* language is more than just a programming language; it is an almost indispensable tool for many system administrators and UNIX programmers. The language itself is easy to learn, easy to master, and amazingly flexible. After you get the hang of using *gawk*, you'll be surprised how often you can use it for routine tasks on your system.

To help you understand *gawk*, we will follow a simple order of introducing the elements of the programming language, as well as showing good examples. You are encouraged, or course, to experiment as the chapter progresses. It's not possible to cover all the different aspects and features of *gawk* in this chapter, but we will look at the basics of the language and show you enough, hopefully, to get your curiosity working.

# # What Is the gawk Language?

*gawk* is designed to be an easy-to-use programming language that lets you work with information either stored in files or piped to them. The main strengths of *gawk* are its capabilities to do the following:

+   - Display some or all the contents of a file, selecting rows, columns, or fields as necessary.
- Analyze text for frequency of words, occurrences, and so on.
- Prepare formatted output reports based on information in a file.
- Filter text in a very powerful manner.
- Perform calculations with numeric information from a file.

*gawk* isn't difficult to learn. In many ways, *gawk* is the ideal first programming language because of its simple rules, basic formatting, and standard usage. Experienced programmers will find *gawk* refreshingly easy to use.

# # Files, Records, and Fields

Usually, *gawk* works with data stored in files. Often this is numeric data, but *gawk* can work with character information, too. If data is not stored in a file, it is supplied to *gawk* through a pipe or other form of redirection. Only ASCII files (text files) can be properly
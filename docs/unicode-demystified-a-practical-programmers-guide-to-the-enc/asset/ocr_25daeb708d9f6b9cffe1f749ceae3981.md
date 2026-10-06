# aspell

Checks a file for spelling errors

aspell action [options] filename
The Aspell utility checks words in a document against a standard dictionary. You can use the aspell utility interactively: It displays each misspelled word in context, together with a menu that gives you the choice of accepting the word as, choosing one of aspell's suggested replacements for the word, inserting the word into your personal dictionary, and entering a new word. You can also use aspell so that it reads from standard input and writes to standard output. This mode is suitable when you want to redirect from standard input or output or simply want a list of misspelled words, per line.

For more information refer to /usr/share/doc/aspell* on your system (with manuals in the man-html and man-text subdirectories) and to the aspell home page at aspell.sourceforge.net.

| aspell Is Not Like Other Utilities Regarding Its Input | tip

Unlike many other utilities, aspell does not accept input from standard input when you do not specify a filename on the command line. Instead, the aspell specifies where aspell gets its input.

# Action

You can specify the aspell action¹ using the long form (not preceded with a hyphen) or the short form (preceded with a hyphen)—not all actions have short forms. You must choose one and only one of the actions when you run aspell.

+   - check -c Runs aspell as an interactive spell checker. Input comes from a single filename on the command line.
- config Displays aspell's configuration: both the default and current values. Output goes to standard output. Send the output through a pipe to less to read the whole document.
- help -2 Displays an extensive page of help. Output goes to standard output. Send the output through a pipe to less for easier viewing.
- list -1 Runs aspell noninteractively. Input comes from standard input. Output goes to standard output.

+   1. The aspell manual uses the term comands where its usage message uses the term action. This book uses action.
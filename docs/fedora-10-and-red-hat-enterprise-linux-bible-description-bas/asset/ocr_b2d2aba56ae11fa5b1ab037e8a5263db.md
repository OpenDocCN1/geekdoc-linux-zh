# Creating Documents in Groff or LaTeX

You can create documents for either of Linux's Groff (nroff) or LaTeX (TeX) styles of publishing using any text editor. Fedora and RHEL come with several text editors, or you can download them from the Internet. See the section "Text Editors and Notpads," earlier in this chapter, for more information.

The process of creating documents in Groff or LaTeX consists of the following general steps:

+   1. Create a document with any text editor. The document will contain text and markup.
2. Format a document using a formatting command that matches the style of the document that you created (for example, with groff or latex). During this step, you may need to indicate that the document contains special content, such as equations (eqn command), tables (tbl command), or line drawings (pic command).
3. Send the document to an output processor with a GUI. The device may be a printer or display program.

If you are used to a word processor with a GUI, you may find these tools difficult. In general, Groff is useful to create man pages for Linux. LaTeX is useful if you need to produce mathematical documents, perhaps for publication in a technical journal.

# Text processing with Groff

nroff and troff formatting commands were the first interfaces available for producing typesetting output with the UNIX system. They aren't editors; rather, they are commands that you send to troff, with the result being formatted:

+   * nroff — Produces formatted plain text and includes the ability to do pagination, indents, and text justification, as well as other features.
* troff — Produces typeset text, including everything nroff can do, plus the ability to produce different fonts and spacing. The troff command also supports kerning.

The groff command is the front end for producing nroff/troff documentation. Because Linux man pages are formatted and output in Groff, many of the examples here help you create and print man pages with Groff.

People rarely use nroff/troff markup. Instead, there are common macro packages that simplify the creation of nroff/troff-formatted documents:

+   * man — The macros are used to create Linux man pages. You can format a man page using the -man option to the groff command.
* mm — The mm macros (memorandum macros) were created to produce memos, letters, and technical white papers. This macro package includes macros for creating a table of contents, lists of figures, references, and other features that are helpful for producing technical documents. You can format an mm document using the -mm groff option.
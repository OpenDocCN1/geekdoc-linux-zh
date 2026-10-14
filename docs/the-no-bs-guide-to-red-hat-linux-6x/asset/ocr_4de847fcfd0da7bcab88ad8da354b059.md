For most people, a text editor is the most basic and often-used computer tool. If you want to write a letter, send email, or compose a computer program, you use a text editor to enter your prose and save it in a file.

Although they perform the same basic functions, a text editor and a word processor (such as Word or WordPerfect) are slightly different in nature. In general, a text editor is like a very basic word processing program—it doesn’t offer fancy stuff like fonts, underlining, and boldface. A text editor is useful for entering, updating, and storing text, but you need a word processor to create really sharp-looking documents.

Aside from their differing looks and abilities, text editors and word processors store data in different formats. Text editors store files in plain-text (ASCII) format, which means the files can be read by any other text editor or program, whereas word processors store them in specially coded formats that can be read only by that program. (Actually, most of the popular word processors can read files created by other programs, but you don’t always get the same formatting.) In the DOS/Windows environment, the Edit and Notepad programs are simple text editors, whereas Microsoft Word is a true word processor.

This chapter focuses on three nongraphical Linux text editors (vi, Emacs, and Pico) and two that run under X Windows (Gnotepad+ and gEdit), which can be used to create and modify files. You’ll get an introduction to each one here, and then you can decide which one is best for you.

# THE VI EDITOR

The vi editor comes with every version of Linux or Unix. It’s a terribly unfriendly beast of an editor, but you should know about it because someday you’re likely to find yourself on a system where you have no other choice but to use it. A friend of mine calls vi the Heart of Evil, but that might be just a bit harsh—you decide.

Using vi is similar to using other editors in that you can see your file on the screen (this is not the case with a line editor, for example), move from point to point in the file, and make changes. But that’s where the similarities end. Cryptic commands, a frustrating user
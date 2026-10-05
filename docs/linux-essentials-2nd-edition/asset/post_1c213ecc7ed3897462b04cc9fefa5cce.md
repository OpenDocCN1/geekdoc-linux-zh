
- C. dmesg
- D. rpm
- E. apt-get
- 2. What is the usual name of the first process that the Linux kernel runs, aside from itself?
- A. init
- B. bash
- C. cron
- D. login
- E. grub

- 3. Where do most log files reside on a Linux computer?
- A. /var/log
- B. /etc/logging
- C. /usr/log
- D. /home/logging
- E. /log/usr

- 4. True or false: When using suitable commands, you can install a program and be sure that all of the software on which it depends will also be installed, provided you have an Internet connection.

- 5. True or false: By default, the first process in top is currently consuming the most CPU time.

- 6. True or false: The dmesg command may produce different output after a computer has been running for weeks than when it first started.

- 7. Most Linux distributions maintain information on what packages are installed in the ____________ (Two words).

- 8. You're using bash, and you type emacs to launch the emacs editor. In this case, emacs is bash's ____________

- 9. General system messages are likely to be found in /var/log/messages or /var/log/____________, depending on your distribution.

- 10. The command that you use to read messages generated during the boot process and stored in the kernel buffer is the ____________ command.

# Editing Files

Computer documents come in in many forms, but one of the most basic and flexible is a text file. Typically, configuration files and shell scripts are text files. Because you will often be modifying configuration files and creating shell scripts, you must be able to edit text files. This chapter covers this task with an emphasis on the simple text-mode pico, nano, and vi editors. A few roles played by text files are described first; then how to select a editor is covered. To edit text files, of course, you must be able to start the editor, either on an existing document or a new one. The pico and nano editors are quite similar, so their operation is described together, followed by vi, which is a much more unusual editor by modern standards.

- Understanding the role of text files
- Choosing an editor
- Launching an editor
- Editing files with pico or nano
- Editing files with vi

# Understanding the Role of Text Files

A text editor lets you edit documents that are stored in plain-text format. The American Standard Code for Information Interchange (ASCII) used to be the common format, but now files typically use Unicode formats to support additional characters. These formats store text documents that, by themselves, include no special formatting or embedded features. Text files cannot include graphics, use multiple fonts, emphasize words by italicizing them, or use other features that you probably associate with word processors (although markup tools provide a partial exception to this rule).

> If a text file is encoded in ASCII, it's encoded in Unicode too. ASCII encoding is a subset of Unicode.

# ASCII AND UNICODE

ASCII dates to the 1960s. It's a 7-bit code, meaning that it supports a maximum of 2⁷ or 128 characters. (In practice, ASCII uses 8 bits, so an extra 128 characters are available. These bits encode control characters or are used in ASCII extensions.) ASCII was created to encode the letters used in English, digits, and symbols. This original intent, combined with ASCII's limited character count, makes it unhelpful for many English languages. ASCII doesn't have enough characters to handle all the requirements of non-English languages.

Over the years, extensions to, and variants of, ASCII have been used to support additional characters and alphabets that ASCII doesn't support. One way to do this is to use a code page to specify an alphabet. For instance, code page 866 encodes Cyrillic (the alphabet used by most Slavic languages). The problem with code pages is that you can generally use one at a time.

Unicode is a more modern approach. It provides a much larger character set, allowing the encoding of any alphabet in common use on Earth, including the huge graphic writing systems used in languages such as Chinese and Japanese. The problem is that Unicode requires more bits, and ways to encode it efficiently. Fortunately, Unicode Transformation Format (UTF) schemes are limited in number compared to code pages. Some, such as UTF-8, have the first characters the same as ASCII, so an ASCII file is also a valid UTF-8 file (or other Unicode formats). Many text editors handle UTF-8 well so you can use a text editor to write text files in any language you like. You may still need to set localization options to tell Linux what sort of keyboard you use and use code page to rely on code.

Text files encode the ends of lines using one or two ASCII characters. End of line encoding differs between Unix (Linux) and Windows, but most programs can handle either method.

Formatted text files encode special formatting using unique character sequences. Although you can edit such files with specialized editors also exist for many of these file types.

Text files consist of lines that can vary in length from 0 characters to the file entire size and can hold any number of data types. You might want to create or edit some of these as an ordinary user, while others are important for administering a Linux system. The main file types include the following:

- Human language files
- Programming language files
- Formatted text files
- Program and system configuration files
- Program log files

Some files contain elements of multiple categories. Email, for instance, can be stored in text files. An email file consists largely of human language, but email messages include headers, which describe the origin and destination computers, with information on how the message traveled from one site to the other, which is similar to formatted text or log data.

# Choosing an Editor

All Linux distributions ship with many text editors. Broadly speaking, text editors fall into one of two categories: text-mode and GUI. Beginners are generally more comfortable with GUI editors, which can be more convenient to use even for experts. But when a GUI is not available, you may have to use a text-mode editor. Thus it is recommended that you familiarize yourself with at least one text-mode editor. Some popular text editors include the following:

- vi This editor is a Unix staple. It is small and usually installed by default, you can be certain that it's present on any Linux computer. It is, however, strange by modern standards—it uses multiple editing modes, and you must switch between them to accomplish various tasks. Many Unix and Linux administrators like vi for its flexibility, power, and size.

- emacs This is another Unix staple. It is a big editor with lots of features, so it's less likely to be installed by default, particularly on small, lightweight distributions. Its operating mode is more those of the text editors with which novices are familiar, but its commands can seem rather odd.

- pico Some small editors are modeled after emacs, but they omit many advanced features in an effort to simplify the editor. One is pico, which originated as part of the pico email package.

- nano This is a clone of pico that adds extra features. Even with the additional features, nano is small, lightweight, and easy to use. The nano editor is probably the best place to start, because of its ease of use. If nano is not already installed, it's typically available in most distributions' software repositories. If you don't find installed on your distribution, see Chapter 9, "Exploring Processes and Data," for installing the nano package.) For the most part, pico works just like nano, but because nano adds to pico, nano is a more capable editor. Figure 10.1 shows nano in operation within a text-mode login session, editing a file called pets.txt.

With text-mode editors, several GUI editors are available, including the following:

emacs This editor is a text-mode editor and a GUI editor. The GUI features of emacs, however, are sometimes a bit odd; for instance, the scroll bar move through the file appears on the left side of the window rather than the more common right side.

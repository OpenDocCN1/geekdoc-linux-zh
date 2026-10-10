Scripting-Language Configuration

A more open-ended approach is to make available a simple scripting language with which the user can write new commands or routines. This works well if the language is simple enough to learn easily but still provides the necessary “hooks” into the application’s internals. This is the route that Emacs developers have fol- lowed, but Emacs’ use of Emacs-Lisp goes beyond the usual relationship of an application and its scripting language. Although the core of Emacs is written in C (for speed and window-system display purposes), the actual editing functions are written in Lisp. Since the scripting language is also Lisp, changing Emacs behav- ior is both convenient and powerful. While it’s running, Emacs stores in your machine’s memory a plethora of functions and variables. All of these are accessible and therefore modifiable using simple Lisp statements. Even the documentation for the functions and variables is instantly available, because it is stored within the Lisp files. (See Chapter 3.)

Emacs Vocabulary and Conventions

To help you learn about Emacs, I will define a few peculiar terms. Many of them are ordinary English words that have a different meaning when used in Emacs documentation. Some of these words are a legacy of the early days of computing, when Emacs and Lisp were first being developed.

Buffers and the Point

The word *buffer* refers to a text file loaded into memory (the text may be displayed or hidden) by Emacs. The word was originally a computer programmer’s term for an area of machine memory set aside for a specific purpose. This term is used rather than *file* to emphasize the difference between the copy of the file being edited and the actual file on disk. When the edited buffer is saved, it is written back to the hard disk, overwriting the original file. Emacs can edit multiple files at once, so at any given time there might be many buffers.

Emacs also has internal buffers that don’t correspond to any file. One of these is visible when Emacs is started up without a file name as an argument. It is called the *Scratch buffer*. It automatically appears in a special editing mode used for writ- ing Emacs-Lisp code. A new Lisp-Interaction item appears on the menu bar whenever the Scratch buffer is visible.
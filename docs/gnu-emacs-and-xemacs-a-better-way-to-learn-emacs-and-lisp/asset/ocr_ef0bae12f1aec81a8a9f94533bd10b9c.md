**string.** A sequence of text characters. A general term that includes but is not limited to words and sentences.

**symbol.** A type of atom. Symbols have names which consist of a sequence of characters uninterrupted by whitespace. They are used to uniquely identify Emacs Lisp functions. A symbol can also have a value associated with it, in which case the symbol identifies a variable. A single symbol can identify both a variable and a function. See atom, function, and variable.

**variable.** An Emacs Lisp symbol that has a value that can be changed, roughly equivalent to a setting. A variable can have more than one symbol associated with it. You can customize many aspects of Emacs behavior by changing the values of variables.

**window.** An editing area in an Emacs frame that has its own modeline. The frame can display one window that fills the available area. Two or more windows can share the same frame, with the division between them either horizontal or vertical. An Emacs window is not the same as an X window; an Emacs X window is called a frame so as to distinguish the two.

**yank.** The Emacs term for inserting previously cut or copied text into a buffer. Most applications use the term “paste” instead.
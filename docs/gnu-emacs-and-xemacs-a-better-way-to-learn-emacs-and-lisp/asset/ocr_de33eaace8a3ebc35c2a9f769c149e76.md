**markup.** Special characters that are understood by text-formatting systems and languages such as LaTeX and HTML. These characters are a code that tells external software how to display different sections of a file.

**minibuffer.** A horizontal strip in an Emacs frame just beneath the modeline. This is an area where the user communicates with Emacs. Messages from Emacs are displayed here. This is where you type in information Emacs needs to do its work, such as commands or file names.

**mode.** A bundle of Emacs settings optimized for a certain type of editing. A mode can be invoked manually or automatically, as when a file with a particular suffix is loaded. A major mode is a mode that alters many settings, such as the keybindings and screen appearance. Only one major mode can be active at a time. A minor mode affects just a few settings. More than one minor mode can be active at the same time along with a major mode.

**modeline.** Just beneath the editing area of an Emacs window is a multi-purpose horizontal area, usually of a contrasting color, that is full of information about the current state of affairs. You can see the current file's name, whether it has been modified, where point is in the buffer, and the currently active modes. Several options control what you see in the modeline.

**point.** Synonymous with cursor location. Every buffer has a point position that Emacs remembers even when you are editing another buffer. The cursor is present only in the current buffer. See also **mark**.

**query-replace.** A form of search-and-replace during which the user is asked whether each match should be replaced with the new string or left alone.

**region.** An area of text that has been selected or marked with either the keyboard or the mouse. The marked region may be highlighted, but this is optional and isn't the default in some versions of Emacs. A region can be copied or deleted (killed). In Emacs terminology, a region is an area of text between **point** (the cursor location) and **mark**. See **point** and **mark**.

**regular expression (regexp).** A technique used by software to find matches for strings of text. Special “wildcard” characters are reserved for matching characters and sequences of characters that fulfill certain requirements. A regular expression is a pattern of characters that match themselves, interspersed with the special characters. See Chapter 3 for a description of how regular expressions can be used in the various Emacs searching commands.

**setq.** A commonly used Emacs Lisp function that assigns a value to a variable.

**shell buffer.** A special type of Emacs buffer that contains a shell prompt. You can run text-mode Linux commands and use any of the Emacs commands on the output.
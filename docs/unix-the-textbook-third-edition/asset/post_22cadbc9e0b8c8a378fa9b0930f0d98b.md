
## TABLE 3.11 Summary of Help Command Syntax

|  |  |
|---|---|
| <Ctrl+H> a topics <Enter> | Display a list of commands whose names match topics (apropos-command). |
| <Ctrl+H> b | Display all active key bindings—minor mode bindings first, then those of the major mode, then global bindings (describe-bindings). |
| <Ctrl+H> c key | Show the name of the command that the key sequence key is bound to (describe-key-briefly). Here c stands for "character." For more extensive information on key, use <Ctrl+H> k. |
| <Ctrl+H> d topics <Enter> | Display the commands and variables whose documentation matches topics (apropos-documentation). |
| <Ctrl+H> e | Display the *Messages* buffer (view-echo-area-messages). |
| <Ctrl+H> f function press <Enter> | Display documentation on the Lisp function named function (describe-function). Since commands are Lisp functions, this works for commands too. |
| <Ctrl+H> h | Display the HELLO file, which shows examples of various character sets. |
| <Ctrl+H> i | Run Info, the GNU documentation browser (info). The emacs manual is available in Info. |
| <Ctrl+H> k key | Display the name and documentation of the command that key runs (describe-key). |
| <Ctrl+H> l | Display a description of your last 300 keystrokes (view-lossage). |
| <Ctrl+H> m | Display documentation of the current major mode (describe-mode). |
| <Ctrl+H> n | Display news of recent emacs changes (view-emacs-news). |
| <Ctrl+H> p | Find packages by topic keyword (Finder-by-keyword). This lists packages using a package menu buffer. |
| <Ctrl+H> P package <Enter> | Display documentation about the package named package (describe-package). |
| <Ctrl+H> r | Display the emacs manual in Info (info-emacs-manual). |
| <Ctrl+H> s | Display the contents of the current syntax table (describe-syntax). The syntax table says which characters are opening delimiters, which are parts of words, and so on. |
| <Ctrl+H> t | Enter the emacs interactive tutorial (help-with-tutorial). |
| <Ctrl+H> v var <Enter> | Display the documentation of the Lisp variable var (describe-variable). |
| <Ctrl+H> w command <Enter> | Show which keys run the command named command (where-is). |
| <Ctrl+H> C coding <Enter> | Describe the coding system coding (describe-coding-system). |
| <Ctrl+H> C <Enter> | Describe the coding systems currently in use. |
| <Ctrl+H> F command <Enter> | Enter Info and go to the node that documents the emacs command command (Info-goto-emacs-command-node). |
| <Ctrl+H> I method <Enter> | Describe the input method method (describe-input-method). |
| <Ctrl+H> K key | Enter Info and go to the node that documents the key sequence key (Info-goto-emacs-key-command-node). |
| <Ctrl+H> L language-env <Enter> | Display information on the character sets, coding systems, and input methods used in language environment language-env (describe-language-environment). |
| <Ctrl+H> S symbol <Enter> | Display the Info documentation on symbol symbol according to the programming language you are editing (info-lookup-symbol). |
| <Ctrl+H> ? | Display the help message for a special text area, if the point is in one (displaylocal-help). (These include, for example, links in *Help* buffers.) |

graphical style of interaction. When a menu choice is grayed out, that means it is not available at the current level you are operating at. The following is a brief description of what tasks each menu bar item accomplishes.

- File: Facilities for opening, saving, and closing buffers, files, windows, and frames
- Edit: Means to modify text in buffers
- Options: Facilities to make configuration changes
- Buffers: A pull-down menu listing of the currently open buffers
- Tools: File and application functions
- Help: Extensive documentation and online manual for emacs

The speed button bar contains single-button presses for (1) file and buffer operations; (2) common text-editing operations, such as cut and paste; and (3) printing, searching, and changing preferences.

## 3.3.1.2 Buffers, File, Windows, and Frames

The most important concept in emacs is that of a buffer, or text object that is currently being edited by emacs. This different from a file, which is a text object stored on disk. The differentiation is made, in simple terms, because (1) the object currently being modified and viewed in emacs cannot be the same object stored on disk as you have not yet saved your edits; and (2) emacs can work on text objects that are not files and never will be, such as the output from commands typed on the UNIX command line. When you first launch emacs and specify a file to edit, you are looking into the buffer created by emacs for that file in what is generally known as an emacs frame, with a single window open to allow you to see the buffer contents. A frame consists of one window, or possibly many windows, tiled in it, the pull-down and speed button bar menus, the mode line, and the minibuffer. In Practice Sessions 3.12, 3.13, and 3.14, you will work with multiple buffers viewed in emacs using multiple windows in one frame only.

## 3.3.1.2 Point, Mark, and Region

The second most important concept in emacs is that of the point and mark, and the region of text they demarcate. The point is located in the white space before the character the cursor is highlighting. The mark, set by placing the cursor over a character and then holding down <Ctrl+Space> or <Ctrl+@>, is also in the white space before the character the cursor is highlighting. The region or area of text you want to manipulate in operations is cutting and copying, is all text between the point and the mark. For example, in the line of text Now is the time for all good men, if the cursor is on or highlighting the N in the word Now (the point is in the white space before the N), and the mark has been set before the character i in the word time by placing the cursor on the letter i and holding down <Ctrl+Space>, then the region is defined as Now is the t.

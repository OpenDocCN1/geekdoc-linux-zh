
<F3>

Start defining a keyboard macro (kmacro-start-macro-or-insert-counter).

<F4>

Dual-purpose function key. If a keyboard macro is being defined, end the definition; otherwise, execute the most recent keyboard macro (kmacro-end-or-call-macro).

<Ctrl+U> <F3>

Re-execute last keyboard macro, then append keys to its definition.

<Ctrl+U> <Ctrl+U> <F3>

Append keys to the last keyboard macro without re-executing it.

<Ctrl+X> <Ctrl+K> r

Run the last keyboard macro on each line that begins in the region (apply-macro-to-region-lines).

To start defining a keyboard macro, type <F3>. From then on, your keys continue to be executed, but also become part of the definition of the macro. Def appears in the mode line. When you are finished, type <F4> (kmacro-end-or-call-macro) to terminate the definition. For example:

<F3> <Alt+F> Mansoor <F4>

defines a macro to move forward a word and then insert Mansoor at the point. <F3> and <F4> do not become part of the macro.

After defining the macro, it is the most recently defined keyboard macro, and you can call it with <F4>. In the example, this has the same effect as typing <Alt+F> Mansoor again.

The two roles of the <F4> command: it ends the macro if you are in the process of defining one, or calls the macro otherwise.

You can also supply <F4> with a numeric prefix argument n, which means to invoke the macro n times. An argument of zero repeats the macro indefinitely, until it gets an error or you type <Ctrl+G> to terminate it.

After ending the definition of a keyboard macro, you can append more keystrokes to its definition by typing <Ctrl+U> <F3>. This is equivalent to plain <F3> followed by retyping the whole definition so far. As a consequence, it re-executes the macro as previously defined. If you change the variable kmacro-execute-before-append to nil, the existing macro will not be re-executed before appending to it (the default is t). You can also add to the end of the definition of the last keyboard macro without re-executing it by typing <Ctrl+U> <Ctrl+U> <F3>.

When a command reads an argument with the minibuffers, your minibuffers input becomes part of the macro along with the command. So when you replay the macro, the command gets the same argument as when you entered the macro. For example:

<F3> <Ctrl+A> <Ctrl+K> <Ctrl+X> b Mansoor <Enter> <Ctrl+Y>
<Ctrl+X> b <Enter> <F4>

defines a macro that kills the current line, yanks it into the buffer Mansoor, then returns to the original buffer. The command <Ctrl+X> <Ctrl+k> r (apply-macro-to-region-lines) repeats the last defined keyboard macro on each line that begins in the region. It does this line by line, by moving the point to the beginning of the line and then executing the macro.

All defined keyboard macros are recorded in the keyboard macro ring. There is only one keyboard macro ring, shared by all buffers. The basic keyboard macro ring operations are

<Ctrl+X> <Ctrl+K> <Ctrl+K>

Execute the keyboard macro at the head of the ring (kmacro-end-or-callmacro-repeat).

<Ctrl+X> <Ctrl+K> <Ctrl+N>

Rotate the keyboard macro ring to the next macro (defined earlier) (kmacrocycle-ring-next).

<Ctrl+X> <Ctrl+K> <Ctrl+P>

Rotate the keyboard macro ring to the previous macro (defined later) (kmacrocycle-ring-previous).

Note: The maximum number of macros stored in the keyboard macro ring is determined by the customizable variable kmacro-ring-max.

## 3.3.13.5.2 Naming, Saving, and Invoking or Using Keyboard Macros

The following are the ways to name, save, and invoke or use keyboard macros, particularly with regard to retaining them in your ~/.emacs or init file so that they will be available in all future sessions of emacs (anything below enclosed in [ ] is optional).

- 1. <Ctrl+X> <Ctrl+K> n <Enter> macroname <Enter>

Gives a command name (for the duration of the current emacs session only) to the most recently defined keyboard macro (kmacro-name-last-macro). If you wish to save a keyboard macro for later use, you can give it a name using this syntax. This sequence reads a name as an argument, by prompting for the name in the minibuffers, and uses the minibuffers-supplied name and defines that name so that you can execute the last

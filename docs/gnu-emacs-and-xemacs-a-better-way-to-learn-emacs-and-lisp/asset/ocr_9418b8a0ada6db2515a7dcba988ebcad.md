do basic mathematics, such as working with integers, random numbers, and logical operators. The greater emphasis was on strings of characters: matching, searching, pasting, and all the other text-manipulation operations. Portability was another issue. Some of the older Lisp variants were optimized for particular platforms and would be difficult to port. Stallman wrote his Lisp in C, a language that can be compiled on nearly any platform.

Though some Lisp implementations have compilers, Stallman chose to make Emacs-Lisp an interpreted language. This allows on-the-fly changes of variable values and function definitions, significant assets for a programmable editor.

Lisp was designed to be an extensible language. Due to the fact that Lisp code is interpreted at runtime (rather than being compiled into a binary executable), changes in Lisp source-code files can be made and tested quickly without a time-consuming compilation. This trait fits in perfectly with Richard Stallman's idea of a user-configurable editor, an application that any user with a little knowledge of Lisp could extend for unanticipated purposes.

# A Mixture of C and Lisp

Lisp has a drawback common to all interpreted languages: lack of execution speed. Programs written in compiled languages such as C run quickly. In a sense, the interpretation of the language is done beforehand, when the source code is compiled and linked into a binary executable. The downside is that in order to modify a program's behavior, the source code must be changed and the program recompiled—something an end-user shouldn't be required to do.

Using Lisp, an Emacs user can change variables and functions “on-the-fly,” and they will take effect immediately. This is a direct result of using Lisp as the editing engine on top of a low-level layer of compiled C code.

# Why Emacs Is Written in Two Languages

Emacs was designed to benefit from the best characteristics of both Lisp and C. Aspects of the editor that users would rarely if ever change are written in C. These components are the substructure of the editor—the parts that interact with the host operating system and windowing system. These low-level parts could be thought of as the bones of Emacs, while the Lisp components make up the flesh.
Emacs-Lisp is a human-readable language. It might not be as easy to read as English, but words and phrases are identifiable, and the characters are all ASCII text. This readability is a plus for people, but it is a stumbling block for programs that need to read Lisp files, such as the Emacs-Lisp interpreter.

A computer program doesn’t read a file the way we read text. Like people tend to do, a program starts at the beginning of a file and makes its way to the end. A big difference between a machine’s and a person’s reading technique is that people don’t scrutinize every character and every chunk of white space (such as tabs and spaces), searching for meaning. A computer program doesn’t have ideas concerning the relative importance of spaces, indentation, and characters.

The very traits that make it possible for the programmer to quickly scan a Lisp file, noting the various function and variable declarations and the file’s general logical flow, are nothing but a time-consuming hindrance for a program. A Lisp interpreter spends time laboriously plowing through the very white space that makes a program human-readable in order to get at the “meat” of a file.

This was more of a problem in the early days of Emacs, when machines were slow and every means was taken to squeeze more efficiency from computer programs.

# The Byte-Compiler

The solution the Emacsen developers came up with is a Lisp program called the byte-compiler. This program is made up of several related Lisp files that join forces to transform a normal Lisp file into a more efficient form.

The byte-compiler can be thought of as a virtual machine, an emulated Lisp computer running within the actual hardware machine. Compiled-code executables, such as Emacsen or any other C or C++ program, directly access the computer’s hardware (though the operating system acts as an intermediary layer). The byte-compiler evaluates Lisp code and passes the results to Emacsen. This additional evaluation is responsible for the relative slowness of byte-compiled-as compared with compiled code, but there are advantages to this approach. Byte-compiled code is machine- and platform-independent. A byte-compiled Lisp file from a Linux machine will run equally well on a Windows or Space machine as long as the Emacsen versions are the same.

The idea of a virtual machine is also used in the Java language. A `.java` source file is compiled into a `.class` file; this is analogous to an Emacsen Lisp `.elc` byte-compiled file. A `.class` file is also portable between platforms because it is run within a Java virtual machine.
# Macro Libraries

Just as procedures macros may be gathered in libraries external to your program, so may macros be gathered into macro libraries. A macro library is really nothing but a text file that contains the source code for the macros in the library. Unlike procedures gathered into a module, macro libraries are not separately assembled and must be passed through the assembler each time the program is assembled. This is a problem with macros in general, not only with macros that are gathered into libraries. Programs that manage complexity by dividing code into macros we will assemble more slowly than programs that have been divided into separately assembled modules.

Macro libraries are used by including them into your program’s source code file. The means to do this is via the %include directive precedes the name of the macro library:

```
%include "MYLIB.MAC"
```

Technically this statement may be anywhere in your source code file, but you must keep in mind that all macros must be fully defined before they are invoked. For this reason, it's a good idea to use the %include directive near the top of your source code file, before any possible invocation of one of the library macros could occur.

If the macro file you want to include in a program is not in the same directory as NASM itself, you may need to provide a more complete DOS path specification as part of the %include directive:

```
%include "BOOK\MYLIB.MAC"
```

Otherwise, NASM may not be able to locate the macro file and will hand you a relatively unhelpful error message:

```
D:\NASM\BOOK\EATS5.ASM:18: unable to open file 'MYLIB.MAC'
```

The following is a macro library containing macro versions of all the procedures discussed in the previous section, plus a few more:

+   - Source name : MYLIB.MAC
- File type : NASM macro library
- Code model : Real mode OR flat model
- Version : 2.0
- Created date : 9/12/1999
- Last update : 9/18/1999
- Author : Jeff Dentemann
- Description : A simple example of a multi-line macro file for NASM containing utility procedures for
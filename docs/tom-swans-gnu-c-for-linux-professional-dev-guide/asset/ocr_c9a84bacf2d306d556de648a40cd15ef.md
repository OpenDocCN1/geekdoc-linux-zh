# Note

You might come across documentation that states a.out is an "old format" replaced by the ELF executable code format. Nowadays, a.out is in ELF format, and you don't need to do anything special to enable the newer system. To be sure, however, enter a Linux file command as follows and check the reported message:

```
$ file ./a.out
./a.out: ELF 32-bit LSB executable, Intel 80386,
 version 1, dynamically linked, not stripped
```

# THE OUTPUT FILE OPTION

Compiling programs to a.out is convenient for quick tests, but subsequent compilations overwrite the output file. To save a.out, you can rename the file using a mv command, but it's easier to specify an output filename in the first place. To do that, use the compiler's -o option in a command such as

```
$ g++ -o welcome welcome.cpp
```

Follow -o with the output filename. It's conventional to use the same filename as the source with no extension. You may specify a different name if you want. Some authorities say not to add a space after -o; others show the command as I do. If the preceding command fails for you, try -owelcome. After compiling, you can run the program by entering

```
$ ./welcome
Welcome to GNU C++ for Linux programming!
```

# Warning

Be especially careful when using the -o option to supply a filename. If you type a command such as g++ -o xxx.cpp, the compiler overwrites xxx.cpp! Always double check that you have supplied the name of a file after -o and that you are sure it is safe to overwrite the file.

# UNDERSTANDING THE WELCOME PROGRAM

Now that you know how to compile and run a C++ program, take a look at the source code in welcome.cpp (refer to Listing 4.1). The first line is a preprocessor directive. This is a command to the compiler that, in this case, tells it to include the declarations from a file named iostream.h, one of hundreds of similar header files that come with GNU C and C++. Include directives are usually in the following form:

```
#include <filename.h>
```

Although include directives might appear just about anywhere in a program's source code file, they are normally best located near the top above any other programming. The directive begins with #include, and is followed by a filename enclosed in angle brackets (otherwise known as less-than and greater-than signs). The preprocessor doesn't have to end
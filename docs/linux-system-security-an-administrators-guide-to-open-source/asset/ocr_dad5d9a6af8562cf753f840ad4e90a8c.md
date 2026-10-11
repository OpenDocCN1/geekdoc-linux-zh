and install it. We'll assume that the source directory for the bigcrypt version is /usr/src/c50aARC/src. Once you have installed libc-crypt, you will need to edit /usr/src/c50aARC/src/util/ecild.c and change the two lines (they are close to each other, but not next to each other)

```
#define PLAINTEXTSIZE    8
...
#undef CRYPT16
```

to

```
#define PLAINTEXTSIZE    16
...
#define CRYPT16
```

and now you are ready to compile.

# Preparing Crack for crypt (3)

You actually need to do nothing for standard crypt (3)-hashed passwords; however, the Crack distribution includes 1ibdes, a highly optimized hashing engine written by Eric Young. Your Linux system will likely come with libcrypt from the folks at GNU (this is the case with Red Hat 5.2/6.0). If you wish to use 1ibdes, simply change directories to the src/libdes subdirectory and execute make. This step is required if you are going to use Crack7 (see Crack7 on page 330).

# Compiling and Linking Crack

Once you have completed the necessary preliminary steps given in the section Modifying Crack for Linux on page 318 and the steps outlined for MD5 and/or Bigcrypt, you are ready to compile and link the programs comprising Crack.

Crack can be invoked with a number of different options. It turns out that if you invoke Crack to start work on a password file, it will compile and link all necessary programs that aren't already built. This may be useful once you know that it will build properly on a given platform; however, the first time through, you probably want to take a stepwise approach. The discrete steps to compile and link the cracking engine and then the dictionaries are outlined in the next two sections.

# Compiling Crack Itself

You've basically done all the work. To compile and link the various programs comprising Crack, simply execute crack -makeonly. Example 12-4 provides an illustration. That's all there is to it! Next you'll want to build the dictionaries.
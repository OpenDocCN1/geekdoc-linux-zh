The tdate.h header file begins with two directives that prevent its own text from being included more than once. At the end of the file is a third directive that corresponds to the first. Examine the three directives together—minus the class in between—to understand what the directives accomplish:

```
#ifndef __TDate_H
#define __TDate_H
... items processed only on the first include
#endif
```

The first directive ("if not defined") states to the compiler (actually the preprocessor) that if the symbol __TDate_H is not defined, then it should process the following statements. The first of those statements is another directive, which #defines the __TDate_H symbol. Subsequently, the next time this header is included by another module, the preprocessor recognizes the __TDate_H symbol, and it skips directly from #ifndef to the corresponding #endif at the end of the file. In other words, the header file is processed fully the first time it is included. If it is included additional times, the preprocessor ignores the file's contents. As a result, the TDate class is declared only once regardless of how many modules include tdate.h

> Note
> A "symbol" such as __TDate_H exists only during compilation. The symbol is not part of the program, nor does it need a value. All that matters is whether the symbol has been #defined. It is traditional to precede the symbol's name with two underscores, but this is not a requirement.

Getting back to TDate, notice that its two declared constructors are the same as in most other TDate classes you have seen. Because of that, you can use the new TDate class in most of the sample programming in this and the preceding chapter, even though its internal data representation has drastically changed. This principle points out one of the major advantages of restricting access to data members in classes. Because TDate's data is private to the class, that data representation is easily changed by merely updating the class module. Users of the class are unaffected by the change.

> Tip
> By always making data members private and using member functions to read and write the private data, you greatly simplify future updates to your programs. Follow this advice now, and you will thank yourself many times in the future.

# THE TDate MODULE

The second element of the TDate module is its implementation. This is best placed in another file, apart from the class declaration header, and should end with .cpp or another recognized C++ source code filename suffix. Listing 13.7, tdate.cpp, implements the TDate class as a separate module.
the Fancy interface:

```
module FancyModule {
  uses interface Fancy;
}

implementation {
  char *name = GLOBAL_NAME;
}
```

Listing 3.37 FancyModule.nc: C preprocessor pitfalls

Compiling FancyModule will report that GLOBAL_NAME is an unknown symbol. Why? The problem is that the first step in compiling FancyModule.nc is to preprocess it. At that point, the Fancy interface hasn’t been seen yet, therefore it hasn’t been loaded and the GLOBAL_NAME #define is unknown. Later on, when FancyModule is analyzed, the Fancy interface is seen, the Fancy.nc file is loaded and GLOBAL_NAME gets #defined. But this is too late to use it in FancyModule.nc.

There are two lessons to be drawn from this: first, as we’ve already seen, it’s best to use enum rather than #define to define constants when possible. Second, if you must use #define, use it as you would in C: place your definitions in a header file protected with #ifndef/#define, and #include this header file in all components and interfaces that use the #define symbol. For instance, both Fancy.nc and FancyModule.nc should

```
#include "Fancy.h"
```

where Fancy.h contains:

```
#ifndef FANCY_H
#define GLOBAL_NAME "fancy"
#endif
```

Listing 3.38 Fancy.h: the reliable way to use C preprocessor symbols

# **Programming Hint 10**  ALWAYS #DEFINE A PREPROCESSOR SYMBOL IN A HEADER FILE. USE #INCLUDE TO LOAD THE HEADER FILE IN ALL COMPONENTS AND INTERFACES THAT USE THE SYMBOL.

# 3.5.6  C libraries

Accessing a C library is easy. The implementation of the generic SineSensorC component uses the C library’s sin function, which is defined in the math.h header file:

```
#include <math.h>
generic module SineSensorC() {
  provides interface Init;
  provides interface Read<uint16_t>;
}
```
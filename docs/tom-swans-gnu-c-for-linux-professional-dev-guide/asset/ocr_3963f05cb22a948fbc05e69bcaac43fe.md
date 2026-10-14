This is called *automatic template instantiation*, and depending on your version of GNU C++, might or might not require a preceding function prototype. In any case, using `f()`’s template declaration, C++ performs two actions:

+   1. It instantiates the template, meaning that it writes the symbolic code for an actual function based on the data type (int here) for the placeholder type (T) in the function.
+   2. It compiles the generated function and stores its code in the current module.

Action number two is where the problem with templates comes into play. Consider now that the program expands into two modules, moduleA and moduleB. The second module also needs to call `f()` using an integer argument. So, on compiling moduleB, which also includes the template’s header file, the compiler generates another instance of `f(int)` and stores its code in moduleB’s object code file.

Now there are two identical instances of `f(int)`. Obviously, this is wasteful, and it complicates debugging. We want the compiler to recognize that it has already instantiated the function and to use that instantiation in all modules. But granting that wish isn’t half as easy as making it. The following sections discuss some of the solutions currently making the rounds in C++ compiler design.

# THE BORLAND MODEL

The Borland C++ model offers a simple solution to the proliferation of template instantiations. In this model, the compiler instantiates a template in each module. Using the example from the preceding paragraph, after compiling, the object-code files module.a and module.b (or any temporary files named similarly) contain identical instances of function `f(int)`. In other words, under this model, the compiler simply ignores the problem.

However, during linking, the Borland linker recognizes that the same function exists in multiple modules, and it collapses all such instances into one. This solves the problem but comes with a troublesome disadvantage. In a program with dozens of modules using the same template classes and functions, the compiler has to generate instances of all of them. This makes the compiler work harder than necessary, and as a consequence, programs that extensively use templates take longer to compile.

# THE CFRONT MODEL

The AT&T C++ to C translator, CFront, handles template instantiation differently. In this approach, a *template repository* is created during compilation of statements that use template classes and functions. The repository doesn’t contain code, but symbolic linker names and other information that enable the compiler to create the template instances that the linker needs. In other words, this is a two-pass system. On pass one, the compiler creates a repository that tells the linker where to find and, if necessary, how to create any template instances needed to complete the final code file.

There are two main advantages with this approach. One is a decrease in compilation time because template instantiation doesn’t occur until the program’s modules are linked
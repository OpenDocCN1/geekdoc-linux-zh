# EXPLANATION

+   1.  The `Dog.pm` module is in a directory called `MyPet`.
+   2.  This is a user-defined **import** function that will be automatically called when the user of this module says `use MyPet<,:Dog>`.
+   3.  Turning off `'refs'` for **strict** allows the program to use symbolic references; in this case, symbolic refs to `typeglob`s to **manipulate** the symbol table.
+   4.  Perl’s built-in `caller` function, with an argument `0`, returns the name of the package where this `import()` was called.
+   5.  Each symbol in the `foreach` list (`@speak`, `@eat`, and `@nap`) will be exported by this import routine to the caller's namespace.
+   6.  Here’s where we manipulate the user’s symbol table. A reference to each of the symbols in the list is assigned to the user’s package symbol table via a `typeglob`.

# 13.3 Modules from CPAN

You may want to use a module that has already been created by another programmer and stored somewhere other than in your library files. The best resource to start with is CPAN (the Comprehensive Perl Archive Network) a central repository for a collection of thousands of Perl modules. To find the CPAN mirror closest to you, go to `http://www.perl.com/CPAN`.

Perl modules that depend on each other are bundled together by name, author, and category. You can find these modules under the CPAN `modules` directory or by using the CPAN search engine at `http://metacpan.org`. If you need to install these modules, the CPAN documentation gives you easy-to-follow instructions. The home page for CPAN is shown in Figure 13.5.

![](bbox=[0.05, 0.67, 0.95, 0.94])

Figure 13.5 The CPAN homepage.
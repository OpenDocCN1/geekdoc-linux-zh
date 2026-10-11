
## EXPLANATION (CONTINUED)

- 4 `%name` is a global package variable and found on the symbol table, accessible by this and other packages.
- 5 Now we will loop through the symbol table for `%main::`. The key is the name of the identifier, and the value is the corresponding typeglob value. The typeglob is an alias for any type of that name; for example, `*main::friends` is an alias for `@friends`, `$friends`, `%friends`, `sub friends`, and so forth.

### EXAMPLE 13.4

```perl
(The Script)
1 package A; # Package declaration
use 5.010;
#use strict;
#use warnings;
2 sub count{
3   state $n = 1;
4   $n++;
return $n;
}
5 say count;
6 say count;
7 say count;
8 my $money=50000; # lexical, not a package variable
9 our @friends=qw(tom dick harry);
10 $name="Joe"; # package
11 package B; # Declare a new package
# Let's see what we can get from the A:: package
12 say "My money is: $A::money"; # Not a package variable
13 say "The state variable is not package variable $A::n.";
14 say "Your name is $A::name";
15 say "Call function in A package:" . A::count();
16 say "You can see your friends: @A::friends ";
17 say "and like this @friends"; # lexical scope
18 say "I am in scope: $money";
```

**(Output)**
5
2
6
3
7
4
12 My money is: ;
13 The state variable is not package variable .
14 Your name is Joe
15 Call function in A package: 5
16 You can see your friends: tom dick harry
17 and like this tom dick harry
18 I am in scope: 50000

## EXPLANATION

- 1 This is a declaration for package A. It will have its own namespace called `%A::`
- 2 **A subroutine**, *count*, is defined.
- 3 A *state variable*, `$n`, is declared and initialized. This is just like a `my` variable in that it is lexically scoped, except it will never be reinitialized and will retain its value from one call of the function to the next. The variable will go out of scope when the function block ends. It is not in the symbol table for this package and can only be accessed when the function is called.
- 4 Every time the function is called, the value of `$n` is increased by one.
- 5–7 The *count* function is global in scope for package A. Its name is on the symbol table and it is available to other packages. It is called three times.
- 8 *Money* is declared as a lexically scoped *my* variable. It is given its own private scratch pad and visible from the point of declaration until the end of the block or file. It is not on the symbol table.
- 9 `@*friends` is declared as an *our* variable. It is global for the package and is found on the symbol table. It is just like *my* and *state* variables in that it is lexically scoped but isn't allocated a private scratch pad. Its value is not printed.
- 10 `$name` is a global package variable for package A.
- 11 Package B is declared. We now switch from package A to package B. Each package has its own symbol table. From this point on until the program ends or unless another package is declared, the B package is in scope.
- 12 To access the variable *Money* in package A, first the dollar sign is prepended to the package name to indicate that the type of the variable is a scalar, followed by the name of the package, A, two colons, and the variable name, *Money*. This allows you to switch namespaces from within this package. But *Money* is a *my* variable, **not a package variable**, and therefore is not associated with the symbol table for package A.
- 13 The *state* variable `$n` is like the *my* variable in that it is not associated with a symbol table and cannot be accessed from package A's symbol table.
- 14 The global package variable, `$name`, is available to this package by qualifying its name with `A::` since it is on the symbol table for package A.
- 15 The subroutine, *count*, is also global and was defined in package A. We can call the subroutine by qualifying its name as `A::count()`. We have access to the state variable within the subroutine and, as you can see, the count has gone up to 5.
- 16, 17 `@*friends` was declared in package A as an *our* variable. It is a package variable and can be accessed in two ways: by fully qualifying its name with the package name, or, in this example, because it is in file scope, it can be accessed as on line 17.
- 18 The *Money* variable was declared in package A as a lexically scoped *my* variable. It is still in scope, but cannot be accessed as `$A::money` because it isn't in A's symbol table. It isn't associated with any package.

## 13.2 The Standard Perl Library

![Figure 13.4](img/8556abcb353c0991f12099420ec28735_446_0.png)

Figure 13.4 Accessing package variables.

The Perl distribution comes with a number of standard Perl library functions and packages. The Perl 4 library routines are procedural programs and their names end in a `.pl` extension. The Perl 5 modules end with a `.pm` extension. In Perl 5, the `.pm` files are called **modules**. The `.pm` files are modules written in two programming styles: procedural and object-oriented. The module filenames start with a capital letter. The `.pm` filenames starting with a lowercase letter are a special type of module, called a **pragma**. A **pragma** is a module that tells the compiler that certain conditions must be checked in a Perl program before it can run. Files that have no extension at all are subdirectories. They contain common modules that are divided into several `.pm` files; for example, the Math subdirectory contains *BigFloat.pm*, *BigInt.pm*, *Complex.pm*, and *Trig.pm*.

The following is a sample listing from the standard Perl 5.18 library:

| Col 1 | Col 2 | Col 3 | Col 4 | Col 5 |
| :--- | :--- | :--- | :--- | :--- |
| ActivePerl | Bit | Compress | Data | Errno.pm |
| ActivePerl.pm | Bundle | Config | Date | Eval |
| ActiveState | CGI | Config.pm | Devel | Exception |
| Algorithm | CGI.pm | Config.pod | Digest | Exporter |
| AnyDBM_File.pm | CORE | Config_gn.pl | Digest.pm | Exporter.pm |
| App | CORE.pod | Config_heavy.pl | DrvHandle.pm | ExtUtils |
| Archive | CPAN | Cwd.pm | Dist | Fatal.pm |
| Attribute | CPAN.pm | DB.pm | Dumpvalue.pm | Fcntl.pm |
| AutoLoader.pm | CPANPLUS | DBD | DynaLoader.pm | File |
| AutoSplit.pm | CPANPLUS_pm | DBI | Email | FileCache.pm |
| B | Carp | DBI.pm | Encode | FileHandle.pm |
| B.pm | Carp.pm | DBM_Filter | Encode.pm | Filter |
| BSD | Class | DBM_Filter.pm | English.pm | FindBin.pm |
| Benchmark.pm | Clone.pm | DB_File.pm | Env.pm | GD |
| GD.pm | O.pm | Symbol.pm | autodie | mro.pm |
| Getopt | Object | Sys | autodie.pm | mylib.pm |
| HTML | Opcode.pm | TAP | autouse.pm | newgetopt.pl |
| HTTP | POSIX.pm | Task | base.pm | oase.pm |
| Hash | POSIX.pod | Tcl | benchmark.pl | opn.pm |
| II8N | PPI | Tcl.pm | bigint.pm | ops.pm |
| IO | PPI.pm | Term | bignum.pm | overload |
| IO.pm | PPIx | Test | bigint.pm | overload.pm |
| IPC | PPM | Test.pm | lib.pm | overloading.pm |
| JSON | Package | Text | bytes.pm | parent.pm |
| JSON.pm | Params | Thread | bytes_heavy.pl | perl5db.pl |
| LWP | Parse | Thread.pm | charnames.pm | perlfaq |
| LWP.pm | Perl | Tie | constant.pm | perllocal.pod |
| List | PerlIO | Time | dbiixs_revp | pods |
| Locale | PerlIO.pm | Tlx | deprecate.pm | re.pm |
| Log | Pod | Tlx.pm | diagnostics.pm | sigtrap.pm |
| MIME | Readonly | Try | dumpvar.pl | sort.pm |
| MLDBM | Readonly.pm | UNIVERSAL.pm | encoding | strict.pm |
| MLDBM.pm | SDBM_File.pm | URI | encoding.pm | subs.pm |
| MRO | SQL | URI.pm | feature.pm | threads |
| Mac | Safe.pm | Unicode | fields.pm | threads.pm |
| Math | Scalar | User | ftest.pm | unire |
| Memoize | Search | Win32 | inc | utf8.pm |
| Memoize.pm | SelectSaver.pm | XML | integer.pm | utf8_heavy.pl |
| Module | SelfLoader.pm | XSLoader.pm | less.pm | vars.pm |
| Moose | SelfLoader.pm | YAML | lib.pm | version |
| Moose.pm | Shell | _charnames.pm | local.pm | version.pod |
| Mozilla | Socket.pm | arybase.pm | lib.pm | vmish.pm |
| NDBM_File.pm | Storable.pm | attributes.pm | libpod.pod | warnings |
| NEXT.pm | Sub | auto | metaclass.pm | warnings.pm |
| Net | | | | |

> 2. The pathname to the standard Perl library is determined at the time Perl is installed. This can be assigned either a default value or a pathname designated by the person installing Perl.

### **13.2.1 The @INC Array**

The special array `@INC` contains the directory path to where the library modules are located and is set when Perl is installed. To include directories not in the `@INC` array, you can use the `-I` switch at the command line, or set the `PERLLIB` environment variable to the full pathname. Normally, this variable is set in one of your shell initialization files, either *login* or *profile* if using UNIX.
